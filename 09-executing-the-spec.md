# Module: AI-Integrated SDLC
## Submodule 9 — Executing the Spec

*"A spec is a promise. Execution is where you find out if it was a promise you could actually keep."*

---

### Who this is for

Engineers get the core mechanics — task decomposition, verification gates, parallel execution. Engineering managers get the "human agency at checkpoints" model, which is the actual answer to "how much do we trust the agent here." Product and security should read the drift-handling section closely: it's the moment where a gap in the original brief (Submodule 7) or an unenforced architecture rule (Submodule 4) either gets caught immediately or ships silently.

---

### Learning objectives

- Break an approved spec into isolated, independently testable task units correctly
- Apply verification gates between tasks rather than only at the end of a feature
- Handle spec drift and mid-execution ambiguity without letting it compound silently
- Decide when parallel, worktree-isolated agent execution is appropriate versus sequential
- Know where human review checkpoints are structurally required, not optional

---

### 1. From approved spec to task units

Once a spec is approved — whether written with GitHub Spec Kit, Kiro Specs, or another format from Submodule 7 — execution starts with decomposition, not code. Each task should be implementable and testable in isolation: a unit small enough that "did this work?" has an unambiguous answer. GitHub Spec Kit does this programmatically — a `tasks generate` step turns the specification into individual implementation tasks, each then executed independently (e.g. `implement --agent=<harness> --task=<id>`). *(Source: [Augment Code — Automating Spec-Driven Development with AI Agents](https://www.augmentcode.com/guides/automating-spec-driven-development-with-ai-agents))* The practical discipline underneath any tool: divide and conquer. Feeding an agent one focused task at a time — backend before frontend, schema before API logic — avoids the "curse of instructions," where too many simultaneous directives measurably degrade output quality compared to sequenced, focused ones. *(Source: [Addy Osmani — How to write a good spec for AI agents](https://addyosmani.com/blog/good-spec/))*

---

### 2. Verification gates belong between tasks, not just at the end

The strongest documented execution workflows treat validation as embedded infrastructure, not an optional step someone remembers to run later: code must compile, unit tests must pass, a security scan must complete, and performance benchmarks must clear their bar — all before the next task proceeds. *(Source: [Augment Code — Automating Spec-Driven Development](https://www.augmentcode.com/guides/automating-spec-driven-development-with-ai-agents))* The practical version of this rhythm: don't wait until a feature is "done" to check it against the spec — test after each function or milestone, and let a failed test block progress rather than accumulate as technical debt to sort out at the end. This is the same principle as Submodule 3's TDD discipline, applied at the task-execution level instead of the individual-test level.

---

### 3. Handling drift and mid-execution ambiguity

Specs will still have gaps that only surface once implementation is underway — that's expected, not a failure of the spec-writing process. What matters is what happens next: the spec, not a side conversation or an ad hoc code comment, is the thing that gets updated first. The corrected sequence is: update the spec document, then explicitly re-brief the agent against the change ("I have updated the spec as follows — given this, adjust the plan or refactor accordingly"), and version-control the spec itself so its evolution stays traceable for both the human and the agent. *(Source: [Addy Osmani — How to write a good spec for AI agents](https://addyosmani.com/blog/good-spec/))* Skipping this and just telling the agent verbally is how the spec and the shipped code quietly diverge — exactly the drift this whole discipline exists to prevent.

Auditability is the backstop: capturing each spec-to-implementation run as a replayable workflow (a pattern used in tools like Cosmos) means a team can detect after the fact when executed code diverged from what was approved, even if it wasn't caught live.

---

### 4. Parallel execution with git worktrees — when it earns its complexity

For genuinely independent tasks, multiple agents can execute in parallel using git worktrees: each gets its own branch, working directory, and index (`.trees/TASK-123/`, `.trees/TASK-456/`, etc.) while sharing the same underlying object database, so agents never collide on files mid-execution. Conflicts don't disappear — they move to merge time, where standard git tooling surfaces them, instead of happening silently while both agents are still working. *(Source: [Augment Code — Git Worktrees for Parallel AI Agent Execution](https://www.augmentcode.com/guides/git-worktrees-parallel-ai-agent-execution))*

| Use parallel worktrees when | Stay sequential when |
|---|---|
| Tasks are genuinely independent, minimal file overlap | One agent's output is a dependency for another's input (e.g. API before the frontend that calls it) |
| 3–5 concurrent agents, each on distinct functionality | Work is exploratory with requirements still emerging |
| Each task completes in about an hour or less | The feature needs tightly coordinated, single-threaded implementation |

The task-decomposition step from Section 1 is the actual prerequisite here — worktree isolation solves file collisions, not architectural dependencies. Two agents building coupled pieces in parallel will still produce a broken integration; that has to be sequenced regardless of how many worktrees are available.

---

### 5. Where human agency stays structurally required

None of this is meant to run fully unattended. Review is mandatory at defined phase boundaries — after Specify, after Plan, and again before Implement proceeds past its verification gates — which is what keeps "human agency" real rather than a rubber stamp. This is the direct execution-time counterpart to Submodule 4's governance gap: an approval step that exists on paper but has no named owner or defined standard is exactly the performative oversight that AI-DLC's speed makes easy to fall into.

---

### 6. Where this connects

A task that fails its verification gate for the same reason a third time is a Submodule 2 "Compound" moment — the missing check belongs in the task-generation step itself, not in a human's memory of "watch out for that." A verification gate that should include a security scan or architecture-constraint check pulls directly from Submodule 4's AGENTS.md and Submodule 5's threat-modeling categories, rather than being invented fresh per project. And every executed task here is exactly what Submodule 8's outcome tracing needs a trace for — execution is the event; tracing is how you know later whether it actually held up.

---

### Checkpoint

Take a spec currently mid-implementation (or your last completed one). List its tasks and ask, for each: was there an explicit verification gate before the next task started, or did validation happen only once at the very end? Pick one task where drift was discovered mid-execution and trace whether the spec document itself got updated first, or whether the fix just went straight into code.

---

### References

- [Augment Code — Automating Spec-Driven Development with AI Agents](https://www.augmentcode.com/guides/automating-spec-driven-development-with-ai-agents)
- [Addy Osmani — How to write a good spec for AI agents](https://addyosmani.com/blog/good-spec/)
- [Augment Code — Git Worktrees for Parallel AI Agent Execution](https://www.augmentcode.com/guides/git-worktrees-parallel-ai-agent-execution)
- [GitHub Spec Kit: How It Works (2026 Guide)](https://codemyspec.com/blog/github-spec-kit-guide)
- [What is AIDLC? The AI Development Lifecycle Explained](https://www.augmentcode.com/guides/what-is-aidlc-ai)
