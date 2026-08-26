# Module: AI-Integrated SDLC
## Submodule 3 — Test Suite Management

*"An agent that writes tests fast is not the same as an agent that writes tests that catch bugs."*

---

### Who this is for

Engineers get the concrete tooling and rules. Engineering managers and QA leads get the case for why "more tests, faster" isn't automatically progress. Security should note the flaky-test triage section — an agent that silently quarantines a failing test is exactly the kind of unsupervised action that shouldn't happen near anything security-relevant.

---

### Learning objectives

- Explain why unconstrained AI test generation creates a false-confidence problem, not just a speed win
- Apply coverage-aware generation so new tests land in the right place with the right context
- Apply the seam-based, vertical-slice discipline that keeps AI-written tests meaningful
- Name the anti-pattern of tautological assertions and how to catch it
- Describe how flaky-test triage should be scored deterministically first, with AI only for the ambiguous middle, and a human for the final call

---

### 1. The new failure mode: fast tests that don't test anything

Test suites used to fail by being too small. The AI-assisted failure mode is different: suites that grow large very fast while quietly losing the property that makes a test worth having — the ability to fail when the code is actually wrong. An agent asked to "add tests" with no constraints will often generate many tests in one pass across unrelated seams (horizontal slicing) and, worse, write assertions that simply recompute the expected value the same way the implementation does — a tautological test that passes by construction and can never catch a real bug. Suite size goes up; suite value doesn't. This is the problem test-suite management for AI-assisted SDLC actually has to solve.

---

### 2. Coverage-aware generation: give the agent the map before it writes anything

Rather than letting an agent search a whole codebase to guess where a test belongs, a newer pattern feeds it real coverage data first. JetBrains' `finding-tests` skill queries its dotCover coverage tool to find which existing tests already exercise the code near a change, hands the agent that exact file, and lets it match the project's existing conventions and style rather than inventing new ones. In a documented example, this cut a test-writing task from 26 tool calls and 1.01M tokens down to 14 tool calls and 612K tokens — roughly half the cost — while landing the test in the correct file with matching style. *(Source: [JetBrains — coverage map for AI agents](https://blog.jetbrains.com/dotnet/2026/05/22/claude-codex-ai-agent-skill-for-writing-tests/))* The generalizable lesson beyond this specific tool: wherever a coverage tool exists in your stack, wiring it into the agent's context before test-writing begins is a directly measurable efficiency and consistency win.

---

### 3. Seam-based, vertical-slice TDD for agents

The strongest documented discipline against horizontal slicing comes from a dedicated TDD skill: before any test is written, the agent must identify and get explicit confirmation on the "seams" — the public boundaries where behavior can actually be observed. No test gets written at an unconfirmed seam. Once a seam is agreed, the cycle runs vertically: one failing test, the minimal code to pass it, then the next seam — never a batch of tests written up front. *(Source: [Matt Pocock's TDD skill](https://skillselion.com/skills/mattpocock/skills/tdd))*

Two rules from this skill are worth adopting even outside this exact tool:

- **Red before green, refactor deferred.** Write the failing test first, write only enough code to pass it, and push refactoring to a separate review pass (a code-review skill, per Submodule 1) rather than letting the agent restructure code while it's only protected by one fresh test.
- **No tautological assertions.** An expected value must come from an independent source — a known literal, a worked example, a spec — never a recomputation of the implementation's own logic. This single check catches most "tests that can never fail" before they ship.

---

### 4. Flaky-test triage: deterministic first, AI second, human last

Flaky tests are exactly the wrong place to hand a model unlimited discretion, and the strongest documented pattern here (FlakeWarden, an AgentHack 2026-winning system) makes that explicit through its ordering. It first scores every failing test deterministically across five signals — flip frequency, retry-recovery rate, isolation behavior, error-signature variance, and runtime instability — combined into a single flake score. Scores above 0.62 are confidently flaky, below 0.38 confidently not; only the ambiguous 0.38–0.62 band goes to an AI classifier, and even then only with hard evidence (stack traces, selector diffs, commits) that it must cite in its reasoning. A hard safety rule caps the score whenever a UI selector changed at the same moment the test broke — so a genuine regression can never get waved off as "just flaky." No verdict executes automatically; every classification becomes a proposal a human approves before anything is quarantined. *(Source: [FlakeWarden — AgentHack 2026](https://forum.uipath.com/t/flakewarden-agentic-flaky-test-triage-on-test-cloud-agenthack-2026-winner/5770067))*

---

### 5. Where this connects to the rest of the module

If a category of flaky test or a specific tautological-assertion mistake shows up a third time, that's a Submodule 2 "Compound" moment — it belongs in the TDD skill's rule set, not in someone's memory. And the review harness from Submodule 1 has a natural extension here: a review pass that specifically flags tautological assertions and horizontal-slice PRs is a legitimate, narrow addition to a review skill's checklist.

---

### 6. Anti-patterns to name explicitly

Bulk-generating tests across many seams in one pass. Assertions that recompute rather than independently verify. Letting an agent silently quarantine or delete a flaky test without a deterministic score and a human sign-off. Treating rising test count as a proxy for rising test suite quality.

---

### Checkpoint

Pick one recently AI-generated test file. For each test, ask: does its expected value come from an independent source, or does it just recompute what the implementation does? Flag any tautological ones — that's the single highest-value five-minute audit available on an existing suite.

---

### References

- [JetBrains — What happens when you give AI agents the map of your code's coverage](https://blog.jetbrains.com/dotnet/2026/05/22/claude-codex-ai-agent-skill-for-writing-tests/)
- [Matt Pocock's TDD skill for Claude Code](https://skillselion.com/skills/mattpocock/skills/tdd)
- [FlakeWarden — agentic flaky-test triage, AgentHack 2026 winner](https://forum.uipath.com/t/flakewarden-agentic-flaky-test-triage-on-test-cloud-agenthack-2026-winner/5770067)
- [TDD with AI Agents: A Practical Guide (2026)](https://www.fundesk.io/test-driven-development-ai-agents-guide)
