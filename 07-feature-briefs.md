# Module: AI-Integrated SDLC
## Submodule 7 — Feature Briefs

*"'The UI should look nice' is a sentence a person can work with and an agent can't."*

---

### Who this is for

Product owns most of this submodule directly — feature briefs are the artifact product writes. Engineers need to know what a brief should already answer before it reaches them, so a missing section is caught at brief-writing time, not mid-implementation. This is the direct downstream step from Submodule 6's meeting-to-PRD pipeline, and it feeds Submodule 8 (Outcome Tracing) through its success-metrics section.

---

### Learning objectives

- Explain why briefs written for AI code-generation need to be machine-parseable, not just human-readable
- Apply the full agent-executable PRD template, including the AI-feature addendum for anything model-based
- Match brief detail level to the harness: "copilot" tools need less upfront completeness than "autopilot" tools
- Know the current landscape of spec/brief tooling well enough to pick one deliberately
- Apply "draft first, interrogate second" instead of trying to write a perfect brief in one pass

---

### 1. Why the brief itself had to change

A traditional PRD is written for a human who fills gaps with judgment and asks clarifying questions in a hallway conversation. An agent does neither — it either executes exactly what's written or hallucinates the gap. That forces three real changes: **unambiguous specificity** ("dark theme with frosted-glass effect cards," never "make it look nice"), **explicit technical constraints stated upfront** (stack, performance targets, scale — not assumed defaults), and **complete context in a single pass**, since modern harnesses can hold 200K+ tokens of context and briefs should use that headroom rather than trickling requirements out over follow-up messages. *(Source: [Writing PRDs for AI Code Generation Tools in 2026](https://www.chatprd.ai/learn/prd-for-ai-codegen))*

---

### 2. The template: a classic spine plus an AI-feature addendum

The core spine, in order: overview; goals (user-facing, business, and explicit non-goals); core concepts and domain terms; entry points (affected screens/triggers); user flows; UI specification covering all four states (default, loading, error, empty); a role-based permissions matrix; edge cases with expected behavior; analytics instrumentation (event names and properties); acceptance criteria as binary pass/fail per feature area; success metrics with post-launch targets; deferred future enhancements with rationale; and open questions with named owners and due dates.

When the feature itself is AI-based, add six more sections conditionally: why a model is justified over a deterministic approach; an evaluation plan (golden set, grading method, ship bar); autonomy levels and tool permissions per action; failure modes and fallback UX for hallucinations, wrong tool calls, injection, and cost overruns; a cost-and-latency budget; and a phased rollout with measurable exit criteria. *(Source: [Product Map — AI PRD Template](https://www.productmap.io/blog/ai-prd-template))* Note how directly the failure-modes and autonomy sections connect back to Submodule 5's threat-modeling categories — a feature brief for an AI feature is, in part, a lightweight security-scoping document.

---

### 3. Match brief completeness to the harness, not a fixed standard

Not every brief needs every section filled exhaustively before work starts — it depends on which kind of harness (Submodule 1) will execute it. Copilot-style tools working iteratively inside an IDE (Cursor-style) tolerate incremental refinement — a brief can be good enough to start and get sharpened through feedback. Autopilot-style tools running more autonomously need detailed, complete-upfront requirements, because there's no human in the loop mid-execution to resolve an ambiguity the way there is with a copilot tool. Writing every brief to autopilot-completeness standards when a copilot tool will execute it is wasted upfront effort; writing an autopilot brief at copilot-level vagueness is how autonomous runs go sideways.

---

### 4. The current tooling landscape

| Tool | Best for |
|---|---|
| GitHub Spec Kit | Structured multi-file spec workflow via slash commands (`/speckit.specify`, etc.) |
| Kiro Specs | Formal requirements in EARS notation with auto-generated design docs |
| OpenSpec | Lightweight, feature-as-reviewable-proposal workflow |
| Task Master | Automatic decomposition of a plain-text PRD into ordered tasks |
| BMAD-METHOD | Distinct PM / Architect / Developer agent roles each producing their own artifact |
| AGENTS.md | Single tool-agnostic file every agent reads — the connective tissue across all of the above |
| Tessl Spec Registry | Prevents agents hallucinating third-party library APIs |
| ai-dev-tasks / Snarktank | Minimal copy-paste workflow for solo developers or small teams |
| spec-workflow-mcp | Approval-gated workflow with a live dashboard for requirements/design/tasks |

*(Source: [9 PRD and Spec Templates Built for AI Coding Agents](https://securityboulevard.com/2026/06/9-prd-and-spec-templates-built-for-ai-coding-agents/))* No single tool is "correct" — pick based on team size, whether you need role-separated agents (BMAD), or whether a lightweight proposal model (OpenSpec) fits your review culture better than a heavier multi-file spec.

---

### 5. Draft first, interrogate second

The recommended discipline inverts the instinct to perfect a brief before sharing it: draft the full template fast, even with gaps, then interrogate it section by section for what's missing or ambiguous — prioritizing which gaps matter most rather than filling every section in strict order. A brief that's 80% complete and actively being sharpened moves faster than one held back until it's theoretically finished.

---

### 6. Where this connects

The success-metrics section here is the direct handoff into Submodule 8 (Outcome Tracing) — a metric with no defined post-launch target at brief time is a metric nobody traces later. And a brief's AI-feature addendum should be reviewed using the same dual-harness principle from Submodule 1: whoever writes the brief shouldn't be the only one grading whether its evaluation plan and ship bar are actually rigorous.

---

### Checkpoint

Take a feature brief you've written or received recently. Check it against the "unambiguous specificity" test: find one sentence that reads like "make it better" or "should look nice," and rewrite it as a measurable, agent-executable requirement.

---

### References

- [Writing PRDs for AI Code Generation Tools in 2026](https://www.chatprd.ai/learn/prd-for-ai-codegen)
- [Product Map — AI PRD template: the full structure agents can execute](https://www.productmap.io/blog/ai-prd-template)
- [9 PRD and Spec Templates Built for AI Coding Agents](https://securityboulevard.com/2026/06/9-prd-and-spec-templates-built-for-ai-coding-agents/)
- [How to Write Product Requirements for AI Features (2026)](https://www.ideaplan.io/blog/how-to-write-product-requirements-for-ai-features)
