# Module: AI-Integrated SDLC
## Submodule 4 — Architecture as Code

*"A decision record tells a human what was decided once. A constraint file tells an agent what's not allowed, every single time."*

---

### Who this is for

Engineers and architects get the concrete file structure and tooling. Engineering managers get the AI-DLC lifecycle shift and its real governance gaps — this is a section worth reading closely before adopting it wholesale. Security should focus on the security-guardrails category in the architecture template below; it's where network egress rules and secrets handling become machine-enforced rather than merely documented.

---

### Learning objectives

- Describe AWS's AI-DLC lifecycle and how its three phases replace sprint-based planning
- Explain why architecture documentation is shifting from passive ADRs to active, machine-read constraint files
- Apply the six-category architecture-governance template inside an AGENTS.md file
- Use spec-driven development's spec → plan → tasks → code pipeline, including where specs act as CI gates
- Name the real governance gaps in current AI-DLC guidance, so adoption doesn't outrun oversight

---

### 1. AI-DLC: the lifecycle this whole module sits inside

AWS's AI-Driven Development Lifecycle (AI-DLC) replaces the two-week sprint with much shorter cycles — sometimes called "bolts" — on the reasoning that a two-week cycle is largely queueing delay once an agent can draft a domain model or test suite in minutes. It runs three phases: **Inception (Mob Elaboration)**, where product, engineering, and QA convene together while AI drafts requirements and decomposes work — surfacing ambiguity immediately instead of weeks into implementation; **Construction (Mob Construction)**, where AI proposes architecture, code, and tests iteratively, with the team validating each proposal before it executes; and **Operations**, where infrastructure-as-code, deployment, and monitoring get AI assistance under team oversight. *(Source: [AI-DLC Explained — AWS's AI-Driven Development Lifecycle](https://www.exploreagentic.ai/insights/ai-dlc/))* This submodule focuses on what happens inside Construction: how architecture actually gets proposed, constrained, and recorded.

---

### 2. Spec-driven development: the pipeline underneath AI-DLC's Construction phase

Spec-driven development (SDD) gives Construction its actual mechanics: **specification** (outcomes, scope boundaries, constraints, prior decisions, task breakdown, verification criteria) → **planning** (translating the spec into architectural decisions) → **task decomposition** (discrete, testable units) → **code generation** (executed under the spec's constraints). The important shift: a spec here isn't a passive doc — it functions as an *executable contract*. Wired into CI, a build can fail before code ever reaches human review if generated output violates the spec's constraints. *(Source: [Augment Code — What Is Spec-Driven Development](https://www.augmentcode.com/guides/what-is-spec-driven-development))*

The dominant open-source scaffolding for this today is **GitHub Spec Kit** — a CLI supporting roughly 28 agent platforms with four commands: `/speckit.specify`, `/speckit.plan`, `/speckit.tasks`, `/speckit.implement`. AWS's own agent IDE, Kiro, enforces the same shape natively through `requirements.md`, `design.md`, and `tasks.md` files, which is exactly the artifact trail governance requires.

---

### 3. The bigger shift: architecture docs go from passive record to active constraint

Traditional Architecture Decision Records answer *"what did we decide, and why?"* — useful history, but static, and easy for an agent (or a human) to ignore months later. The pattern replacing it treats AGENTS.md (from Submodule 1) as the architecture document instead, answering a different question: *"what rules must never be broken when this code changes?"* An ADR is consulted after the fact, if at all; an AGENTS.md-style constraint file is consulted by the agent *before* it generates anything. *(Source: [AGENTS.md is the new ADR](https://ai.gopubby.com/agents-md-is-the-ew-architecture-decision-record-adr-3cfb6bdd6f2c?gi=24ae3b2b33f3))*

---

### 4. A concrete architecture-governance template

Six categories, kept to roughly 30–60 lines total — the goal is encoding senior-engineer instincts as machine-readable constraints, not writing a design document:

| Category | Example rule |
|---|---|
| Layering & dependencies | UI calls Application services only, never Infrastructure directly; Domain never imports from adapters |
| Data boundaries | PII handled only in designated services; no customer data in logs |
| Error handling | All message handlers idempotent; bounded retries with exponential backoff |
| Observability | Correlation IDs on every request; structured logging mandatory |
| Test expectations | Unit tests for business logic, integration tests for APIs; specific local commands must pass before completion |
| Security guardrails | Network egress requires allowlist updates; secrets via vault only, never committed env files |

Notice the overlap with Submodule 5 (Threat Modeling): the security-guardrails row is where architecture-as-code and security scoping meet directly — a rule here is enforced on every generation, not just checked once during a threat-modeling session.

---

### 5. The governance gap worth naming out loud

Published AI-DLC guidance says humans "verify and approve before execution," but doesn't specify *who* holds approval authority or *what standard* that approval is measured against. A second, sharper gap: the "self-grading problem" — an agent that writes both the code and the tests validating that code is not an independent check, which is exactly why Submodule 1's dual-harness pattern (a different tool building versus reviewing) matters more here, not less. Adopt AI-DLC's speed without also adopting an explicit approval owner and a review harness separate from the build harness, and oversight becomes performative at bolt speed rather than real.

---

### 6. Where this connects

A constraint violated a third time (Submodule 2's Compound rule) belongs as a new line in the architecture-governance file, not a recurring comment in review. And because these constraints are consulted before generation rather than after, they compound in exactly the way Submodule 2 describes: each rule added makes the next Construction cycle cheaper and safer than the last.

---

### Checkpoint

Take your current architecture documentation — ADRs, wiki pages, or nothing formal at all — and draft the security-guardrails and layering rows of the template above for one real service. Where would an agent, left unconstrained, most likely violate a rule your team assumes is obvious?

---

### References

- [AI-DLC Explained — AWS's AI-Driven Development Lifecycle](https://www.exploreagentic.ai/insights/ai-dlc/)
- [Augment Code — What Is Spec-Driven Development](https://www.augmentcode.com/guides/what-is-spec-driven-development)
- [AGENTS.md is the new Architecture Decision Record](https://ai.gopubby.com/agents-md-is-the-ew-architecture-decision-record-adr-3cfb6bdd6f2c?gi=24ae3b2b33f3)
- [How AI-DLC Implements Spec-Driven Development](https://buildwithdc.substack.com/p/aidlc-implements-spec-driven-development)
- [AWS Prescriptive Guidance — Agentic AI patterns and workflows](https://docs.aws.amazon.com/prescriptive-guidance/latest/agentic-ai-patterns/introduction.html)
