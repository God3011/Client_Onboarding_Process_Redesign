# Improvement Memo: Client Onboarding

**Document:** 04 of 05 - Improvement Recommendations
**Version:** 1.0
**Date:** August 2026
**To:** Founder / Operations Head
**Re:** Five recommended changes to client onboarding, and one deliberate exclusion

---

## Summary

The current process was mapped in `01-current-state.md` and five failure points were
identified. This memo recommends a change for each, with expected impact, implementation
effort, and the risk each change introduces.

The changes are ordered by leverage, not by sequence in the process. R1 and R4 address
the two places where time is most reliably lost. R3 addresses the failure with the
highest downstream cost.

One further change was considered and is **not** recommended. It is set out in section 6,
because the reasoning for not doing it matters as much as the reasoning for the rest.

| ID | Addresses | Change | Effort |
|---|---|---|---|
| R1 | P1 | Automated intake with single named owner | 2 days |
| R2 | P2 | Tracker with retained stage history | 2 days |
| R3 | P3 | Mandatory written handoff brief | 0.5 days |
| R4 | P4 | Consolidated access request with escalation ladder and clock pause | 1 day |
| R5 | P5 | Documented build-versus-configure criteria | 1 day |
| - | P5 | **Not recommended:** automating the build-versus-configure decision | - |

---

## 1. R1 - Automated intake with a single named owner

**Addresses:** P1 - enquiry alert has no named owner

### Problem

Inbound enquiries alert sales leads, the ops team, and managers simultaneously. Three
parties receive the same notification and none owns it. Each assumes another has picked
it up. There is no first-response clock and no record of who acted, so an unclaimed lead
produces no signal until someone notices it in the sheet days later.

### Proposed change

Route all enquiries through a structured intake form feeding an automation that:

- validates the submission and diverts malformed entries to a separate error log
- classifies the enquiry by service category and urgency using an LLM
- writes a structured record to the intake sheet with a timestamp
- alerts a single named on-duty Sales Lead for high-urgency enquiries only
- routes everything else to a standard queue reviewed daily

Built and running. See `make-automation/`.

### Expected impact

First contact becomes measurable, because assignment is timestamped and automatic. The
4-hour SLA at step 2 of the SOP becomes enforceable rather than aspirational. Urgent
enquiries surface immediately rather than waiting for someone to read the queue.

The classification also produces a structured record where there was previously only
free text, which makes category and urgency mix visible for the first time.

### Effort

2 days. Built on Make free tier and the Gemini free tier. No recurring cost at current
volume.

### Risks

**The classifier will be wrong sometimes.** An enquiry classified low that is genuinely
urgent will sit in the standard queue. Mitigations in place: the standard queue is
reviewed daily rather than on alert, the alert email shows the client's own service
selection alongside the AI classification so disagreement is visible, and the alert
states explicitly that the classification may be wrong.

**Dependency on two external services.** If Make or Gemini is unavailable, intake stops.
An error handler writes the raw submission to the sheet with a failure flag so nothing
is lost, but the classification and alert would not fire. At current volume the fallback
is manual review of the sheet, which is the status quo.

**Phone enquiries bypass the automation.** These must be entered into the form manually
by whoever takes the call. This is a real gap and depends on discipline rather than
tooling.

---

## 2. R2 - Tracker with retained stage history

**Addresses:** P2 - leads sheet holds status but no history

### Problem

The leads sheet records a current status only. It does not record when the status was
set, by whom, or what preceded it. Two consequences follow. The 2-day follow-up cadence
is unenforceable because nothing stores the date of last contact. And no cycle-time
analysis is possible, because the data to support it was never captured.

### Proposed change

Replace the leads sheet with a tracker covering the full engagement rather than the lead
stage only. One row per engagement, with stage, owner, date entered, and an automatic
SLA status. Every stage transition appends a dated row to a history tab.

A summary tab shows live count by stage, engagements breaching or at risk, average cycle
time, and average days per stage.

Design specified in `03-tracker.md`.

### Expected impact

Follow-up compliance becomes visible rather than dependent on memory. Breaches surface
at 80 percent of the allowed time rather than after the deadline has passed.

The more significant gain is diagnostic. Average days per stage and breach rate by stage
identify where the process actually loses time, which is currently unknown and is
therefore guessed at. This is the data that should drive the next round of improvements.

### Effort

2 days to build and populate. Ongoing effort is one update per engagement per stage
transition, roughly 2 minutes.

### Risks

**Manual updates decay.** A tracker only reflects reality if people update it. At 10 to
15 live engagements this is manageable; past roughly 30 it will need automating or it
will quietly stop being accurate.

**A stale tracker is worse than no tracker,** because decisions get made on it. The
30-day review at SOP step 23 should include a check that tracker state matched reality.

---

## 3. R3 - Mandatory written handoff brief

**Addresses:** P3 - sales-to-delivery handoff is verbal and lossy

### Problem

The Sales Lead briefs the Tech Lead and Account Lead on a call. Everything learned during
the sales conversation exists in the Sales Lead's head and in an email chain. The call
transfers whatever the Sales Lead remembers to mention, and nothing is written down in a
form the delivery team can refer back to.

The highest cost is around informal commitments. A client told during the sales call that
something "should be straightforward to include" will expect it at delivery. If that never
reached the Tech Lead, it surfaces as a scope dispute weeks later, after the build decision
has been made on incomplete information.

### Proposed change

The handoff call is retained, but a written brief becomes the deliverable and the call
reviews it. The brief covers: stated problem, current process, systems in scope, explicit
exclusions, **commitments made during the sales conversation**, known constraints, and
client contacts with roles.

Tech Lead and Account Lead acknowledge receipt. The brief is filed in the project folder.

Paired with a change at SOP step 3: any commitment made during the requirements call is
written to the lead record at the time it is made, not reconstructed at handoff.

### Expected impact

Scope disputes become resolvable against a record rather than against recollection. The
SOP's exception path E3 turns on exactly this: if a client asserts something was promised,
the Account Lead checks the brief. Recorded means in scope and delivered without charge.
Not recorded means it is treated as a change request.

That rule is only fair, and only enforceable, if the brief is reliably complete.

### Effort

0.5 days to write the template. Roughly 20 minutes per engagement thereafter.

This is the cheapest of the five changes and addresses the failure with the highest
downstream cost.

### Risks

**The brief becomes a formality.** A Sales Lead under time pressure will write a thin
brief that technically satisfies the requirement. The Tech Lead's acknowledgement is the
control here - acknowledging a brief that is obviously incomplete should be treated as a
process failure, not a formality.

**Commitments may still go unrecorded** if the Sales Lead does not recognise something as
a commitment when saying it. The template asks directly - "what did you tell the client we
would do?" - rather than leaving it to judgement.

---

## 4. R4 - Consolidated access request with escalation ladder and clock pause

**Addresses:** P4 - access delays are untracked and unescalated

### Problem

Access provisioning is the one step where progress depends entirely on someone outside
the firm, and it is the most common cause of onboarding slippage. Nothing tracks how long
a request has been outstanding, nobody is designated to chase it, and there is no
escalation threshold.

Because the delay is invisible, it is also attributed wrongly. The engagement appears
slow, and the cause is not recorded anywhere that would show it was a client-side
dependency.

### Proposed change

Three parts.

**One consolidated request.** Every system needed, listed once, with the access level
required, the named person on the client side responsible for each, and the date needed.
Piecemeal requests restart the client's internal approval process each time.

**An escalation ladder.** Chase at day 3 by the Ops Associate. Escalate at day 5, Account
Lead to client decision-maker directly. Notify the Founder and flag the engagement at
risk at day 10.

**A clock pause.** The engagement clock pauses when the step begins and resumes when it
completes. A client who takes six days to provide access moves the delivery date by six
days, and that shift is recorded against the access step rather than absorbed by delivery.

Verification is also separated from provisioning. The Ops Associate confirms every access
point works before kickoff rather than accepting the client's assurance.

### Expected impact

Client-side delay becomes visible, owned, and correctly attributed. The clock pause
protects the delivery timeline without stopping the chase - the ladder runs during the
pause.

Separating verification prevents the common failure of discovering during kickoff that
credentials do not work, which wastes the call and requires a second one.

### Effort

1 day to write the request template and add the tracking columns. No tooling required.

### Risks

**The clock pause can be read as excuse-making.** A client who sees their delivery date
move will not always accept that the cause was on their side. Mitigated by stating the
rule in the proposal and at kickoff, before it is ever invoked. Applying it retroactively
would damage trust.

**Escalating at day 5 to the decision-maker may irritate the client contact,** whose own
IT approval chain may be the real constraint. The ladder should be applied with judgement -
the Account Lead should know whether the delay is the contact or their organisation.

---

## 5. R5 - Documented build-versus-configure criteria

**Addresses:** P5 - build-versus-configure decision has no stated criteria

### Problem

This is the highest-leverage decision in the process. It determines whether the client
receives a solution in days or in two weeks, and it drives margin on the engagement. It
is currently made on the Tech Lead's judgement with no written criteria.

Undocumented judgement is not necessarily wrong. An experienced Tech Lead will usually
get it right. The problem is that it is unauditable and non-transferable. The same
requirement could receive different decisions from different people, the reasoning is not
available to anyone reviewing the engagement later, and a new Tech Lead has nothing to
learn from.

It also creates a quiet incentive problem. With no criteria to point at, the path of least
resistance under delivery pressure is to configure something existing and stretch it to fit.

### Proposed change

Four criteria on each side, with a 5-working-day configuration-effort threshold as the
tiebreaker. Where criteria conflict, the Tech Lead decides and records why. Full criteria
are in SOP step 17.

The decision and its reasoning are recorded and reviewed at the 30-day review, which is
what makes the criteria improvable over time.

### Expected impact

Decisions become consistent across people and auditable after the fact. The 30-day review
gains a specific question it can answer: did the build-versus-configure call prove correct?

The recorded reasoning is also the raw material for refining the criteria. The 5-day
threshold is a starting estimate and should move once there is data on how configured
solutions that exceeded it actually performed.

### Effort

1 day to draft the criteria and agree them with the Tech Lead. The criteria are a
starting point and should be revised at the first quarterly review.

### Risks

**The threshold is a guess.** Five days is a reasonable starting number, not a measured
one. It should be treated as provisional until there is data.

**Criteria can be gamed.** An effort estimate that determines the outcome is an estimate
someone has an incentive to shade. The recorded reasoning is the control - an estimate
that turns out to be badly wrong is visible at the 30-day review.

---

## 6. Considered and not recommended: automating the build-versus-configure decision

An obvious extension of R1 is to apply the same classification approach to step 17. The
inputs are structured - the scope note, the systems list, the product catalogue - and an
LLM could plausibly produce a recommendation.

**This is not recommended.**

### Why not

**The decision depends on knowledge that is not written down anywhere.** Whether a gap
can be closed by configuration rather than code depends on the actual state of the
existing products, including known fragilities, half-finished features, and which
components other clients depend on. None of that exists in a form a model could read. It
lives with the Tech Lead.

**The cost of a wrong answer is asymmetric.** A misclassified enquiry at intake costs a
few hours - it sits in the wrong queue until someone notices. A wrong build-versus-configure
call costs a rebuild, a missed delivery date, or a configured product stretched past what
it can support and generating maintenance cost for every subsequent client on it.

**Automation would import a bias, not remove one.** The existing incentive problem is a
drift toward configuring under pressure. A model given a product catalogue and asked
whether an existing product fits will tend toward yes, because that is the shape of the
question. Automating it would make an existing bias faster and harder to see, while
appearing to make the decision objective.

**The problem was never that the decision was slow.** It was that it was unauditable.
Written criteria and recorded reasoning solve that. Automation solves a problem this
process does not have, and creates one it currently does not have either.

### What to do instead

R5, and revisit at the quarterly review. If the recorded reasoning shows the criteria are
being applied consistently and the 30-day reviews show the calls were right, the decision
is working as a human judgement and should stay one.

If the reviews show inconsistency, the answer is still not automation - it is better
criteria, or a second reviewer on borderline cases.

---

## 7. Sequencing

| Order | Change | Why this order |
|---|---|---|
| 1 | R3 - handoff brief | Cheapest, addresses the highest-cost failure, no tooling |
| 2 | R4 - access request and ladder | No tooling, addresses the most common source of slippage |
| 3 | R1 - intake automation | Already built, needs adoption rather than build |
| 4 | R2 - tracker | Depends on the stage definitions the SOP settles |
| 5 | R5 - decision criteria | Requires Tech Lead time to agree, benefits from R2 data |

R3 and R4 require no tooling and can be adopted immediately. R2 should follow rather than
lead, because its stage list depends on the SOP being settled first.

---

## 8. What would change these recommendations

**If volume grows past roughly 30 live engagements,** R2's manual tracker becomes
unsustainable and should be replaced with something that updates from system events rather
than by hand.

**If the classification in R1 proves unreliable** - more than roughly one in ten enquiries
misrouted - the alert threshold should widen to include medium urgency rather than the
classifier being tuned. A wider net is cheaper than a better model at this volume.

**If scope disputes continue after R3,** the problem is not the brief but what is being
promised during sales, and the fix moves upstream to the requirements call.
