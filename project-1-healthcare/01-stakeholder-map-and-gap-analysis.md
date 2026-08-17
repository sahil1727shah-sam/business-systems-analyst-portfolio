# Healthcare Appointment Management System — Discovery Phase

**Author:** SAHIL SHAH

**Role:** Business Systems Analyst (Project 1)



**Discovery Phase — Stakeholder Map \& As-Is Process Note**



**1. Purpose**

This document captures the findings from an initial interview with the Hospital Operations Manager regarding the current ("as-is") patient appointment booking process. It identifies stakeholders, maps the existing workflow, and surfaces early gaps that will feed into the Gap Analysis and BRD in later weeks.



**2. Elicitation Method**

**Technique used:** 1:1 stakeholder interview.

**Stakeholders interviewed:**

1. Hospital Operations Manager (process owner) — high-level process walkthrough
2. Front-desk Receptionist (frontline user) — validation against actual day-to-day workflow
3. Compliance Officer (risk owner) — access control and regulatory exposure



**3. Stakeholder Map (Power/Interest Grid)**

|**Stakeholder**|**Power**|**Interest**|**Quadrant**|**Why they matter**|
|-|-|-|-|-|
|Hospital Operations Manager|High|High|**Manage closely**|Process owner, project sponsor, primary decision-maker|
|Chief Medical Officer|High|High|**Manage closely**|Owns clinical impact of scheduling changes|
|Hospital IT Director|High|Low|Keep satisfied|Owns MediSlot infrastructure and any integration work|
|Compliance Officer|High|Low|Keep satisfied|Interviewed (see §7) — confirmed no documented access policy exists; ownership of access control currently unclear|
|Front-desk receptionists (3)|Low|High|Keep informed|Primary day-to-day users, most affected by any process change|
|Billing team (2)|Low|High|Keep informed|Directly impacted by duplicate-profile cleanup workload|
|Nursing supervisors|Low|High|Keep informed|Consumers of the daily schedule, read-only access|
|General patients|Low|Low|Monitor|End users of any future booking channel, but not decision-makers|
|MediSlot vendor support|Low|Low|Monitor|External technical dependency, engaged only when issues arise|



**RACI for a scheduling process change (example, to refine per requirement):**



|**Activity**|**Ops Manager**|**IT Director**|**Receptionists**|**Billing**|**Compliance**|
|-|-|-|-|-|-|
|Approve new requirements|A|C|I|I|C|
|Define booking rules|R|C|C|I|I|
|Test new duplicate-detection logic|I|A|R|C|I|
|Sign off on access-control changes|C|R|I|I|A|

*(R = Responsible, A = Accountable, C = Consulted, I = Informed)*



**4. As-Is Process — Appointment Booking (Narrative)**

1. Patient initiates contact — primarily by phone (\~70% of bookings), with some walk-ins and email bookings from existing patients with a case manager.
2. Receptionist opens MediSlot and manually checks doctor availability.
3. Receptionist searches for the patient by phone number. **MediSlot only supports exact-match search** — no fuzzy matching on name or partial number.
4. **Branch A (no match found):** Receptionist creates a new patient profile. If the patient is already in the system (different number, typo, or simply not recognized), this creates a **duplicate profile**.
5. **Branch B (match found):** Receptionist proceeds with the existing profile.
6. Slot is booked directly in MediSlot's live calendar. In theory, booking one slot locks it instantly — in practice, **double-bookings occur \~3–4 times/month**, likely due to a calendar refresh delay when two receptionists book simultaneously.
7. A manual reminder call is placed the day before the appointment, made by whichever receptionist has downtime. **No SMS/text reminder exists today**, despite phone numbers already being captured at booking.



**5. Early Findings (Gap Analysis)**

|**#**|**Finding**|**Root cause (initial hypothesis)**|**Impact**|
|-|-|-|-|
|1|Duplicate patient profiles|Exact-match-only search; no enforced de-duplicate rule|Billing rework (1 day–2 weeks per case); insurance claim errors|
|2|Double-bookings|Likely a calendar refresh/concurrency issue in MediSlot|Patient experience, staff time to resolve on the spot|
|3|Inconsistent reminders|No automated reminder system; manual, ad hoc process|Likely contributes to no-show rate (not yet quantified)|
|4|Overly broad data access|No role-based access control; all "full access" users can see clinical notes, not just scheduling data|Compliance risk — flagged directly by the Ops Manager, unprompted|



**6. Assumptions \& Open Questions**

* **Assumption:** The "3–4 times/month" double-booking frequency is the Ops Manager's estimate, not a system log — will need to validate against actual MediSlot audit logs if available.
* **Open question:** What is the current no-show rate, and is there any data connecting it to the inconsistent reminder process?
* **Open question:** Has Compliance ever formally reviewed MediSlot's access controls? Need to schedule that interview next.
* **Open question:** What is billing's actual time cost (hours/week) spent resolving duplicate profiles? Needed to build a business case in the BRD.



**7. Validation Interviews — Receptionist \& Compliance Officer**

**7.1 Front-desk Receptionist (Maria)**

Interviewing frontline staff surfaced a **discrepancy** from the manager's account: the manager described the process as "search by phone number," but the receptionist described a real-world workaround under time pressure.

* When the phone-number search returns no match, staff don't always trust it — patients calling from a different number or with a typo are missed. Under time pressure, receptionists sometimes skip the name-search fallback entirely and create a new profile, knowingly risking a duplicate, because "**billing sorts it out later**."
* **The system gives no warning when a slot is double-booked.** Staff only discover it when the calendar looks fine at booking time but a conflict surface later (a patient walks in, or a manager's morning review catches two names on one slot).
* In-the-moment fixes (rescheduling a bumped patient) happen fast, within the hour — but the underlying duplicate-profile cleanup still routes to billing with the same delay described earlier.

**Reframed root cause:** Finding #1 (duplicate profiles) is not purely a *technology* gap — it's also a **process/training gap**. There is no defined escalation rule for what staff should do when a search comes back empty, so behavior varies by how busy the desk is.



**7.2 Compliance Officer (Priya Nair)**

This interview shifted from workflow to risk, and surfaced three findings the Ops Manager could not have provided:

* **No documented access policy exists.** Access levels were set up once and never formally reviewed; even "read-only" for nurses hasn't been precisely scoped (unclear if it excludes clinical notes).
* **No clear ownership of access control.** Provisioning currently sits informally with the Ops Manager as system admin, but policy ownership should sit with Compliance, implemented by IT — that split doesn't exist today.
* **Regulatory compliance is unverified, not confirmed.** No signed Business Associate Agreement or audit report has been reviewed to confirm MediSlot meets patient-data handling requirements (encryption, access logging, etc.). The Compliance Officer explicitly could not confirm an audit trail exists for who accessed or changed a record.



**8. Gap Analysis**

|**#**|**As-Is**|**To-Be**|**The Gap**|**Priority**|
|-|-|-|-|-|
|1|Exact-match-only phone search; duplicates created when a patient calls from a different number or there's a typo|System flags likely duplicates using fuzzy matching (name + partial phone + DOB) before creating a new profile|No fuzzy-match/dedup logic exists|**High** — direct billing cost + insurance claim errors|
|2|Two receptionists can book the same slot simultaneously due to a calendar refresh delay|Real-time slot locking the instant a booking is initiated (not just on save)|Concurrency handling in the booking flow|**High** — direct patient-facing failure|
|3|Manual, inconsistent reminder calls; some patients get none|Automated SMS + optional call reminder sent 24–48h before appointment|No automated reminder system, despite phone data already being captured|**Medium** — likely reduces no-shows, but not yet quantified|
|4|All "full access" users (receptionists, billing) can view clinical notes, not just scheduling data|Role-based access control (RBAC): receptionists/billing see scheduling data only; nurses stay read-only|No RBAC implemented in MediSlot|**High** — compliance/security risk, unprompted stakeholder concern|
|5|No defined rule for what staff should do when a search returns no match; behavior varies by workload|A clear escalation rule (e.g. mandatory name+DOB fallback search before creating any new profile)|Process/training gap, not just a technology gap|**High** — root cause behind Finding #1, confirmed via receptionist interview|
|6|No confirmed audit trail; regulatory compliance assumed but not verified with the vendor|Signed Business Associate Agreement and independent audit confirming encryption, access logging, and compliance|Unverified vendor compliance documentation|**High** — legal/regulatory exposure, confirmed via Compliance Officer interview|



**Prioritization rationale:** patient-facing failures and compliance/legal exposure (#1, #2, #4, #5, #6) outrank pure efficiency gains (#3), even though #3 is the easiest win to describe to non-technical stakeholders. Findings #5 and #6 emerged only after validating the manager's account against frontline staff and Compliance — a reminder that a single stakeholder's account is never the full picture. This ordering will be defended again at the BRD stage.



**9. SWOT (scoped to this project)**

* **Strengths:** Phone numbers already captured at booking, giving reminder automation a data foundation with no new collection needed; the Ops Manager is engaged and forthcoming, suggesting low organizational resistance to change so far.
* **Weaknesses:** No role-based access control exists in the current system; core processes (de-duplicate checking, reminders) rely on staff memory and habit rather than system-enforced rules.
* **Opportunities:** Patients are already requesting SMS reminders, meaning built-in demand for one of the fixes; solving the dedup problem also resolves a standing billing pain point — a single change with two stakeholder wins.
* **Threats:** Any process change requires retraining 3 receptionists and 2 billing staff, creating adoption risk; the Compliance Officer has not yet been consulted and may surface requirements that reshape scope once involved.



**10. Next Steps**

1. Request MediSlot access logs / no-show data if available, to replace assumptions with real numbers.
2. Request confirmation (or the missing documentation) from the MediSlot vendor: signed Business Associate Agreement, audit log capability, encryption details.
3. Draft the escalation rule referenced in Gap #5 for review with the Ops Manager and receptionist team.
4. Use this Gap Analysis and SWOT as direct inputs to the BRD (Module 8), where each gap becomes a business requirement.

