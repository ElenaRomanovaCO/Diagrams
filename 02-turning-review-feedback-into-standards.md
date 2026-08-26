# Module: AI-Integrated SDLC
## Submodule 2 — Turning Review Feedback into Standards

*"A lesson a review teaches once and nobody writes down gets re-taught forever."*

---

### Who this is for

Builds directly on Submodule 1 (Codebase Standards and Patterns) — same file types (CLAUDE.md/AGENTS.md, SKILL.md), same review-skill mechanics, now applied as a closing step rather than a one-time setup. Engineers get the workflow and file changes; engineering managers get the case for why this changes team velocity over months, not days; product and security get the same benefit from a different angle — recurring feedback on requirements ambiguity or security gaps gets captured the same way recurring code issues do.

---

### Learning objectives

- Name the underlying problem: why AI-assisted teams plateau instead of compounding without this practice
- Apply the "Plan → Work → Review → Compound" loop as a mandatory step, not an optional retro
- Know the five places a lesson can land, and pick the right one for a given kind of feedback
- Apply the "third occurrence" rule to avoid over-codifying from a single data point
- Recognize the maintenance cost this creates and the discipline that offsets it

---

### 1. The problem this solves: capability without accumulation

Teams running AI-assisted development often notice something counterintuitive: the model gets more capable release over release, but the team's actual output doesn't compound the way that should predict. The reason is almost always the same — knowledge learned in a code review evaporates the moment the PR merges. The agent re-explains the same convention next week, fixes a variant of the same bug next month, and every review pays the same "teaching tax" it paid the first time. This pattern is named **Compound Engineering**, and its premise is simple: codification has to be a closing condition of the work, not an optional afterthought. *(Source: [Compound Engineering — Encyclopedia of Agentic Coding Patterns](https://aipatternbook.com/compound-engineering))*

---

### 2. The loop: Plan → Work → Review → Compound

Most teams already run the first three steps. The fourth is the one that gets skipped under deadline pressure — and it's the one that determines whether next month's work gets cheaper or stays flat.

Before a fix, feature, or review is considered done, the closing question is: *what general lesson did we learn here, and which durable surface should it live on?* That question turns a one-off correction into a standing asset the next task inherits for free.

---

### 3. Where a lesson lands: five surfaces, not one

Not every piece of feedback belongs in the same place — routing it correctly is most of the skill. These map directly onto the file types from Submodule 1:

| Surface | What it's for | Maps to |
|---|---|---|
| Instruction files | Durable "always/never" rules ("use 2-space indentation in markdown") | CLAUDE.md / AGENTS.md |
| Skills | Multi-step workflow expertise (steps, templates, quality bar) | SKILL.md |
| Hooks | Deterministic, non-negotiable enforcement (formatters, build gates) | CI config, pre-commit |
| Subagents | A specialized lens that should activate automatically on relevant diffs (security, accessibility, perf) | Review-skill variants from Submodule 1 |
| Tests and evals | A behavioral contract that prevents the exact regression from recurring | Test suite (see Submodule 3) |

*(Source: [Compound Engineering pattern](https://aipatternbook.com/compound-engineering))* A vague style preference belongs in an instruction file; a security gap that must never ship belongs in a hook or a test, not a suggestion in a markdown file someone might skim.

---

### 4. The rule that keeps this disciplined: wait for the third occurrence

The single biggest failure mode in this practice is over-codifying from one data point — turning every one-off review comment into a permanent rule bloats the instruction files that Submodule 1 explicitly warned against over-lengthening. The guideline worth adopting explicitly: **don't codify on the first occurrence.** Wait until the same class of feedback shows up a third time before it earns a permanent line in a standards file. The first two occurrences might be genuinely situational; the third is a pattern.

---

### 5. A worked example

A two-engineer team shipping an AI email assistant found, through repeated review cycles, that the agent kept building new form components instead of reusing existing ones. After the pattern recurred, one line went into the instruction file: reuse existing form components before creating new ones. Separately, a database migration shipped without an `IF NOT EXISTS` guard — another rule, added the same way. Over six months this team accumulated roughly sixty such rules. The reported effect: the agent stopped reaching for fresh components or unguarded migrations, and feature velocity kept climbing weekly instead of plateauing. *(Source: [Compound Engineering — Encyclopedia of Agentic Coding Patterns](https://aipatternbook.com/compound-engineering))*

---

### 6. The companion discipline: Garbage Collection

Compounding rules without pruning them is how a standards file becomes a liability instead of an asset — contradictory rules accumulate, skills go stale as the codebase evolves, hooks block requirements nobody remembers the reason for. Treat rule pruning as a scheduled review, not a someday task: periodically re-read the instruction files and skills for rules that no longer apply, contradict a newer rule, or reference code that's since been rewritten. This is the direct counterpart to the "too long to be read" anti-pattern flagged in Submodule 1 — a file that grows forever eventually gets skimmed past regardless of how it grew.

---

### 7. How this plugs into the dual-harness pattern

If Submodule 1's split holds (build in one harness, review in another), the "Compound" step is naturally where the review harness earns its keep beyond a single PR: a review agent that surfaces the *same category* of finding across multiple PRs is signaling a codification candidate, not just flagging individual diffs. Worth building into a review skill's output format directly — alongside severity, a note like "seen 3x this month" turns the review output itself into the trigger for the Compound step, rather than relying on a human to notice the pattern.

---

### Checkpoint

Look back at your last 5–10 merged PRs' review comments. Find one piece of feedback that shows up more than once. Decide which of the five surfaces it belongs on — and if it's genuinely recurred a third time, write the rule today rather than letting review number eleven re-teach it again.

---

### References

- [Compound Engineering — Encyclopedia of Agentic Coding Patterns](https://aipatternbook.com/compound-engineering)
- [10 Lessons for Agentic Coding](https://www.dbreunig.com/2026/05/04/10-lessons-for-agentic-coding.html)
- [AI Code Review Trends 2026 — Critique](https://www.critique.sh/ai-code-review-trends-2026)
- [Learnings Loop: Claude Code Skills Self-Improvement](https://www.mindstudio.ai/blog/learnings-loop-claude-code-skills-self-improvement)
