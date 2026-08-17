# Module 1 — Business Analysis Foundations
*Personal learning notes — written in my own words as I work through this module.*

---

## SDLC (Software Development Life Cycle)

**What it is (in my own words): The structured stages a system goes through, from idea to retirement.

Standard 7 phases: 
Planning → Analysis → Design → Development → Testing → Deployment → Maintenance

Requirement Gathering / Planning – Understand what the business needs
Analysis – Break down requirements, feasibility study, cost-benefit
Design – System architecture, database design, UI/UX design (HLD & LLD)
Development / Implementation – Developers write the actual code
Testing – QA validates the software against requirements
Deployment – Release to production/live environment
Maintenance – Bug fixes, updates, enhancements post-launch


**The models I need to know:**
| Model | When it's used | How I'd explain it in an interview |

1. Waterfall
* When it's used: Fixed-scope, regulated projects where requirements are well understood upfront (banking, government, compliance-heavy systems)
* How I'd explain it in an interview: "Waterfall is sequential — each phase finishes before the next starts, so I'd gather all requirements completely before design even begins. I'd use it when the client needs certainty on scope and cost upfront, like a regulated banking system, but it's risky if requirements are likely to change mid-project."

2. Agile (SCRUM, KANBAN)
* Most modern software/SaaS products, evolving requirements, need for fast feedback
* "Agile breaks work into short sprints so we can adapt as we learn. As a BA, instead of writing one giant BRD upfront, I'd continuously refine the backlog — writing and re-prioritizing user stories sprint by sprint based on stakeholder feedback."

3. Iterative
* Complex systems built up in repeated cycles, each adding more functionality
* "Iterative is like Agile's parent model — you build in repeated passes, each one adding functionality and refining what came before. I'd re-analyze requirements at the start of each iteration rather than assuming the first pass got everything right."

4. V-Model 
* Safety-critical or highly regulated systems (medical devices, aviation, sometimes healthcare/banking)
* "V-Model pairs every development phase with a matching testing phase, planned in parallel — not bolted on at the end. As a BA, I'd write test cases at the same time as requirements, not after, since verification is built into the model from the start."
 
5. Spiral
* Large, high-risk, expensive projects where risk needs constant reassessment
* "Spiral combines Waterfall and Iterative with a heavy risk-analysis step in every loop. I'd use it on large, high-cost projects where getting something wrong is expensive — each cycle we'd reassess risk before committing further."


NOTE: 
"Iterative is the umbrella principle — build in cycles and refine. 
 Agile is a specific, disciplined implementation of that principle, with time-boxed sprints, continuous stakeholder collaboration, and a shippable increment at the end of every cycle."
---

## BA Lifecycle

**The 5 stages, in order:**
1. Enterprise Analysis — understand the business problem before jumping to a solution
2. Requirements Planning — decide who to talk to, which technique, and timeline
3. Elicitation — gather requirements (interviews, workshops, surveys, observation, document review)
4. Analysis & Documentation — turn raw input into BRD/FRD/user stories
5. Solution Assessment & Validation — confirm the delivered solution actually solves the original problem

---

## Requirement Gathering Techniques

| Technique | Best used when | Weakness |
|---|---|---|

| Interviews |	Deep, individual insight; good for sensitive topics | Time-consuming to scale across many stakeholders |
| Workshops/JAD | Resolves conflicting needs fast, multiple views at once | Can be dominated by louder voices in the room |
| Surveys/Questionnaires | Scales to many people cheaply | Low depth, no follow-up possible|
| Observation ("job shadowing") | Reveals things people forget to mention or don't realize they do | Time-intensive, people may behave differently when watched |
| Document Analysis | Fast way to understand existing process/systems | Documents may be outdated or not reflect real practice |
| Prototyping | Surfaces requirements people can't articulate cold, gets concrete reactions| Requires a draft/mockup to already exist|

Brainstorming, Focus Group, Reverse Engineering


## Stakeholder Analysis

**RACI — what each letter means, in my own words:**
- R: RESPONSIBLE
- A: ACCOUNTABLE
- C: CONSULTED
- I: INFORMED

Only one person/role should ever be Accountable per task — that's the single point of sign-off.

Power/Interest Grid — plots stakeholders on two axes:
1. Manage Closely (high power, high interest) — most engagement, sign-off matters most
2. Keep Satisfied (high power, low interest) — update periodically, don't overwhelm with detail
3. Keep Informed (low power, high interest) — most affected day-to-day, needs regular updates
4. Monitor (low power, low interest) — minimal effort, light-touch communication

**Power/Interest grid — why do "Manage Closely" stakeholders matter more than "Monitor" ones?**
Manage Closely Stakeholders are more important because they have high power & high interest in the project. They can make important decision which is strongly affect the project's success. So, I communicate with them regularly, involve them in key decisions, and manage their expectation.
Monitor stakeholders have low power & low interest. So, we don't need to spend as much as time with them. We just keep an eye on them and provide information when needed.

---

## BRD vs FRD vs SRS

**The difference, explained simply (as if to a non-BA friend):**


**One-line example of each, from my own project:**
- BRD: Why are we doing this? = Business stakeholders/sponsors
- FRD: What should system do? = Delivery/developers team
- SRS: How should it behave, technically? = Developers/QA

BRD: KEY SECTION 
1. Executive Summary/Project Overview
2. Business objective/goal
3. Project Scope (in scope - out scope)
4. Stakeholder list
5. Business Requirement (BR-001, BR-002,....)
6. Assumption & Constrains
7. Risks
8. Success criteria/KPIs
9. Approval/Sign-off

In practice, many companies merge FRD and SRS into one document — know the theoretical distinction.

FRD: KEY SECTION 
1. Intro/Purpose
2. Functional Requirement (FR-001, FR-002,....)
3. Use Case/User Stories
4. Business Rule
5. Data Requirement
6. Non-Functional Requirement (Performance, Security, Usability, Reliability/Availability, Scalability)
7. UI Mockups/Wireframes
8. Assumption, dependencies


SRS: KEY SECTION (IEEE 830 STANDARD)
1. Intro/Purpose/Scope/definition
2. Overall Description
3. Functional Requirement (FR-001, FR-002,....)
4. Non-Functional Requirement (Performance, Security, Usability, Reliability/Availability, Scalability)
5. External Interface Requirements (APIs, hardware, OS)
6. Appendices

---

## Gap Analysis, SWOT, Root Cause Analysis

**Gap Analysis — the 4 columns I always fill in:** Compare As-Is (current state) vs To-Be (desired state); the difference is the gap the project must close.
1. As-Is
2. To-Be
3. The Gap (specific deficiency)
4. Priority/Impact

**SWOT — what makes a good SWOT specific to a project rather than generic:**
“A good project-specific SWOT focuses only on factors that can directly affect that particular project. It should not contain general statements.”

1. Strength: Experienced project team
2. Weakness: Limited project budget
3. Opportunity: New technology can reduce project time
4. Threat: Competitor may launch a similar product first

**Root Cause Analysis — "5 Whys" example from my own interview findings:**
A problem-solving method to find the underlying cause of an issue, rather than just fixing the symptom.
Critical because a BA who fixes symptoms without finding the root cause leads projects to fail repeatedly on the same issue.

A) 5 Whys:

Problem: Customers are cancelling subscriptions.

Why? → They say the app is too slow.
Why is it slow? → The database queries take too long.
Why do queries take long? → No indexing on the main search table.
Why no indexing? → It was never added during initial development.
Why wasn't it added? → No performance requirement was specified in the original SRS.

Root cause: Missing non-functional (performance) requirement during requirement gathering — not "slow app" as originally assumed.

B) Fishbone Diagram (Ishikawa/Cause-and-Effect Diagram) – Visually organizes potential causes into categories: People, Process, Technology, Environment, Materials, Management. Useful when a problem has multiple contributing factors, not just one linear chain.

	People        Process
           \             /
            \           /
             >-------- PROBLEM
            /           \
           /             \
      Technology      Environment


Q: "5 Whys vs Fishbone — when would you use which?" 
→ 5 Whys for a single linear problem chain; Fishbone when multiple unrelated factors could be contributing and you need to brainstorm broadly first.
---

## Business Process Mapping
Definition: Visual documentation of how a process actually works, step by step — usually with swimlanes showing which role performs each step.

Why it matters to a BA: a flowchart reveals things a narrative description hides — bottlenecks, handoff points where errors creep in, and steps that don't need to exist at all.

**What a swimlane diagram shows that a simple flowchart doesn't:**
Swimlane Diagrams – Shows which department/role owns each step — critical for spotting handoff delays and unclear ownership

[Employee: Submit leave request] 
        → [Manager: Review request] 
              → <Approved?> 
                   -- Yes → [HR: Update leave balance] → [System: Notify employee] → (End)
                   -- No  → [System: Notify employee of rejection] → (End)

Swimlanes here would be: Employee | Manager | HR | System — each step placed under the role responsible.


---

