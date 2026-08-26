# Module: AI-Integrated SDLC
## Submodule 6 — Backlog Grooming

*"An agent that triages your backlog is only useful if a human still owns the judgment calls it can't make."*

---

### Who this is for

Product and engineering management get most of this one — it's where the AI-DLC pattern moves upstream of code entirely. Engineers benefit from understanding what's now automated before a ticket ever reaches them, so they know what to trust and what to double-check. This submodule assumes the file/skill vocabulary from Submodule 1 and the Compound-Engineering loop from Submodule 2, both of which apply directly to a backlog agent's own rule set.

---

### Learning objectives

- Name the four core triage functions an agentic backlog system performs today
- Know what inputs those functions actually require, and where accuracy predictably degrades
- Apply the meeting-transcript-to-ticket pipeline as a concrete agentic workflow
- Combine agentic scoring with an explicit prioritization framework instead of an opaque AI ranking
- Identify where human review checkpoints must remain non-negotiable

---

### 1. What an agentic backlog system actually does

Four functions show up consistently across current tooling: **duplicate detection** via semantic similarity — transformer-based embeddings that catch meaning, not just keyword overlap, so "login fails on mobile" and "auth broken on iOS Safari" get correctly flagged as the same issue; **severity classification** using classifiers trained on historical bug data; **auto-labeling and routing**, where an NLP classifier reads a ticket's title and description and assigns component/team/feature tags automatically; and **effort estimation**, predicting story points from historical issue data. That last one comes with a real caveat worth stating plainly: accuracy degrades sharply in cross-project scenarios — a model trained on one team's history estimates that team's tickets far better than a stranger's. *(Source: [Augment Code — AI Backlog Grooming](https://www.augmentcode.com/guides/ai-backlog-grooming))*

---

### 2. What it needs to work, and what happens without it

These functions aren't magic — they need historical backlog data to train on, real codebase context (one documented system processes 400,000+ files for this), and ticket metadata with enough history to learn from. A team standing this up on day one, with no history, should expect it to behave like a junior triager: reasonable on the obvious cases, unreliable on anything requiring institutional memory. Reported gains where it's mature: 30 minutes to 2+ hours saved per sprint, and up to a 45% reduction in backlog triage time. The honest caveat alongside those numbers: throughput gains upstream don't automatically translate downstream — one report notes "delivery instability remains elevated" even where triage sped up, meaning faster grooming without matching capacity elsewhere just moves the bottleneck rather than removing it.

---

### 3. From meeting to ticket: the agentic pipeline

A concrete three-stage pipeline turns a raw stakeholder conversation into backlog-ready work: **input processing** takes the meeting transcript as-is; a **PRD-generation** step (an agent purpose-built for this, not a general chat prompt) turns the discussion into a structured product requirements document; and a **ticket-creation** step extracts discrete, actionable tickets from that PRD and pushes them directly into Jira or Linear with consistent formatting. *(Source: [Mistral — Agentic workflows from meetings to dev tickets](https://mistral.ai/fr/news/agentic-workflows-from-meetings-to-dev-tickets))* The value isn't just speed — it's consistency: every ticket traces back to the same PRD structure instead of however the person writing it up that day happened to phrase it.

---

### 4. Score with a named framework, not an opaque ranking

An agent that hands back "priority: high" with no visible reasoning is a worse decision aid than a spreadsheet. Pair agentic scoring with an explicit, inspectable framework — **RICE** (Reach × Impact × Confidence ÷ Effort) for reach-driven feature work, or **WSJF** (Weighted Shortest Job First: cost of delay ÷ job size) when time-sensitivity and sequencing matter more than raw reach. The agent's job is to populate the framework's inputs faster and more consistently — surfacing likely reach from usage data, flagging effort estimates that look off relative to similar past tickets — not to replace the framework with its own unlabeled judgment.

---

### 5. Where the human checkpoint has to stay

Duplicate detection and auto-labeling are low-stakes to automate fully — a wrong label gets caught and fixed cheaply. Severity classification and effort estimation are not: a misjudged severity can bury a real incident, and a bad estimate cascades into a bad sprint commitment. Keep human review mandatory specifically at the point where a classification changes what gets worked on next, not just how it's tagged — that's the line between administrative automation and a decision an agent shouldn't be making alone.

---

### 6. Where this connects

If the backlog agent's severity or effort model is consistently wrong for a specific ticket category — a third occurrence, per Submodule 2 — that's a signal to retrain or add an explicit rule, not to keep manually correcting it every sprint. And a PRD generated from a meeting is the natural upstream input to Submodule 7 (Feature Briefs) — the two are adjacent stages of the same pipeline, not separate processes.

---

### Checkpoint

Pull your last 10 groomed tickets. For each, ask: was the priority score inspectable — could you see *why* — or was it a number you had to trust? Redo the scoring for one ticket using RICE or WSJF explicitly, and compare it to what the agent (or your team) originally assigned.

---

### References

- [Augment Code — AI Backlog Grooming: How Engineering Teams Cut Triage Time](https://www.augmentcode.com/guides/ai-backlog-grooming)
- [Augment Code — How AI Ticket Triage Workflows Route Engineering Work](https://www.augmentcode.com/guides/ai-ticket-triage)
- [Mistral — Agentic workflows: from meetings to dev tickets](https://mistral.ai/fr/news/agentic-workflows-from-meetings-to-dev-tickets)
- [RICE vs WSJF: Choosing the Right Prioritization Framework](https://www.centercode.com/blog/rice-vs-wsjf-prioritization-framework)
