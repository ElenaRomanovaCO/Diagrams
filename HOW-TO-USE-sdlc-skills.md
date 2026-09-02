# How to use the SDLC skills (for humans)

You talk to Copilot in plain English. Copilot picks the right skill from what you say. You never have to type a skill's name, though you can ("use the grill-me skill") when you want to be sure.

Everything below happens in **VS Code → Copilot Chat → Agent mode**, with your repo open.

## One-time setup

1. Unzip `copilot-sdlc-skills` anywhere on the machine that has your repo.
2. Open the repo in VS Code, open Copilot Chat, switch to Agent mode.
3. Paste the contents of `COPILOT-INSTALL-PROMPT.md` (fill in `<PATH>`). Copilot will walk through twelve steps and ask you a few yes/no questions (replace an existing file? create labels?). Answer as it goes.
4. When it finishes, it will have documented your codebase in `docs/codebase/` and asked you some `[ASK USER]` questions. Answer them; that is the agent learning your project.

That is it. The skills now live in `.github/skills/` in your repo and travel with it, so teammates get them by pulling.

## What each skill is for, in one line

| You want to... | Say something like... | Skill that answers |
|---|---|---|
| Understand a repo you've never seen | "onboard me to this repo" | acquire-codebase-knowledge |
| Make the repo friendlier for AI agents | "make this repo AI-ready" | ai-ready |
| See what a piece of code touches before changing it | "zoom out on the checkout module" | zoom-out |
| Think a change through before coding | "grill me on adding CSV export" | grill-me |
| Same, but for a big feature, and write the decisions down | "grill me with docs on the new billing flow" | grill-with-docs |
| Turn the discussion into a spec issue | "write this up as a spec" | to-spec |
| Turn a spec into small, independent issues | "break this into tickets" | to-tickets |
| Get a step-by-step implementation plan | "write a plan for issue #42" | writing-plans |
| Make sure it really works before calling it done | (automatic; you can say "verify before you say done") | verification-before-completion |
| Review a branch or PR | "review my branch since main" / "review PR #57" | code-review |
| Capture a lesson so the mistake isn't repeated | "retro" / "remember: never call the DB from components" | retro |
| Tidy up the lessons once a week | "dream" / "consolidate lessons" | dream |
| Write good React / Next.js code | (automatic when you touch React files) | react-best-practices |
| Fix a component with too many boolean props | "clean up this component's props" | composition-patterns |
| Check UI for accessibility and UX problems | "review my UI" / "check accessibility" | web-design-guidelines |
| Look at a running page for layout bugs | "check the layout on the dashboard page" | web-design-reviewer |
| Test the frontend in a real browser | "test the login flow in the browser" | webapp-testing |

## Typical days

**A small fix in existing code**

1. "Zoom out on the reports page export button." Copilot shows you a short brief: who calls it, what it depends on, how it is tested.
2. Make the change (or ask Copilot to).
3. Copilot verifies (runs tests/build) before saying done. If it says "should work", ask "verify it".
4. "Review my changes since main."
5. If Copilot did something you had to correct: "retro" and it writes the lesson down.

**A new feature in existing code**

1. "Zoom out on <area>."
2. "Grill me with docs on <feature>." Answer the numbered questions round by round. Copilot fills in facts itself and only asks you for decisions. It writes glossary terms and decision records as you go.
3. "Write this up as a spec." → a GitHub issue.
4. "Break it into tickets." Approve the breakdown, then it creates the issues with blockers.
5. For each ticket: "write a plan for #NN", then implement, verify, "review since main", "retro".

**A brand new project**

Start with "grill me with docs on <the product>", then spec, tickets, and "make this repo AI-ready" once there is a skeleton.

**Weekly hygiene (five minutes)**

- "Dream." Copilot shows which lessons recurred and where it wants to promote them (instructions, coding standards, glossary, decisions). Approve or reject each. Nothing is committed until you say so.

## Chained or handpicked?

Both. Every skill works on its own. The chains above are suggestions; Copilot offers the next step and you say yes or no, or you ask for several in one sentence ("grill me, then spec, then tickets"). The only step you should never skip is verification before "done".

## Files the skills create in your repo

- `CONTEXT.md` — the glossary. Short definitions, no implementation details.
- `docs/adr/` — decision records. Only for hard-to-reverse decisions.
- `docs/codebase/` — the generated map of the repo.
- `docs/plans/` — implementation plans.
- `docs/agents/LESSONS.md` — lessons log (retro writes, dream tidies).
- `docs/agents/issue-tracker.md` — how issues are read and created. Edit if you use Jira / Azure DevOps.

All plain markdown, reviewable in pull requests.

## If something doesn't trigger

Say the skill's name: "use the code-review skill on PR #57". If it still doesn't load, ask Copilot to "reload skills" or check that `.github/skills/<name>/SKILL.md` exists on your branch.

## Wave 2 (not installed yet)

TDD, systematic debugging, triage, architecture improvement, a backend conventions skill. Ask for them when the first wave feels natural.
