# Context: wrkflow.ai Client Onboarding

**Document:** 00 of 05 - Context
**Version:** 1.0
**Last updated:** August 2026

---

## About this case study

This is a constructed case study, not a client engagement. The firm described below is
fictional, modelled on a small consulting practice. The process, pain points, and
recommendations are my own analysis. The automation described in `02-make-automation/`
is real and runnable.

The purpose is to work through a full process improvement cycle end to end: map the
current state, identify where it breaks, document how it should run, build one of the
fixes, and show the resulting future state.

---

## The firm

**wrkflow.ai** is a consulting firm that helps clients automate and implement business
workflows.

| | |
|---|---|
| **Headcount** | 25 |
| **New clients** | ~8 per month |
| **Location** | Hyderabad |
| **Engagement length** | 2 to 6 weeks from signature to delivery |

### Services offered

1. **Workflow Automation** - automating manual, repetitive processes such as approvals, data entry, and handoffs
2. **AI Integration** - embedding LLM tools into existing workflows for document processing, drafting, summarization, and classification
3. **System Integration** - connecting existing tools so data flows between them
4. **Custom Internal Tools** - dashboards, trackers, and small internal applications
5. **Training and Enablement** - teaching the client team to run and maintain what was built

Enquiries that do not fit these categories, or where the client is not yet sure what
they need, are handled as **Other**. These make up a meaningful share of inbound
volume and carry the least structured information.

---

## Roles

| Role | Responsibility |
|---|---|
| **Sales Lead** | Owns the lead from enquiry to signed contract. Steps back after handoff. |
| **Ops Associate** | Onboarding legwork - lead entry, internal setup, access coordination. |
| **Account Lead** | Owns the client relationship from handoff onward. Single point of contact post-sale. |
| **Tech Lead** | Technical assessment, build-versus-configure decision, delivery oversight. |
| **Delivery Consultant** | Builds, configures, and hands over the solution. |
| **Finance** | Invoicing and payment tracking. |
| **Client** | Provides requirements, access, decisions, and sign-off. |

---

## Current tooling

| Stage | Tool in use |
|---|---|
| Enquiry intake | Shared contact email and phone number |
| Alerting | Email alert fires to sales leads, ops team, and managers simultaneously |
| Lead tracking | A shared Google Sheet - the "leads sheet" |
| Everything after conversion | Email chains |
| Project files | Shared drive, created ad hoc per client |

---

## Why this project exists

The firm has a lead pipeline. It does not have an onboarding process.

The leads sheet covers everything up to the moment a client says yes. It records who
enquired, what they wanted, and whether they converted. Past that point the sheet stops
and nothing replaces it. Contract, payment, handoff, access provisioning, kickoff, build
decision, delivery, and sign-off are all coordinated over email chains, with no shared
view of where any client stands.

This is a common pattern in firms of this size. Sales tooling matures first because
sales volume is visible and revenue depends on it. Post-sale onboarding stays informal
because it is handled by fewer people who assume they can hold it in their heads. At
8 new clients a month with 2 to 6 week engagements, roughly 10 to 15 clients are in
flight at any time, which is past the point where that assumption holds.

The consequences are not dramatic failures. They are slippage: delays nobody owns,
context lost between sales and delivery, access requests that sit unanswered for a week,
and no way to answer "where is this client and what is blocking them" without reading
an email thread.

---

## Scope of this case study

**In scope:** the full path from enquiry received to delivery signed off and the account
moved to ongoing support - 22 steps across 7 roles.

**Out of scope:** the ongoing support relationship after the 30-day review, internal
hiring and resourcing, and the technical delivery methodology itself.

---

## Documents in this pack

| File | Contents |
|---|---|
| `00-context.md` | This document |
| `01-current-state.md` | Current process map and pain point analysis |
| `02-sop-client-onboarding.md` | Written standard operating procedure |
| `03-tracker.md` | Tracker design and screenshots |
| `04-improvement-memo.md` | Recommended changes with reasoning |
| `05-future-state.md` | Revised process map |
| `make-automation/` | Working intake triage automation |
