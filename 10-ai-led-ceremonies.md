# Module: AI-Integrated SDLC
## Submodule 10 — AI-Led Ceremonies

*"An agent that tells you what happened frees the meeting to be about what to do next — but only if someone still owns the 'what to do next' part."*

---

### Who this is for

Engineering managers and Scrum Masters/PMs get most of this directly — it's their ceremonies being restructured. Engineers should read the standup section closely since it changes what a status update actually is. Everyone should read the risks section: this is the submodule most directly about how automation can go wrong in ways that damage trust rather than just producing a bad output.

---

### Learning objectives

- Map traditional ceremonies onto AI-DLC's bolt-based cadence (Submodule 4) rather than fixed two-week sprints
- Apply the right autonomy level per ceremony — status reporting versus planning versus retrospectives are not the same risk category
- Run an agentic standup correctly: what the agent should generate, and what stays a live conversation
- Distinguish human team velocity from agent capacity, and why treating them as the same number breaks planning
- Name the specific risks (surveillance perception, nuance blindness, metric gaming, hallucination) that make ceremony automation different from code automation

---

### 1. Ceremonies didn't disappear — the cadence they run on changed

Submodule 4 covered AI-DLC replacing two-week sprints with shorter "bolts," on the logic that a two-week cycle is largely queueing delay once an agent can draft a domain model in minutes. Ceremonies don't go away in that model — they compress and shift purpose. A standup, planning session, or retro built for a two-week rhythm doesn't just get automated as-is; it gets re-scoped for a cadence where the underlying work moves at bolt speed, and the ceremony's job becomes surfacing the things a human still has to decide, not reciting status that's already visible elsewhere.

---

### 2. Match autonomy level to the ceremony, not a blanket policy

The clearest documented framework grades four ceremony types by how much an agent should be trusted to run unsupervised:

| Ceremony | Agent autonomy | What stays human |
|---|---|---|
| Status reporting | High — agent pulls what shipped, what's blocked, what changed, drafts the report | PM reads and approves before it sends |
| Sprint/bolt planning | Moderate-to-high — agent tracks capacity drift, scope changes, dependency shifts continuously, surfaces a "plan health" view | Priority decisions stay entirely human |
| Retrospectives | Moderate — agent synthesizes closed tasks, comments, escalations into a draft | Facilitator drives the actual conversation about what changes |
| Reviews (performance, promotion-adjacent) | Limited | Judgment calls on people stay fully human, always |

*(Source: [Quire — Agentic Project Management: The 2026 Playbook](https://quire.io/blog/p/agentic-project-management.html))* Status reporting is the correct low-risk entry point for a team just starting to adopt this — it's approval-only by design, which makes a bad first draft cheap to catch.

---

### 3. What an agentic standup actually looks like

A concrete, documented pattern: an agent scans git (commits, push timestamps), the project tracker (ticket status transitions), and team chat, then posts an async summary before the synchronous meeting even starts — something like *"Rohan completed the API logic, no blockers. Sarah is stuck on the database migration (Error 503), needs DevOps."* Blockers surface two ways: automated detection of stalled tickets or failed deployments, and contextual analysis flagging work that hasn't progressed across recent commits. The result: the live meeting compresses to a few minutes focused only on resolving what's actually blocked, instead of a status recitation everyone could already read. *(Source: [AI Scrum Master: Can Agents Run Your Daily Standup?](https://agileleadershipdayindia.org/blogs/agentic-ai-agile-project-office/ai-scrum-master-automate-daily-standup.html))*

---

### 4. Two capacities, not one: human velocity vs. agent capacity

A structural mistake worth naming explicitly: treating an AI agent's throughput as the same kind of number as a human team's velocity. They aren't. The recommended model runs sprint/bolt planning as two distinct conversations — human team velocity commitments, tracked the traditional way, and AI agent capacity budgeting, tracked separately with an assigned human "handler" accountable for what that agent takes on. *(Source: [Agentic AI Is Rewriting the Sprint Lifecycle](https://medium.com/agileinsider/agentic-ai-is-rewriting-the-sprint-lifecycle-2ecd15bee4c4))* Definition of Done needs a parallel update for agent-completed tickets specifically — requiring human code review and automated test passage before anything an agent built counts as "done," which is the ceremony-level version of the dual-harness principle from Submodule 1.

---

### 5. Retros need a new diagnostic question

Alongside the usual "what should we change," an AI-led retro should explicitly ask: *what did our agents fail at, and why?* That question is where this submodule connects directly back to Submodule 2's Compound Engineering loop — a recurring agent failure surfaced in retro is exactly a "third occurrence" candidate for becoming a permanent rule in an instruction file or skill, not just a talking point that resurfaces unresolved next retro.

---

### 6. The risks that are specific to automating ceremonies, not code

Ceremony automation fails in ways code automation doesn't, because the subject is people, not just artifacts. Named risks worth taking seriously: **surveillance perception** — developers can reasonably feel monitored when an agent is reading their commit timestamps for a status report; **nuance blindness** — the system has no way to detect that someone's slower pace this week is exhaustion or a personal circumstance, not a blocker; **metric gaming** — teams can learn to commit unnecessary code just to look active in the agent's summary; and **hallucination risk** — a human still has to audit whether the agent correctly interpreted what actually happened, especially before a status report goes out under the team's name. None of these are reasons not to automate — they're reasons the human facilitator role doesn't disappear, it shifts to auditing and psychological safety.

---

### 7. The universal guardrail

Across every ceremony, the same rule holds: an agent should surface a planned action for human approval before executing anything with real consequence — a reassignment, a scope cut, a report going out externally. "Hand control back" before executing is the ceremony-level equivalent of the approval checkpoints in Submodule 4's AI-DLC Construction phase and Submodule 9's execution gates — the pattern repeats because the underlying principle is the same one.

---

### 8. Where this connects

An agent capacity budget that consistently overruns is itself a metric worth tracing (Submodule 8) rather than re-negotiating from scratch every bolt. And a retro's "what did our agents fail at" answer, once it recurs, becomes a Submodule 2 Compound entry the same way a code review finding does — the mechanism for turning a lesson into a standard doesn't change just because the lesson came from a ceremony instead of a PR.

---

### Checkpoint

Look at your team's next scheduled standup or retro. Identify one piece of it that's pure status recitation an agent could draft from existing data, and one piece that's a genuine judgment call that has to stay human. Draft what the agent's summary would say for the first one — and notice how much of the actual meeting time that would free up for the second.

---

### References

- [Quire — Agentic Project Management: The 2026 Playbook](https://quire.io/blog/p/agentic-project-management.html)
- [AI Scrum Master: Can Agents Run Your Daily Standup?](https://agileleadershipdayindia.org/blogs/agentic-ai-agile-project-office/ai-scrum-master-automate-daily-standup.html)
- [Agentic AI Is Rewriting the Sprint Lifecycle](https://medium.com/agileinsider/agentic-ai-is-rewriting-the-sprint-lifecycle-2ecd15bee4c4)
- [Spinach — AI Scrum Master: What it is and how agile teams benefit](https://www.spinach.ai/blog/ai-scrum-master)
