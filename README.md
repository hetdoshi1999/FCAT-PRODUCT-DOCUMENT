# FCAT-PRODUCT-DOCUMENT

---

---

## Executive Summary

FIITJEE's FCAT module was doing exactly what it was built to do: collecting student scores, logging performance data, and generating reports after every test cycle. On paper, it worked.

The problem was what happened after the data was collected. Nothing.

Students scoring critically low on specific concepts weren't being flagged. Faculty weren't receiving any automated signal. The student would fail a concept, move into the next test cycle, and carry that gap forward — unaddressed, unresolved, compounding.

The FCAT had become a scoreboard. It had no mechanism to act on what it was measuring.

Most people in the org saw this as a data visibility issue — a dashboard problem. I reframed it as a **loop problem**: the signal existed, but the delivery mechanism was broken. The fix wasn't a better report. It was a closed-loop intervention system that automatically turned low scores into targeted action.

I designed that system end-to-end — from trigger thresholds and notification routing to session assignment, re-assessment cadence, and score write-back — and worked cross-functionally to ship it.

**Outcome: FCAT transformed from a passive reporting layer into a diagnostic and intervention infrastructure.**

---

## Background & Business Context

FIITJEE is one of India's largest and most competitive engineering entrance preparation institutes, known primarily for IIT-JEE coaching. The academic pressure in this environment is high, the curriculum is dense, and the gap between a student who gets early intervention and one who doesn't can be the difference between clearing the exam and missing it.

The FCAT — Formative Cumulative Assessment Tool — was built into FIITJEE's student portal to track performance across three core subjects: Physics, Chemistry, and Mathematics. After every test cycle, scores were broken down by concept and topic, giving the institute a granular view of where each student stood.

The intent was sound: capture performance data at a concept level so that weak areas could be identified early.

The execution had a critical missing piece: **no one had designed what should happen after the data was captured.**

The portal tracked. The portal reported. The portal did not act.

In a high-stakes academic environment where concept gaps compound quickly across weekly test cycles, a tool that observes but never intervenes is not just passive — it's a missed obligation.

---

## Problem Discovery

### What the Data Was Hiding

The problem wasn't obvious from the outside. The FCAT was populated, reports were being generated, and the product team considered it functional. But a closer look at how the data was actually being consumed revealed a system that was producing output nobody was acting on.

**1. Faculty weren't using the FCAT data**
Conversations with subject teachers revealed that they were relying on classroom observation and their own intuition to identify struggling students. The performance breakdown view in the portal existed, but faculty rarely visited it. The tool required manual check-ins — and those check-ins weren't happening.

**2. No automated signal existed**
The portal had no alert mechanism. If a student scored 32% on Electrostatics, that number sat inside a table. Nothing surfaced it. Nobody was notified. The system expected humans to go looking for problems rather than bringing problems to humans.

**3. Students were repeating the same failures across cycles**
Looking at performance patterns across multiple test cycles, a clear and troubling pattern emerged: the same students were underperforming on the same concepts, test after test. This wasn't a one-time miss — it was a recurring gap that nobody was catching because no intervention was triggering between cycles.

**4. The loop was broken, not the data**
This was the sharpest insight. The data was fine. The FCAT was capturing accurate, concept-level performance information. The failure was in what happened next — or more precisely, what didn't happen next.

> Low concept score → silence → next test → same gap → compounding failure
> 

That was the actual user journey. Not because of negligence, but because the system wasn't designed to close the loop.

---

## Root Cause Reframing

> *"We need to improve the dashboard so faculty can see the data more clearly."*
— The initial framing inside the team
> 

That framing wasn't wrong. But it was pointing at a symptom, not the root cause.

Better dashboards still require humans to check them. And in a high-volume academic environment where faculty are managing dozens of students across multiple subjects, manual check-ins are unreliable at scale.

I reframed the problem this way:

**The root cause isn't that the data is hard to find. It's that the data has no delivery mechanism — and no pathway to action.**

| Default Framing | Reframed Diagnosis |
| --- | --- |
| Faculty can't easily see weak students | The system doesn't push alerts — it expects pulls |
| Dashboard needs improvement | The loop between data and action is missing entirely |
| Students aren't recovering from concept gaps | No intervention is triggered before the next test cycle |
| Re-assessment is rare | Re-assessment has no structural place in the workflow |
| Low scores are reported | Low scores are not acted on |

The shift: from "make the data more visible" to "make the data automatically trigger the right response." That's a fundamentally different product problem — and a fundamentally different solution.

---

## Product Thinking Framework

### Users, Goals & Constraints

| Dimension | Detail |
| --- | --- |
| **Primary User 1** | Students — need to recover from concept gaps before the next test cycle |
| **Primary User 2** | Faculty — need to know which students require intervention, and on which concepts |
| **Secondary User** | Academic Coordinators — need visibility into intervention status and recovery outcomes |
| **User Goal** | Identify weakness → receive targeted help → improve before the next cycle |
| **Business Goal** | Improve student outcomes, reduce concept gap carry-forward, make intervention systematic |
| **Core Constraint** | Cannot add significant manual workload to faculty — alerts must be automated and actionable |
| **Key Risk** | Alert fatigue — if too many notifications fire for minor dips, faculty start ignoring them |
| **Core Assumption** | Faculty will act on alerts if they are specific, low-noise, and require minimal additional effort to respond to |

### Design Principles

- **Specificity over generality** — "Electrostatics: 38%" is actionable. "Physics is weak" is not
- **Push over pull** — the system surfaces problems; users don't have to hunt for them
- **Action over reporting** — every alert should point toward a defined next step, not just display a number
- **Closed-loop accountability** — every intervention should write back into the system so progress is measurable
- **Shared ground truth** — students, faculty, and coordinators should see the same data with no information silos

---

## User Personas

### Persona 1 — Aryan, JEE Aspirant (Student)

Aryan is a 17-year-old in his second year of JEE prep. He's strong in Mathematics but has been consistently weak in Electrostatics and Modern Physics. He doesn't always know where his gaps are — he just knows he's struggling. Without a structured intervention, he moves into the next test cycle carrying the same unresolved weaknesses.

**Pain point:** "I don't know which concepts to revise before the next test, and no one tells me."

---

### Persona 2 — Mr. Sharma, Physics Faculty

Mr. Sharma teaches Physics to a batch of 60 students. He has a strong sense of which students are struggling in class, but he can't track concept-level gaps across 60 students manually after every test cycle. He doesn't open the FCAT dashboard regularly — it's not part of his daily workflow.

**Pain point:** "I know some students are weak in certain topics, but I don't have time to check the portal for every student after every test."

---

### Persona 3 — Priya, Academic Coordinator

Priya oversees academic performance across multiple batches. She needs to know when students are falling behind and whether intervention sessions are actually happening. Currently, she has no visibility into whether faculty have acted on any given student's performance gap.

**Pain point:** "I can see scores, but I can't tell whether anyone has actually done anything about them."

---

## Existing System Problems

Before the feedback loop was introduced, the FCAT workflow looked like this:

1. Student takes test → scores are logged in the portal
2. Performance breakdown is available in the FCAT view
3. Faculty occasionally check the portal
4. No alert fires, no notification is sent
5. Student moves to the next test cycle with gaps unaddressed
6. The same concept failures repeat across multiple cycles

**Specific problems embedded in that flow:**

**No signal delivery** — the portal captured data but had no mechanism to push it to the people who needed to act on it. Passive dashboards require active users. Active users were not consistently checking.

**No concept-level specificity in alerts** — even in cases where coordinators flagged weak students informally, the guidance was subject-level ("this student is weak in Physics"), not concept-level. Faculty couldn't act on that without doing additional diagnosis themselves.

**No structured re-assessment cadence** — re-assessment was informal and inconsistent. It happened when individual faculty remembered to schedule it. It wasn't built into the post-test workflow.

**No loop closure** — there was no mechanism for re-assessment scores to write back into the FCAT. Even when intervention did happen informally, the outcome was invisible to the system. Progress was unmeasured.

**Siloed information** — students, faculty, and coordinators were all working from partial pictures. A student might know their score; the faculty might not. A coordinator might know a student was struggling; the faculty might not have been notified.

---

## Solution Design

The core design principle was simple: **performance data should automatically trigger action, not reports.**

The solution was a closed-loop intervention system layered onto the existing FCAT infrastructure — not replacing it, but activating it.

### Layer 1 — Concept-Level Threshold Triggers

The system monitored scores at the concept level (not the subject level) after every test cycle. When a student's score on a specific concept fell below a defined threshold, an alert was automatically generated.

This specificity was a deliberate design decision. A subject-level alert — "student is weak in Physics" — gives faculty nowhere to start. A concept-level alert — "student scored 38% on Electrostatics" — tells them exactly what to teach, to whom, and when.

### Layer 2 — Automated Notification Routing

Alerts were routed to the relevant subject faculty automatically. Faculty received a structured notification that included:

- The student's name
- The specific concept that triggered the alert
- The score that triggered it
- A suggested action (schedule a remedial session)

The faculty didn't have to find the problem. The problem came to them.

### Layer 3 — Session Assignment & Re-assessment Scheduling

Once an alert fired, the system supported the coordinator in assigning a targeted revision session for the affected student. The session was scoped to the specific concept — not a general "catch-up" session, but a focused remedial intervention.

After the session, a re-assessment was scheduled on the same concept to measure recovery.

### Layer 4 — Score Write-back & Loop Closure

Re-assessment scores were written back into the FCAT. This was the element that closed the loop.

Every intervention now had a measurable outcome. Coordinators could see whether the student's score on the flagged concept had improved, plateaued, or declined. No intervention went unmeasured. No recovery went untracked.

### Layer 5 — Shared Dashboard Visibility

The updated system gave students, faculty, and coordinators aligned visibility into the same data:

- **Students** saw their own concept-level performance, flagged gaps, and upcoming re-assessment schedules
- **Faculty** saw which students in their subject had active alerts and what intervention actions were pending
- **Coordinators** saw the full intervention pipeline — who was flagged, what sessions were assigned, and whether scores had improved post-intervention

---

## Detailed Workflow Walkthrough

**Step 1: Test cycle completes**
Students complete a test. Scores are processed and logged in the FCAT at the concept level — e.g., Electrostatics: 38%, Thermodynamics: 71%, Wave Optics: 44%.

**Step 2: Threshold check runs automatically**
The system evaluates each concept score against the defined intervention threshold. Any score below the threshold generates an alert. This happens without any manual input.

**Step 3: Faculty receives concept-level alert**
Mr. Sharma opens his dashboard and sees: *"Aryan Kumar — Electrostatics: 38%. Intervention recommended."* He doesn't need to browse through 60 student profiles. The system has already surfaced the students who need attention.

**Step 4: Coordinator assigns remedial session**
The academic coordinator schedules a targeted revision session for Aryan, scoped specifically to Electrostatics. The session is logged in the system.

**Step 5: Student sees their gap and upcoming session**
Aryan's dashboard shows his concept-level performance, the flagged weakness, and the scheduled remedial session. He enters the session knowing exactly what will be covered and why.

**Step 6: Re-assessment is administered**
After the remedial session, Aryan takes a concept-specific re-assessment on Electrostatics. The result is captured in the system.

**Step 7: Score writes back into FCAT**
Aryan's updated score is reflected in the FCAT. The coordinator can see whether the intervention worked. If the score has recovered, the alert closes. If not, the loop triggers again.

**Step 8: Full loop visible to all stakeholders**
The complete cycle — detection, intervention, re-assessment, outcome — is visible to the student, the faculty, and the coordinator. No information silos. No guesswork about whether anything happened.

![Screenshot from 2024-01-13 19-06-19.png](attachment:1ac18450-2936-4974-9446-1819ff7fb5e7:Screenshot_from_2024-01-13_19-06-19.png)

---

---

## My Contribution

> I came into this project with close proximity to how the academic workflow actually operated — which meant I could see the gap between what the FCAT was measuring and what the institution needed it to do. That visibility was the starting point for everything that followed.
> 

My role was that of a **Product Consultant working on an internal EdTech platform**. I owned the problem diagnosis, the solution design, and the cross-functional coordination required to ship it.

Here's specifically what I owned:

---

### 1. Problem Identification — Finding the Loop Failure

Through a combination of usage audits, faculty interviews, and student performance pattern analysis, I identified that the FCAT was generating data that nobody was acting on. Students were failing the same concepts across multiple test cycles with no intervention firing in between.

I was the first to frame this explicitly as a **loop failure** — not a data failure, not a dashboard failure, but a broken pathway between signal and action.

**The PM thinking here:** I resisted the default framing ("build a better report") and pushed toward the structural question: why isn't the data triggering a response? That reframe changed the entire solution direction.

---

### 2. Root Cause Reframing — From Visibility Problem to Loop Problem

The team's initial instinct was to improve the FCAT dashboard — make it easier for faculty to find struggling students. I argued that this was solving the wrong problem.

A better dashboard still requires someone to look at it. The real fix was eliminating the dependency on manual check-ins entirely by making the system deliver alerts automatically, at the right level of specificity, to the right person.

This reframe was the critical unlock. It moved the solution from "UI improvement" to "intervention infrastructure."

---

### 3. End-to-End System Design

Once the reframe was accepted, I designed the full intervention flow:

- Defined **concept-level threshold logic** for alert triggers
- Designed the **notification routing structure** — which alerts go to which faculty, in what format
- Specified the **session assignment and re-assessment cadence** in coordination with academic coordinators
- Defined the **score write-back mechanism** to close the loop and make outcomes measurable
- Designed the **multi-stakeholder dashboard** — separate views for students, faculty, and coordinators, all operating on the same underlying data

I functioned as the bridge between academic operations knowledge and product/dev implementation — translating workflow requirements into system specifications.

---

### 4. Cross-functional Coordination

I worked directly with:

- **Dev team** — to define trigger logic, notification format, and score write-back architecture
- **Academic coordinators** — to align on session criteria, re-assessment structure, and threshold definitions
- **Faculty** — to validate that the alert format was actionable and not adding noise to their workflow

This wasn't a solo design exercise. It required alignment across stakeholders with very different mental models of the problem, and I owned that coordination.

---

### 5. Pilot Validation & Handoff

Before full rollout, I validated the loop end-to-end with a pilot batch — ensuring that alerts fired correctly, sessions were being assigned, re-assessments were happening, and scores were writing back accurately. I documented the full flow for handoff and future iteration.

---

### Impact Summary

| Metric | Before | After |
| --- | --- | --- |
| FCAT function | Passive scoreboard | Active intervention engine |
| Low scores | Generated no action | Triggered automated alerts |
| Faculty workflow | Manual, inconsistent | Alert-driven, systematic |
| Concept gap carry-forward | Common across cycles | Reduced through early intervention |
| Re-assessment | Rare, informal | Built into the intervention flow |
| Loop closure | None | Full: detect → act → verify → update |
| Stakeholder visibility | Fragmented | Shared ground truth across student, faculty, coordinator |

---

### What This Project Taught Me About Product Work

The FCAT project reinforced something I now think about in every product context: **a tool that observes but doesn't act is only half a product.**

Data collection is table stakes. The value — and the design challenge — is in what the system does with the data after it's collected. Closing that loop is rarely a technical problem. It's a workflow design problem: who needs to know what, when, and in what form, so that they can take the right action without having to go looking for it.

That principle — designing for action, not just visibility — is what I want to bring to every product problem I work on next.

---

## Screenshots

1. Student Dashboard

![image.png](attachment:a3488c94-a4b5-4673-bc2a-f58d36cc5bf7:image.png)

1. Faculty Dashboard

![image (1).png](attachment:ac8ea130-9dfd-45b3-a430-8ee67a3414e3:image_(1).png)

## Key Takeaways

The core insight this project reinforced is one that applies across every product domain:

> **A system that collects data but doesn't act on it isn't a product. It's a filing cabinet.**
> 

The FCAT had everything it needed to be genuinely useful — granular data, concept-level specificity, regular update cycles. What it was missing was the design layer that connected that data to human action. Adding that layer — alerts, routing, sessions, write-back, shared visibility — didn't require rebuilding the product. It required rethinking what the product was *for*.

The most important product decisions aren't always about new features. Sometimes they're about looking at what a product already knows and asking: *what should happen next?*

---

*Case study written for portfolio purposes. All outcomes are based on real product contribution at FIITJEE.*
