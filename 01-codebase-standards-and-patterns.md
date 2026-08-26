# Module: AI-Integrated SDLC
## Submodule 1 — Codebase Standards and Patterns

*"If the agent has to guess your conventions, it will guess wrong at scale."*

---

### Who this is for

Engineers get the concrete file formats and skill structures. Engineering managers and product get the "why" — this submodule is the foundation the rest of the module (especially Submodule 2, Turning Review Feedback into Standards) builds on. Security should pay close attention to the review-skill and dual-harness sections — this is where security review actually gets enforced, not just documented.

---

### Learning objectives

- Explain why plain-English context files (not wikis or onboarding docs) are now the primary way teams encode standards for AI agents
- Distinguish what CLAUDE.md, AGENTS.md, and SKILL.md each own, and write a minimal version of each
- Describe the "dual-harness" pattern — using one AI tool to build and a different one to review — and why teams are adopting it
- Identify what makes a code-review or security-review skill good versus a generic prompt

---

### 1. The standard moved from the wiki into the repo

For a decade, "coding standards" lived in a wiki page nobody read after onboarding. That's no longer where it matters most: it now has to live in a file the agent reads on every single task, because an agent has no tenure and no memory of the last standup. The unit of standardization changed from "document a human skims once" to "context a machine re-reads every session."

Three files have emerged to carry that context, and mixing up their jobs is the most common early mistake:

| File | Owns | Scope | Read by |
|---|---|---|---|
| `CLAUDE.md` | Claude Code's default project context | Single root file (with `@imports` for nesting) | Claude Code natively |
| `AGENTS.md` | Tool-agnostic project context: stack, commands, style, security rules | Plain markdown, nestable per-directory | 30+ agents — Codex, Cursor, Copilot, Devin, etc. |
| `SKILL.md` | One reusable, invokable capability (a procedure, not project facts) | Modular — one skill, one file, gated by its YAML `description` | Any agent that supports Skills, only when triggered |

*(Source: [AGENTS.md Spec 2026 guide](https://www.morphllm.com/agents-md-guide); [CLAUDE.md vs AGENTS.md vs SKILL.md](https://medium.com/data-science-collective/claude-md-vs-agents-md-vs-skill-md-which-file-owns-what-in-2026-13859378f56a))*

Practical note as of today: Claude Code doesn't natively read AGENTS.md, so the common workaround is making CLAUDE.md a one-line pointer (`@AGENTS.md`) so both the Claude-specific and cross-tool files stay in sync instead of drifting into two competing sources of truth.

---

### 2. A minimal AGENTS.md, for reference

Keep it to 20–30 lines. Longer files get skimmed less reliably, not more.

```markdown
# Project Name
Next.js 15 App Router, React 19, TypeScript, Tailwind, Drizzle ORM, Bun.

## Commands
- `bun run dev`     — dev server (port 3000)
- `bun run test`    — Vitest suite
- `bun run lint`    — ESLint

## Architecture
- /src/app/        — App Router pages
- /src/lib/        — DB client, utilities
- /src/actions/    — Server actions (mutations)

## Rules
- Mutations via server actions, never direct API routes
- All DB access through Drizzle, never raw SQL in components
- Run typecheck before every commit
- Never commit .env files or hardcoded secrets
```

The pattern generalizes regardless of stack: overview → exact commands → the 3–5 rules that differ from language defaults → security constraints. Skip anything a competent agent would already infer.

---

### 3. Skills are the new runbook

A Skill is a standing procedure the agent picks up only when it's relevant — the YAML `description` field is the trigger, and the agent only reads the rest of the file once that description matches the task at hand. That's what makes skills different from just pasting instructions into CLAUDE.md: they're modular, reusable across projects, and don't bloat the context the agent carries on unrelated work.

The two skill types every team building an AI-integrated SDLC needs first are PR review and security review — because these are the steps where "the agent kind of checked it" is not good enough.

**A good PR-review skill** (pattern seen across community and vendor skills) structures itself as:

```yaml
---
name: code-reviewer
description: Structured review for security, logic, edge cases, performance, and style. Use on any PR or diff review request.
---
```
Then the body defines: a security checklist (hardcoded secrets, missing input validation, non-parameterized queries), architecture checks (layering, repository patterns), style rules, and — critically — a fixed output format: findings grouped by file, ranked Critical / Warning / Suggestion. The fixed output format is what makes review *consistent* across 50 PRs instead of good on the first one and vague by the tenth.

**A good security-review skill or command** goes further: Claude Code's built-in `/security-review` checks for SQL injection, XSS, auth/access-control flaws, insecure data handling, and known-vulnerable dependencies, and can run automatically via a GitHub Action on every PR open, posting inline comments with the finding and a suggested fix. *(Source: [Anthropic — Automated Security Reviews](https://support.claude.com/en/articles/11932705-automated-security-reviews-in-claude-code))* The template worth copying either way: checklist → severity → inline, actionable fix — not a paragraph of prose a reviewer has to re-triage.

---

### 4. The dual-harness pattern: don't let the builder grade its own homework

A pattern that's become common practice in 2026: use one harness to write the code, a *different* one to review it. The logic is simple — a model reviewing its own output inherits its own blind spots. Splitting the harness forces a second, independently-trained perspective onto the diff, the same reason human teams don't let authors merge their own PRs.

A commonly reported split:

| Step | Harness | Why |
|---|---|---|
| Build / greenfield / multi-file refactor | Claude Code | Strong long-context retention across an extended build session |
| Ongoing review cycles / maintenance | Codex | Dedicated read-only `/review` turn; more session-to-session consistency |
| Security review specifically | Either, via a dedicated skill/command (e.g. `/security-review`), not the general chat loop | Purpose-built checklist beats an ad hoc "does this look secure?" prompt |

*(Source: [Claude Code vs Codex, 100+ hours comparison](https://composio.dev/content/claude-code-vs-openai-codex))* The advice from practitioners running both: "keep both installed" — capability differences between these tools shift release to release, so the split itself matters more than which specific tool sits on which side of it this quarter.

---

### 5. Current harness landscape, for context

Not every team needs every tool — but knowing where each one is strong keeps the standards realistic instead of aspirational.

| Harness | Type | Notable strength | Where it fits |
|---|---|---|---|
| Claude Code | Proprietary CLI/cloud | 88.6% SWE-bench Verified — top raw SWE performance | Primary build harness |
| OpenAI Codex | CLI | Dedicated read-only `/review` mode, session consistency | Review / maintenance harness |
| Cursor | IDE-integrated | Tight inline IDE loop | Day-to-day authoring inside an IDE |
| Copilot | IDE-integrated | Broad enterprise deployment, familiar UX | Baseline for orgs standardizing incrementally |
| Windsurf, Cline, Aider, OpenHands | CLI / IDE, mostly open | Varying orchestration models (single-agent, dual-agent plan+build) | Team- or task-specific fits |

*(Source: [AI Multiple — Agent Harness Benchmark](https://aimultiple.com/agent-harness))* Treat this table as a snapshot, not a commitment — benchmark leaders rotate roughly every quarter right now.

---

### 6. Common anti-patterns to name explicitly

A standards file that's too long to be read is worse than no file — teams routinely see agents skim past anything beyond ~30 lines. A skill with no fixed output format produces reviews that degrade in consistency as volume grows. And using the same harness to write and review a change quietly reintroduces the single-reviewer blind spot the dual-harness pattern exists to remove.

---

### Checkpoint

Pull up a real PR from your own repo. Using the checklist structure above (security → architecture → style → severity-ranked output), review it by hand. Then ask: which of these checks could be encoded once, in a skill, so no reviewer has to remember to run them manually again?

---

### References

- [AGENTS.md Spec Guide (2026)](https://www.morphllm.com/agents-md-guide)
- [CLAUDE.md vs AGENTS.md vs SKILL.md — file ownership](https://medium.com/data-science-collective/claude-md-vs-agents-md-vs-skill-md-which-file-owns-what-in-2026-13859378f56a)
- [Anthropic: Automated Security Reviews in Claude Code](https://support.claude.com/en/articles/11932705-automated-security-reviews-in-claude-code)
- [Best Code Review Skills for Claude Code (2026)](https://www.agensi.io/learn/best-code-review-skills-claude-code)
- [Claude Code vs Codex — 100+ hour comparison](https://composio.dev/content/claude-code-vs-openai-codex)
- [AI Multiple — Agent Harness Benchmark](https://aimultiple.com/agent-harness)
