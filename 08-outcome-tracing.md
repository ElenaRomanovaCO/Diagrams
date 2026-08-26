# Module: AI-Integrated SDLC
## Submodule 8 — Outcome Tracing

*"A trace tells you what happened. Only an eval tells you whether that was good."*

---

### Who this is for

This closes the loop for everyone in the module. Product needs this to know whether the success metrics defined back in Submodule 7's feature brief actually happened. Engineering needs the tracing standard so instrumentation is portable and consistent. Security and management both care about the same underlying principle: if you can't explain why an agent did something, you don't actually control it.

---

### Learning objectives

- Apply the standard OpenTelemetry GenAI span hierarchy so tracing is portable across observability tools
- Distinguish what a trace tells you from what an eval tells you, and why you need both
- Apply eval-driven development's loop: golden datasets → eval gates → production monitoring → feedback into the golden set
- Trace a shipped feature's outcome back to the specific success metric defined in its original brief
- Know the minimum two metrics no agentic system should ship without

---

### 1. The standard: OpenTelemetry GenAI conventions

Rather than each team inventing its own tracing format, a vendor-neutral standard has emerged: `gen_ai.*` span and metric attributes, portable across observability platforms so instrumentation doesn't have to be rewritten if the platform changes. Four span types cover an agentic system end to end: `create_agent` (instantiation, fires once), `invoke_agent` (a single execution — CLIENT kind if remote, INTERNAL if local), `invoke_workflow` (the parent span wrapping a multi-agent orchestration), and `execute_tool` (an individual tool call). The practical payoff: a multi-agent handoff becomes one connected, legible trace instead of scattered logs you have to manually reassemble. *(Source: [OpenTelemetry GenAI Conventions for Agent Tracing](https://www.digitalapplied.com/blog/ai-agent-observability-2026-tracing-monitoring-stack-guide))*

Two metrics are the non-negotiable floor: `gen_ai.client.operation.duration` (latency) and `gen_ai.client.token.usage` (tokens in/out). Without exporting these two, cost and speed simply aren't things you can reason about — not "hard to reason about," genuinely impossible.

---

### 2. Three layers of what to actually capture

A trace worth having spans three layers: the **input layer** (data versions, user session, retrieval sources feeding the agent's reasoning), the **decision layer** (intermediate reasoning steps, tool calls with their parameters, guardrail evaluations), and the **outcome layer** (success/failure labels, business context, compliance metadata). Most teams instrument the decision layer well and skip the outcome layer entirely — which is exactly the layer that turns a debugging tool into a business-outcome tool. *(Source: [Agentic AI Observability Playbook 2026](https://www.arthur.ai/column/agentic-ai-observability-playbook-2026))*

---

### 3. Traces answer "what happened." Evals answer "was it good?"

This is the distinction the whole submodule turns on. A trace is a faithful record of execution — it will happily show you an agent that executed flawlessly toward the wrong outcome. An **eval gate** is a scorer paired with that trace, grading output quality against a defined bar. The mature pattern runs both together: traces capture the path, eval gates grade whether the destination was actually good, and together they let a team block a regression from shipping or flag a live quality drop before it damages a real outcome.

---

### 4. Eval-driven development: the loop that ties pre- and post-launch together

Treat evals as the actual product specification, not an afterthought bolted on before launch. **Golden datasets** — curated input/approved-output pairs — form the regression baseline every change is scored against, across dimensions like accuracy, tone, and completeness. **Eval gates** enforce a quality threshold in CI/CD, automatically blocking a change that drops a metric past an acceptable limit, the same way for every change regardless of what it touched under the hood. Once live, **production monitoring** runs a subset of the same evals against real traffic, so development and production share one scoring logic instead of two definitions of "good" that quietly drift apart. The loop closes when production traces reveal a genuinely new edge case: that case gets added back into the golden set, so the evaluation criteria keep evolving with actual user behavior instead of staying frozen at launch-day assumptions. *(Source: [Braintrust — What is eval-driven development](https://www.braintrust.dev/articles/eval-driven-development))*

---

### 5. Closing the loop back to the feature brief

This is where Submodule 7's success-metrics section stops being a planning artifact and becomes an operational one: each metric defined there should map to a specific eval or a specific outcome-layer trace attribute, checked against the target the brief committed to, on a defined post-launch schedule. A success metric with no corresponding trace or eval is a promise nobody is actually keeping track of. Where the brief's AI-feature addendum defined a "ship bar" and failure modes, outcome tracing is the mechanism that continuously checks the shipped feature is still clearing that bar in production, not just on launch day.

---

### 6. Where this connects across the whole module

This is deliberately the last submodule because it closes every earlier loop at once: a recurring outcome-layer failure is a Submodule 2 "Compound" candidate (codify the fix as a rule); a trace revealing an architecture constraint violation belongs back in Submodule 4's AGENTS.md; and an outcome trace surfacing a new attack pattern is a live input to Submodule 5's continuous threat-model updates.

---

### Checkpoint

Take one feature currently live in production. Find its original success metric (from its brief, if one exists). Ask: is there an actual trace attribute or eval currently measuring that specific metric — or has it been assumed true since launch without anyone checking?

---

### References

- [OpenTelemetry GenAI Conventions — Agent Observability Tracing & Monitoring Stack](https://www.digitalapplied.com/blog/ai-agent-observability-2026-tracing-monitoring-stack-guide)
- [Agentic AI Observability: A 2026 Playbook — Arthur](https://www.arthur.ai/column/agentic-ai-observability-playbook-2026)
- [Braintrust — What is eval-driven development](https://www.braintrust.dev/articles/eval-driven-development)
- [What Is Eval-Driven Development? — FutureAGI Guide (2026)](https://futureagi.com/glossary/eval-driven-development/)
