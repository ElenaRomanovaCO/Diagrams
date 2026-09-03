# Prompt: implement a medium feature with the SDLC skills

Fill in the angle-bracket parts, then paste into Copilot Chat (Agent mode) with the repo open. Copilot will stop at the checkpoints and wait for you.

---

I want to implement a medium-sized feature in this existing app using the SDLC skills in `.github/skills/`. Follow the steps below in order. At every **CHECKPOINT** stop, show me the result, and wait for my reply before continuing. Do not commit or push unless I say so.

**The feature:** ingest a JSON file (`<describe the file: where it comes from, rough shape, how often>`), parse it, store it in `<database / table(s)>`, show the resulting values in the linked fields on `<screen(s) / component(s)>`, and make them available to `<downstream process(es)>`.

**Constraints:** `<anything fixed: must be idempotent on re-import, must not change existing table X, must use the existing upload endpoint, etc. — or "none beyond repo conventions">`

## Step 1 — Context (skill: `zoom-out`)

Use the `zoom-out` skill on: the data model and repository/ORM code for `<table(s)>`, the UI screen(s) `<screen(s)>`, and the downstream code `<process(es)>`. Read `CONTEXT.md`, relevant ADRs and `docs/codebase/` if present. Produce one context brief covering inbound callers, outbound dependencies, data shapes, tests and how they run, delivery/migrations, and blast radius. Do not propose a design yet.

**CHECKPOINT 1:** show me the brief.

## Step 2 — Scope (skill: `grill-me`)

Use the `grill-me` skill. Ask the whole frontier in numbered rounds with your recommended answer for each. Cover at least: JSON-to-schema mapping and any fields with no home; validation and what happens to bad, missing or duplicate records; idempotency and re-import of the same file; where the file enters the system (upload, path, schedule, API); how downstream consumes the data and whether it needs a signal or just the rows; migration and backfill; the smallest change that satisfies this and what we are deliberately not building. Look up facts in the repo yourself; ask me only for decisions. Keep the design minimal.

**CHECKPOINT 2 (per round):** wait for my answers. When the frontier is empty, show the numbered list of decisions and wait for my confirmation.

## Step 3 — Plan (skill: `writing-plans`)

Use the `writing-plans` skill to write `docs/plans/<date>-json-ingestion.md` from the confirmed decisions. Order tasks: parser and its tests → schema migration → write path (repository/service) → UI fields → downstream hook → end-to-end check. Each task lists exact files, interfaces consumed/produced, failing test first, minimal implementation, verification command with expected output, commit. No placeholders. Run the plan's self-review (spec coverage, placeholder scan, type consistency).

**CHECKPOINT 3:** show me the plan summary (task list with files) and wait.

## Step 4 — Implement (skills: `react-best-practices`, `composition-patterns` when touching UI; `verification-before-completion` throughout)

Implement the plan task by task. Follow repo conventions over general best practice; make surgical changes only. After each task run its verification command and show me the actual output; do not say a task is done without it. If a task reveals the plan was wrong, stop and tell me instead of improvising.

**CHECKPOINT 4:** after each task, a one-line status with the verification output, then continue unless I stop you. At the end, run the full test suite and build and show the results.

## Step 5 — Review (skill: `code-review`)

Use the `code-review` skill on the diff since `<main>`: Standards axis (repo conventions, smell baseline) and Spec axis against the decisions from Step 2 and the plan. For UI changes also run the `web-design-guidelines` skill on the changed components. Report both axes separately.

**CHECKPOINT 5:** show me the review. Fix only what I approve.

## Step 6 — Wrap up (skill: `retro`)

Use the `retro` skill: list anything I corrected, wrong assumptions, conventions discovered, and slow spots, and append them to `docs/agents/LESSONS.md`. Then give me a PR title and description (problem, what changed, how verified, out of scope) that I can paste.

**CHECKPOINT 6:** show the lessons and the PR text. Stop there; I will commit and open the PR.
