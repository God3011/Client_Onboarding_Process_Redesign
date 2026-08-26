# Onboarding Tracker

**Document:** 03 of 05 - Tracker Design
**Version:** 1.0
**Built in:** Google Sheets

---

## Purpose

The tracker is the operational counterpart to the SOP. The SOP says how the process
should run; the tracker says where every live engagement currently is and which ones
need attention today.

It answers three questions that could not be answered before:

1. Where is each client in the process, and who owns them right now?
2. Which engagements are breaching an SLA or approaching one?
3. Where does the process lose time, across all engagements?

---

## Design principles

**One row per engagement.** Not one row per step. Stage is a column, not a tab. This
keeps the sheet readable at 10 to 15 live engagements, which is the realistic load at
8 new clients a month.

**Status history is retained.** Each stage transition writes a dated entry rather than
overwriting the previous value. This was pain point P2 - a single status field records
where something is but not how long it took to get there, which makes cycle-time
analysis impossible.

**The tracker flags, it does not decide.** Conditional formatting surfaces breaches and
at-risk items. A human decides what to do about them. The tracker never sends anything
or changes an owner automatically.

---

## Tab 1: `Engagements`

One row per live engagement.

| Col | Header | Type | Contents |
|---|---|---|---|
| A | `engagement_id` | Text | `WF-2026-001`, sequential |
| B | `company` | Text | Client company name |
| C | `stage` | Dropdown | Current stage - see stage list below |
| D | `owner` | Dropdown | Role currently responsible |
| E | `stage_entered` | Date | Date the current stage began |
| F | `days_in_stage` | Formula | Business days elapsed |
| G | `sla_days` | Formula | SLA for the current stage, looked up |
| H | `sla_status` | Formula | On track / At risk / BREACH / Paused |
| I | `clock_paused` | Checkbox | TRUE while waiting on the client |
| J | `engagement_start` | Date | Date of first enquiry |
| K | `total_days` | Formula | Business days since enquiry |
| L | `at_risk` | Checkbox | Set manually at day 10 escalation |
| M | `notes` | Text | Free text |

### Stage list (column C dropdown)

```
1. Lead - awaiting first contact
2. Lead - requirements call
3. Lead - ongoing follow-up
4. Proposal sent
5. Awaiting signature
6. Awaiting advance payment
7. Handoff
8. Internal setup
9. Access requested
10. Access verification
11. Awaiting kickoff
12. Build decision
13. In build
14. Handover
15. Awaiting sign-off
16. Closed - in support
17. On hold
```

### Owner list (column D dropdown)

```
Sales Lead
Ops Associate
Account Lead
Tech Lead
Delivery Consultant
Finance
Client
```

---

## Formulas

Enter in row 2 and fill down.

**F - days_in_stage**

```
=IF(E2="","",NETWORKDAYS(E2,TODAY()))
```

`NETWORKDAYS` counts business days only, which matches how the SOP states its SLAs.

**G - sla_days** (looks up the SLA for the current stage from the `SLA_Reference` tab)

```
=IFERROR(VLOOKUP(C2,SLA_Reference!$A$2:$B$18,2,FALSE),"")
```

**H - sla_status**

```
=IF(OR(F2="",G2=""),"",
  IF(I2=TRUE,"Paused",
    IF(F2>G2,"BREACH",
      IF(F2>=G2*0.8,"At risk","On track"))))
```

The `0.8` threshold flags an engagement when it has used 80 percent of its allowed time,
so the warning arrives while there is still time to act rather than after the fact.

**K - total_days**

```
=IF(J2="","",NETWORKDAYS(J2,TODAY()))
```

---

## Tab 2: `SLA_Reference`

A lookup table so SLAs live in one place and can be changed without editing formulas.

| A - stage | B - sla_days | C - type |
|---|---|---|
| 1. Lead - awaiting first contact | 1 | Internal |
| 2. Lead - requirements call | 1 | Internal |
| 3. Lead - ongoing follow-up | 2 | Internal |
| 4. Proposal sent | 3 | Internal |
| 5. Awaiting signature | 5 | Client-dependent |
| 6. Awaiting advance payment | 5 | Client-dependent |
| 7. Handoff | 2 | Internal |
| 8. Internal setup | 1 | Internal |
| 9. Access requested | 5 | Client-dependent |
| 10. Access verification | 1 | Internal |
| 11. Awaiting kickoff | 3 | Internal |
| 12. Build decision | 2 | Internal |
| 13. In build | 10 | Internal |
| 14. Handover | 3 | Internal |
| 15. Awaiting sign-off | 5 | Client-dependent |
| 16. Closed - in support | | |
| 17. On hold | | |

Column C is not used in a formula but makes the internal/client-dependent distinction
visible to anyone reading the sheet.

---

## Tab 3: `Stage_History`

Appended to on every stage transition. This is what makes cycle-time analysis possible.

| Col | Header | Contents |
|---|---|---|
| A | `engagement_id` | Matches Engagements!A |
| B | `stage` | Stage being exited |
| C | `entered` | Date entered |
| D | `exited` | Date exited |
| E | `days` | `=NETWORKDAYS(C2,D2)` |
| F | `breached` | `=IF(E2>VLOOKUP(B2,SLA_Reference!$A$2:$B$18,2,FALSE),TRUE,FALSE)` |
| G | `changed_by` | Who moved it |

---

## Tab 4: `Summary`

Read-only dashboard.

**Live count by stage**

In A2 down, paste the stage list. In B2:

```
=COUNTIF(Engagements!$C$2:$C$200,A2)
```

**SLA status counts**

```
On track:  =COUNTIF(Engagements!$H$2:$H$200,"On track")
At risk:   =COUNTIF(Engagements!$H$2:$H$200,"At risk")
BREACH:    =COUNTIF(Engagements!$H$2:$H$200,"BREACH")
Paused:    =COUNTIF(Engagements!$H$2:$H$200,"Paused")
```

**Average cycle time** - all completed engagements

```
=IFERROR(AVERAGEIF(Engagements!$C$2:$C$200,"16. Closed - in support",Engagements!$K$2:$K$200),"No completions yet")
```

**Average days per stage** - the diagnostic view, showing where the process loses time

In A down, the stage list. Alongside:

```
=IFERROR(AVERAGEIF(Stage_History!$B$2:$B$500,A2,Stage_History!$E$2:$E$500),"")
```

**Breach rate by stage**

```
=IFERROR(COUNTIFS(Stage_History!$B$2:$B$500,A2,Stage_History!$F$2:$F$500,TRUE)/COUNTIF(Stage_History!$B$2:$B$500,A2),"")
```

This last one is the most useful number in the tracker. It shows which stage breaches
most often, which is where process improvement effort should go next.

**Engagements at risk** - a filtered live view

```
=FILTER(Engagements!A2:D200,(Engagements!H2:H200="BREACH")+(Engagements!L2:L200=TRUE))
```

---

## Conditional formatting

On `Engagements`, applied to the whole row via a custom formula rule:

| Rule | Formula | Format |
|---|---|---|
| Breach | `=$H2="BREACH"` | Red background |
| At risk | `=$H2="At risk"` | Amber background |
| Paused | `=$H2="Paused"` | Grey text, italic |
| Flagged at risk | `=$L2=TRUE` | Red left border |

Apply to range `A2:M200`, and use `$H2` with the dollar sign on the column only so the
rule reads across the whole row.

---

## What the tracker deliberately does not do

**It does not send reminders.** Chasing is assigned to a named person in the SOP. A
tracker that emails people creates the same diffusion of responsibility as the broadcast
alert in pain point P1 - everyone receives the nudge, nobody owns it.

**It does not move stages automatically.** A stage transition is a judgement that
something is genuinely complete. Automating it on a date or a checkbox would let
engagements advance on paper while stalled in reality.

**It does not calculate a health score.** A single composite number would hide the
detail that makes the tracker useful. The breach flag and the stage are more actionable
than any index built on top of them.
