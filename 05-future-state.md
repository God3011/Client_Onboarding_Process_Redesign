# Future State: Client Onboarding

**Document:** 05 of 05 - Future State Map
**Version:** 1.0
**Changes applied:** R1 through R5 from `04-improvement-memo.md`

---

## What changed

| ID | Change | Visible in the map as |
|---|---|---|
| R1 | Automated intake with single named owner | New automation lane replacing the broadcast alert |
| R2 | Tracker with retained stage history | Tracker lane, written to at each stage transition |
| R3 | Mandatory written handoff brief | Brief produced before the handoff call, not after |
| R4 | Consolidated access request, escalation ladder, clock pause | Pause marker and ladder on the access step |
| R5 | Documented build-versus-configure criteria | Decision node now references written criteria |

---

## Future-state map

```mermaid
flowchart TB

    subgraph CLIENT["CLIENT"]
        C1["Submits enquiry<br>via intake form"]
        C8["Signs NDA and<br>service agreement"]
        C10["Pays advance<br>invoice"]
        C15["Provides system<br>credentials"]
        C22["Gives written<br>sign-off"]
    end

    subgraph AUTO["INTAKE AUTOMATION"]
        A1{"Submission<br>valid?"}
        A2["Logs to<br>error sheet"]
        A3["Classifies category<br>and urgency"]
        A4{"Urgency<br>high?"}
        A5["Alerts on-duty<br>Sales Lead"]
        A6["Writes to<br>standard queue"]
    end

    subgraph SALES["SALES LEAD"]
        S2["Makes first contact<br>SLA 4 hours"]
        S3["Requirements call<br>logs commitments"]
        S4{"Lead<br>status?"}
        S5["Follows up<br>every 2 days"]
        S6["Sends proposal<br>SLA 3 days"]
        S11["Writes handoff brief<br>then reviews on call"]
        SX["Closed<br>not converted"]
    end

    subgraph FINANCE["FINANCE"]
        F9["Raises advance<br>invoice SLA 1 day"]
        F10["Confirms payment<br>hard gate"]
        F23["Raises final<br>invoice"]
    end

    subgraph OPS["OPS ASSOCIATE"]
        O13["Creates project folder<br>and channel"]
        O14["Sends consolidated<br>access request"]
        O15["Chases per ladder<br>day 3 / 5 / 10"]
        O16["Verifies every<br>access point works"]
    end

    subgraph ACCOUNT["ACCOUNT LEAD"]
        AC12["Introduced as single<br>point of contact"]
        AC17["Kickoff call<br>issues scope note"]
        AC22["Requests written<br>sign-off"]
        AC24["Moves to support<br>schedules 30-day review"]
    end

    subgraph TECH["TECH LEAD"]
        T18{"Existing product fits?<br>4 criteria each way<br>5-day threshold"}
        T20["Two-week build<br>mid-point check-in"]
    end

    subgraph DELIVERY["DELIVERY CONSULTANT"]
        D19["Configures and<br>deploys"]
        D21["Handover and<br>client walkthrough"]
    end

    subgraph TRACKER["TRACKER"]
        TR["Stage, owner, SLA status<br>history appended on<br>every transition"]
    end

    C1 --> A1
    A1 -->|no| A2
    A1 -->|yes| A3 --> A4
    A4 -->|yes| A5
    A4 -->|no| A6
    A5 --> S2
    A6 --> S2
    S2 --> S3 --> S4
    S4 -->|ongoing| S5 --> S3
    S4 -->|not converted| SX
    S4 -->|converted| S6 --> C8 --> F9 --> C10 --> F10 --> S11
    S11 --> AC12 --> O13 --> O14 --> C15
    C15 -.->|no response| O15
    O15 -.-> C15
    C15 --> O16 --> AC17 --> T18
    T18 -->|configure| D19 --> D21
    T18 -->|build| T20 --> D21
    D21 --> AC22 --> C22 --> F23 --> AC24

    A3 -.-> TR
    S4 -.-> TR
    F10 -.-> TR
    O14 -.-> TR
    AC17 -.-> TR
    T18 -.-> TR
    AC24 -.-> TR

    classDef fixed fill:#e3f9e5,stroke:#2b8a3e,stroke-width:2px,color:#000
    classDef paused fill:#fff9db,stroke:#e67700,stroke-width:2px,color:#000
    class A1,A3,A4,A5,A6,S3,S11,O14,O16,T18 fixed
    class C15,O15 paused
```

**Green nodes** are steps changed by R1 to R5. **Amber nodes** are the client-dependent
access step where the engagement clock pauses and the escalation ladder runs.

---

## Before and after, by pain point

### P1 - Enquiry alert has no named owner

**Before:** alert fires to sales leads, ops, and managers at once. No owner, no clock,
no record of who acted.

**After:** intake automation assigns one named on-duty Sales Lead. Assignment is
timestamped, so the 4-hour first-contact SLA is measurable. High-urgency enquiries alert
immediately; everything else lands in a queue reviewed daily.

### P2 - Leads sheet holds status but no history

**Before:** a single status field, overwritten. Follow-up cadence unenforceable, cycle
time unmeasurable.

**After:** tracker retains a dated history of every stage transition. Follow-up compliance
is visible, SLA breaches flag at 80 percent of allowed time, and average days per stage
shows where the process loses time.

### P3 - Sales-to-delivery handoff is verbal and lossy

**Before:** a call transferring whatever the Sales Lead remembers. Nothing written.

**After:** a written brief is the deliverable and the call reviews it. Commitments made
during sales are recorded at the time they are made. Scope disputes resolve against a
record rather than recollection.

### P4 - Access delays are untracked and unescalated

**Before:** invisible dependency. No chase owner, no threshold, delay wrongly attributed
to delivery.

**After:** one consolidated request, an escalation ladder at day 3, 5, and 10, and a clock
pause that moves the delivery date by exactly the delay the client caused. Verification is
separated from provisioning, so credential failures surface before kickoff rather than
during it.

### P5 - Build-versus-configure decision has no stated criteria

**Before:** undocumented judgement. Unauditable, non-transferable, quietly biased toward
configuring under pressure.

**After:** four criteria each way with a 5-day effort threshold. Decision and reasoning
recorded, reviewed at the 30-day review. The decision remains a human judgement - see
section 6 of the improvement memo for why automating it was rejected.

---

## What the map does not show

**The 30-day review loop.** Step 24 schedules a review that feeds back into the criteria
at step 18 and into the SLA reference table. Drawing that edge would make the map harder
to read, but the loop is the mechanism by which this process improves rather than
ossifying.

**Exception paths.** E1 through E5 in the SOP cover unresponsive clients, failed access,
scope change, non-payment, and repeated kickoff rescheduling. Each is a branch that would
triple the node count. The map shows the intended path; the SOP covers what happens when
it does not hold.

**Volume limits.** The tracker is manual. Past roughly 30 live engagements it stops being
reliable, and the process would need a different tool rather than a different design.
