# SOP: Client Onboarding

**Document:** 02 of 05 - Standard Operating Procedure
**Version:** 1.0
**Effective:** August 2026
**Owner:** Operations
**Review cycle:** Quarterly

---

## 1. Purpose

This procedure defines how wrkflow.ai takes a client from first enquiry through to a
signed-off delivery. It exists so that onboarding runs the same way regardless of who
handles it, so that every client has a named owner at every stage, and so that delays
are visible while they are happening rather than discovered afterwards.

## 2. Scope

**Covers:** enquiry received through to delivery signed off and the account moved to
ongoing support.

**Does not cover:** the ongoing support relationship past the 30-day review, internal
resourcing decisions, or technical delivery methodology.

## 3. Definitions

| Term | Meaning |
|---|---|
| **SLA** | A deadline binding on a wrkflow.ai role. A missed SLA is an internal failure and is recorded as such. |
| **Client-dependent step** | A step whose completion depends on the client. These carry a target, not an SLA, and are governed by the escalation ladder in section 6. |
| **Engagement clock** | The elapsed-time count against the delivery timeline quoted to the client. |
| **Business hours** | 10:00 to 18:00 IST, Monday to Friday. |

## 4. Roles

| Role | Owns |
|---|---|
| **Sales Lead** | Lead from enquiry through signed contract and confirmed payment. Hands off at step 10 and steps back. |
| **Ops Associate** | Lead entry, internal setup, access coordination and verification. |
| **Account Lead** | Client relationship from handoff onward. Single point of contact post-sale. Owns kickoff and sign-off. |
| **Tech Lead** | Technical assessment, build-versus-configure decision, delivery oversight. |
| **Delivery Consultant** | Build, configuration, handover, and client walkthrough. |
| **Finance** | Invoicing and payment confirmation. |
| **Founder** | Escalation point of last resort. |

## 5. RACI

**R** Responsible · **A** Accountable · **C** Consulted · **I** Informed

| Stage | Sales Lead | Ops Associate | Account Lead | Tech Lead | Delivery | Finance |
|---|---|---|---|---|---|---|
| Lead intake and qualification | R, A | R | - | - | - | - |
| Proposal and contract | R, A | I | I | C | - | I |
| Invoicing and payment | C | - | I | - | - | R, A |
| Handoff | R, A | I | R | R | I | - |
| Internal setup | I | R, A | I | - | - | - |
| Access provisioning | - | R, A | C | C | - | - |
| Kickoff | - | I | R, A | R | I | - |
| Build decision | - | - | C | R, A | C | - |
| Build and delivery | - | - | I | A | R | - |
| Sign-off and close | - | - | R, A | I | C | R |

---

## 6. Escalation ladder for client-dependent steps

Applies to any step marked **client-dependent** below.

| Elapsed | Action | Owner |
|---|---|---|
| Day 3 | First chase. Email to the client contact, copying the Account Lead. | Ops Associate |
| Day 5 | Escalate. Account Lead calls the client's decision-maker directly. | Account Lead |
| Day 10 | Notify Founder. Engagement flagged as at-risk in the tracker. | Account Lead |

**Engagement clock rule.** The engagement clock **pauses** the moment a client-dependent
step begins and **resumes** when it completes. The escalation ladder runs during the
pause. This means a client who takes six days to provide access moves the quoted
delivery date by six days, and that shift is recorded against the client-dependent step
rather than attributed to delivery.

The pause is not a reason to stop chasing. Pausing the clock protects the timeline;
the ladder protects the relationship. Both run at once.

---

## 7. Procedure

### Stage A - Lead

---

**Step 1 - Receive and assign enquiry**

| | |
|---|---|
| **Owner** | System, then Ops Associate |
| **Trigger** | Enquiry submitted through the intake form, or received by phone |
| **Inputs** | Name, company, email, service selected, problem description |
| **Action** | The intake automation validates the submission, classifies it by service category and urgency, writes a record to the intake sheet, and alerts the on-duty Sales Lead for high-urgency enquiries. Phone enquiries are entered into the form manually by whoever takes the call. |
| **Output** | Intake record created with a named assigned owner |
| **SLA** | Assignment is immediate and automatic |

> **Note on assignment.** Every enquiry has exactly one named owner from the moment it
> arrives. Broadcast alerts to multiple parties are not used, because an alert everyone
> receives is an alert nobody owns.

---

**Step 2 - First contact**

| | |
|---|---|
| **Owner** | Sales Lead |
| **Trigger** | Enquiry assigned |
| **Inputs** | Intake record including AI-generated summary and urgency |
| **Action** | Contact the enquirer by phone or email to acknowledge receipt and schedule a requirements call. |
| **Output** | Contact logged against the lead record with a timestamp |
| **SLA** | **4 business hours** from assignment |

---

**Step 3 - Requirements and costing call**

| | |
|---|---|
| **Owner** | Sales Lead |
| **Trigger** | Requirements call scheduled |
| **Inputs** | Intake record, client's stated problem |
| **Action** | Discuss requirements, current process, systems involved, and indicative cost. Record the systems the client uses, since these determine the access request at step 13. Record any commitment made about scope or timeline, in writing, on the lead record. |
| **Output** | Written requirements note on the lead record, including systems list and any commitments made |
| **SLA** | Note written within **1 business day** of the call |

> **Note on commitments.** Anything said to the client during this call that could be
> read as a promise must be written down here. This is the single most common source of
> scope disputes at delivery, and the written record is the only defence against it.

---

**Step 4 - Set lead status**

| | |
|---|---|
| **Owner** | Sales Lead |
| **Trigger** | Requirements call completed |
| **Inputs** | Requirements note |
| **Action** | Set the lead status to Converted, Ongoing, or Not Converted. Every status change records the date and the person setting it. Status history is retained, not overwritten. |
| **Output** | Lead status updated with timestamped history |
| **SLA** | Same business day as the call |

---

**Step 5 - Follow up ongoing leads**

| | |
|---|---|
| **Owner** | Sales Lead |
| **Trigger** | Lead status is Ongoing |
| **Inputs** | Lead record, date of last contact |
| **Action** | Contact the lead and log the contact date. The tracker flags any Ongoing lead whose last-contact date is more than 2 days old. |
| **Output** | Contact date updated |
| **SLA** | Every **2 business days** until converted or closed |
| **Exit** | After 4 unanswered contacts, set status to Not Converted with reason recorded |

---

### Stage B - Contract and commercials

---

**Step 6 - Prepare and send proposal**

| | |
|---|---|
| **Owner** | Sales Lead |
| **Trigger** | Lead status set to Converted |
| **Inputs** | Requirements note, systems list, indicative costing |
| **Action** | Prepare a proposal stating scope, explicit exclusions, price, payment terms, and indicative timeline. Send to the client. |
| **Output** | Proposal sent, copy filed against the lead record |
| **SLA** | **3 business days** from the requirements call |

---

**Step 7 - Execute NDA and service agreement**

| | |
|---|---|
| **Owner** | Sales Lead (client-dependent) |
| **Trigger** | Client accepts the proposal |
| **Inputs** | Approved proposal, standard NDA and service agreement templates |
| **Action** | Issue both documents for signature. Countersign on return. |
| **Output** | Executed NDA and service agreement filed |
| **Target** | 5 business days. **Client-dependent** - escalation ladder applies |

---

**Step 8 - Raise advance invoice**

| | |
|---|---|
| **Owner** | Finance |
| **Trigger** | Service agreement executed |
| **Inputs** | Executed agreement, agreed price |
| **Action** | Raise an invoice for 50 percent of the engagement value and send to the client's billing contact. |
| **Output** | Advance invoice issued |
| **SLA** | **1 business day** from execution |

---

**Step 9 - Confirm advance payment**

| | |
|---|---|
| **Owner** | Finance (client-dependent) |
| **Trigger** | Advance invoice issued |
| **Inputs** | Invoice, bank records |
| **Action** | Confirm receipt and notify the Sales Lead and Account Lead. |
| **Output** | Payment confirmed on the engagement record |
| **Target** | Per agreed payment terms. **Client-dependent** - escalation ladder applies |

> **Hard gate.** No delivery work begins before advance payment is confirmed. Internal
> setup at step 12 may proceed, but no client-facing commitment of delivery resource is
> made until this step completes.

---

### Stage C - Handoff

---

**Step 10 - Internal handoff**

| | |
|---|---|
| **Owner** | Sales Lead |
| **Trigger** | Advance payment confirmed |
| **Inputs** | Requirements note, systems list, recorded commitments, executed agreement |
| **Action** | Hold a handoff call with the Tech Lead and Account Lead. Before the call, complete the written handoff brief covering: client's stated problem, current process, systems in scope, explicit exclusions, commitments made during sales, known constraints, and client contacts with roles. The call reviews the brief; it does not replace it. |
| **Output** | Written handoff brief filed in the project folder, acknowledged by Tech Lead and Account Lead |
| **SLA** | **2 business days** from payment confirmation |

> **Note.** The brief is the deliverable, not the call. A verbal handoff transfers only
> what the Sales Lead happens to remember, and leaves the delivery team with nothing to
> refer back to when scope is questioned weeks later.

---

**Step 11 - Assign and introduce Account Lead**

| | |
|---|---|
| **Owner** | Account Lead |
| **Trigger** | Handoff brief acknowledged |
| **Inputs** | Handoff brief, client contact list |
| **Action** | Sales Lead introduces the Account Lead to the client by email, stating that the Account Lead is now the single point of contact. Sales Lead steps back from the engagement. |
| **Output** | Introduction email sent; Account Lead recorded as owner on the engagement |
| **SLA** | **1 business day** from handoff |

---

**Step 12 - Internal setup**

| | |
|---|---|
| **Owner** | Ops Associate |
| **Trigger** | Account Lead assigned |
| **Inputs** | Client name, handoff brief, sales correspondence |
| **Action** | Create the project folder on the shared drive using the standard structure, create the internal client channel, and move all sales correspondence into the folder. |
| **Output** | Project folder and channel created and populated |
| **SLA** | **1 business day** from Account Lead assignment |

---

### Stage D - Access

---

**Step 13 - Issue access request**

| | |
|---|---|
| **Owner** | Ops Associate |
| **Trigger** | Internal setup complete |
| **Inputs** | Systems list from the requirements note and handoff brief |
| **Action** | Send the client a single consolidated access request listing every system required, the level of access needed for each, the named person on the client side responsible for granting it, and the date by which it is needed. |
| **Output** | Access request sent; each item logged as an open row in the tracker |
| **SLA** | **1 business day** from setup completion |

> **Note.** One consolidated request, not several. Piecemeal requests restart the
> client's internal approval process each time and are the main reason this stage runs long.

---

**Step 14 - Client provides access**

| | |
|---|---|
| **Owner** | Client, chased by Ops Associate |
| **Trigger** | Access request sent |
| **Inputs** | Access request |
| **Action** | Client grants access or supplies credentials. Ops Associate tracks each item individually and chases outstanding items per the escalation ladder. |
| **Output** | Access granted for each listed system |
| **Target** | 5 business days. **Client-dependent** - escalation ladder applies. **Engagement clock pauses for the duration of this step** |

---

**Step 15 - Verify access**

| | |
|---|---|
| **Owner** | Ops Associate |
| **Trigger** | Client reports access granted |
| **Inputs** | Credentials or access confirmations |
| **Action** | Log in to or otherwise confirm working access to every system on the list. Do not accept the client's assurance in place of verification. Report any failures back to the client immediately as a new open item. |
| **Output** | All access items marked verified in the tracker |
| **SLA** | **1 business day** from client confirmation |

> **Note.** Verification exists because "access has been granted" and "access works"
> are different claims. Discovering the difference during kickoff wastes the call and
> requires a second one.

---

### Stage E - Kickoff

---

**Step 16 - Kickoff call**

| | |
|---|---|
| **Owner** | Account Lead |
| **Trigger** | All access verified |
| **Inputs** | Handoff brief, verified access list |
| **Action** | Hold the kickoff call with the client, Account Lead, and Tech Lead. Cover: introductions and contact routing, scope as understood with client correction invited, explicit exclusions, timeline and what the client owes at each point, communication channel and check-in cadence, and known risks. |
| **Output** | Written scope note and agreed timeline, sent to the client for confirmation |
| **SLA** | Call held within **3 business days** of access verification. Scope note issued within **1 business day** of the call |

> **Note.** The scope note is the output, not the conversation. It is the document
> referred back to when scope is questioned, and it must be confirmed by the client in
> writing.

---

### Stage F - Build

---

**Step 17 - Build-versus-configure decision**

| | |
|---|---|
| **Owner** | Tech Lead |
| **Trigger** | Scope note confirmed by client |
| **Inputs** | Scope note, handoff brief, existing product catalogue |
| **Action** | Assess whether an existing product meets the requirement. Record the decision and the reasoning against the criteria below. |
| **Output** | Decision recorded with written reasoning |
| **SLA** | **2 business days** from scope confirmation |

**Decision criteria.** Configure an existing product where all of the following hold:

1. The existing product covers the core requirement without modification to its logic
2. Any gap can be closed through configuration rather than code
3. The client's systems are already supported by existing connectors
4. Expected configuration effort is under 5 working days

Build new where any of the following hold:

1. The core requirement is not met by any existing product
2. Closing the gap would require changes to an existing product's logic that other clients depend on
3. An unsupported system integration is required
4. Configuration effort would exceed 5 working days, at which point a build is cheaper to maintain

**Where criteria conflict,** the Tech Lead decides and records why. The decision is
reviewed at the 30-day review at step 23, and the record is what makes that review possible.

---

**Step 18 - Path A: configure existing product**

| | |
|---|---|
| **Owner** | Delivery Consultant |
| **Trigger** | Decision recorded as configure |
| **Inputs** | Scope note, verified access, existing product |
| **Action** | Configure and deploy the product to the client environment. |
| **Output** | Working solution in the client environment |
| **SLA** | Per timeline agreed at kickoff |

---

**Step 19 - Path B: new build**

| | |
|---|---|
| **Owner** | Tech Lead and Delivery Consultant |
| **Trigger** | Decision recorded as build |
| **Inputs** | Scope note, verified access |
| **Action** | Two-week build cycle. Hold a mid-point check-in with the client at the end of week one to confirm direction before the build is complete. |
| **Output** | Working solution in the client environment; mid-point check-in recorded |
| **SLA** | 10 business days from decision, subject to engagement clock pauses |

---

### Stage G - Delivery and close

---

**Step 20 - Handover and walkthrough**

| | |
|---|---|
| **Owner** | Delivery Consultant |
| **Trigger** | Solution complete |
| **Inputs** | Working solution, scope note |
| **Action** | Hand over the solution and run a walkthrough session with the client's team covering operation, common failure modes, and who to contact for support. Provide written documentation. |
| **Output** | Walkthrough completed; documentation delivered |
| **SLA** | Within **3 business days** of build completion |

---

**Step 21 - Obtain sign-off**

| | |
|---|---|
| **Owner** | Account Lead (client-dependent) |
| **Trigger** | Walkthrough completed |
| **Inputs** | Scope note, delivered solution |
| **Action** | Request written confirmation from the client that the delivery meets the agreed scope. Any items the client raises are assessed against the scope note and either resolved as defects or handled as change requests per section 8. |
| **Output** | Written sign-off recorded |
| **Target** | 5 business days. **Client-dependent** - escalation ladder applies |

---

**Step 22 - Final invoice**

| | |
|---|---|
| **Owner** | Finance |
| **Trigger** | Sign-off received |
| **Inputs** | Sign-off record, agreed price |
| **Action** | Raise the balancing invoice and track to payment. |
| **Output** | Final invoice issued |
| **SLA** | **1 business day** from sign-off |

---

**Step 23 - Move to support and schedule review**

| | |
|---|---|
| **Owner** | Account Lead |
| **Trigger** | Final invoice issued |
| **Inputs** | Engagement record |
| **Action** | Move the account to ongoing support, confirm the support contact and route to the client, and schedule a review 30 days out. The review covers whether the solution is in use, whether the build-versus-configure decision proved correct, and where the engagement lost time. |
| **Output** | Account marked as in support; review scheduled |
| **SLA** | **2 business days** from final invoice |

---

## 8. Exception paths

### E1 - Client unresponsive

**Applies to:** steps 7, 9, 14, 21.

Follow the escalation ladder in section 6. The engagement clock pauses from the moment
the step begins.

If there is no response by **day 15**, the Account Lead issues a written notice that the
engagement is being placed on hold, stating what is outstanding and what is needed to
resume. The engagement moves to On Hold in the tracker. Resumption requires a new
timeline, quoted from the resumption date.

Work already delivered remains invoiced per the agreement. Advance payments are not refunded
for delays caused by client non-response.

---

### E2 - Access provisioning fails

**Applies to:** steps 14 and 15.

Where verification at step 15 fails, or the client cannot grant access to a system:

1. Ops Associate logs the specific failure and returns it to the client as a new open item, with the ladder restarting for that item only. Verified items remain verified.
2. Where the client cannot grant access at all - a system they do not control, or a security policy that forbids third-party access - the Tech Lead assesses within 2 business days whether the scope can be delivered without it.
3. If scope can be delivered without it, the scope note is amended and re-confirmed by the client.
4. If it cannot, this becomes a scope change under E3.

**Partial access does not block kickoff** where the missing systems are not needed for
the first phase of work. The Tech Lead makes this call and records it.

---

### E3 - Scope change mid-engagement

**Applies to:** any point after step 16.

1. Any request outside the confirmed scope note is logged as a change request by whoever receives it. No change request is actioned informally, including small ones.
2. Tech Lead assesses effort and timeline impact within **2 business days**.
3. Account Lead returns to the client with cost and revised timeline.
4. Work on the change begins only on written client approval. Existing scope continues in parallel.
5. Where the change is material, Finance issues a revised invoice before work begins.

**Where the client asserts something was promised during sales,** the Account Lead checks
the commitments section of the handoff brief. If it is recorded there, it is in scope and
delivered without charge. If it is not, it is treated as a change request. This is why
step 3 requires commitments to be written down.

---

### E4 - Payment not received

**Applies to:** steps 9 and 22.

**Advance (step 9).** No delivery resource is committed. Ops Associate does not issue
the access request. Escalation ladder applies. At day 15, the engagement is placed on
hold and the delivery slot released.

**Final (step 22).** Delivery is complete and the client is in use of the solution.
Finance chases at 7, 14, and 21 days. At 30 days the Founder is notified and the account
is flagged before any further work is accepted.

---

### E5 - Kickoff repeatedly rescheduled

**Applies to:** step 16.

The engagement clock does not start until kickoff is held. After **two client-initiated
reschedules**, the Account Lead contacts the client's decision-maker directly to
establish whether the engagement remains a priority, and records the outcome.

After a third reschedule, the delivery slot is released and the engagement moves to
On Hold. Resumption is subject to delivery availability.

---

## 9. Records

| Record | Held in | Retained |
|---|---|---|
| Lead record with status history | Tracker | Indefinitely |
| Requirements note and commitments | Project folder | Life of client relationship |
| Handoff brief | Project folder | Life of client relationship |
| Access request and verification log | Tracker | Life of engagement plus 1 year |
| Scope note and client confirmation | Project folder | Life of client relationship |
| Build-versus-configure decision and reasoning | Project folder | Indefinitely, for review at step 23 |
| Change requests and approvals | Project folder | Life of client relationship |
| Sign-off | Project folder | Indefinitely |

---

## 10. Revision history

| Version | Date | Change | Author |
|---|---|---|---|
| 1.0 | Aug 2026 | Initial procedure | Operations |
