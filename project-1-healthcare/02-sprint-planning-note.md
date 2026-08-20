# Healthcare Appointment Management System
## Sprint Planning Note — Module 2 (Agile/Scrum)
**Author: Sahil Shah 
**Role: Business Systems Analyst (Project 1) 
**Date: [08/20/2026]

---

## 1. Purpose

This note documents how the 6 findings from the Week 1 Gap Analysis were translated into a Jira backlog, prioritized, and pulled into the project's first sprint. It connects the discovery work (stakeholder interviews, gap analysis) directly to execution (epics, stories, sprint planning) — showing the full BA workflow from requirement to backlog item.

---

## 2. From Gap Analysis to Epics

Each of the 6 Gap Analysis findings became one Jira epic. This 1:1 mapping kept traceability clean — anyone reviewing the board can trace a story straight back to the original stakeholder finding that justified it.

| Gap Analysis Finding | Jira Epic | Priority |
|---|---|---|
| #1 — Duplicate patient profiles | Fix duplicate patient profiles | High |
| #2 — Double-bookings | Prevent double-bookings | High |
| #3 — Inconsistent reminders | Add automated reminders | Medium |
| #4 — Overly broad data access | Implement role-based access control | High |
| #5 — No search escalation rule | Define search escalation rule | High |
| #6 — Unverified vendor compliance | Verify vendor compliance documentation | High |

---

## 3. User Stories & Acceptance Criteria

Each epic was broken into at least one user story in "As a [role], I want [goal], so that [benefit]" format, with acceptance criteria written in Given/When/Then form so "done" is unambiguous.

| Story | Acceptance Criteria (Given/When/Then) |
|---|---|

1. As a receptionist, I want fuzzy-match duplicate detection, so that billing doesn't spend days merging records 
* Given a receptionist searches by phone number, When no exact match is found, Then the system also checks name + partial number before allowing a new profile to be created

2. As a receptionist, I want real-time slot locking, so that two people can't book the same appointment 
* Given two receptionists attempt to book the same slot at the same time, When the first booking is confirmed, Then the slot is locked instantly and the second receptionist sees it as unavailable before submitting 

3. As a patient, I want an SMS reminder 24-48h before my visit, so that I don't forget my appointment 
* Given a patient has an upcoming appointment, When it is 24-48 hours away, Then an automated SMS reminder is sent to the phone number on file 

4. As a compliance officer, I want receptionists restricted to scheduling data only, so that clinical notes stay protected 
* Given a receptionist or billing staff member logs in, When they access a patient record, Then they can view and edit only scheduling data, not clinical notes 

5. As a receptionist, I want a clear fallback process when phone search fails, so that I'm not guessing under time pressure 
* Given a receptionist's phone-number search returns no match, When they are unsure if the patient is new or existing, Then they must complete a name + date-of-birth fallback search before creating a new profile 

6. As a compliance officer, I want a signed BAA and audit-log confirmation from the vendor, so that regulatory exposure is closed 
*  Given the project moves toward implementation, When vendor documentation is requested, Then a signed Business Associate Agreement and confirmation of audit-log capability must be received before go-live 

---

## 4. Sprint 1 Planning Decision

**Included in Sprint 1:** all 5 **High**-priority stories (duplicate detection, double-booking prevention, RBAC, search escalation rule, vendor compliance verification).

**Deliberately excluded from Sprint 1:** the SMS reminder story (Medium priority).

**Why:** this mirrors the prioritization rationale from the Gap Analysis — patient-facing failures and compliance/legal exposure outrank pure efficiency gains. Duplicate profiles and double-bookings directly harm the patient experience today; the RBAC and vendor-compliance items carry legal/regulatory risk that was flagged unprompted by the Compliance Officer. The SMS reminder, while valuable, is a lower-risk improvement that can safely wait for Sprint 2 without compounding existing harm.

---

## 5. Reflection

Running this as an actual Jira board — not just a written plan — made one thing clearer than the theory alone did: **prioritization is a decision you have to defend, not just a ranking exercise.** Leaving the SMS reminder out of Sprint 1 is the kind of call a Product Owner or stakeholder could easily push back on ("why isn't the patient-facing improvement first?"), and having the Gap Analysis reasoning already written down meant I had a ready, specific answer instead of an improvised one.

---

## 6. Artifacts

- Jira Backlog: 6 epics, 6 stories, all linked and with acceptance criteria
- Jira Sprint Board: Sprint 1 active with 5 stories (see `jira-sprint-board.png`)
