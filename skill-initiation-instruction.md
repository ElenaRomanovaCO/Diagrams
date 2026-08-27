# Skill Initiation Instructions

**Purpose:** Hand this file, together with a skill's `SKILL.md` content (or a path/URL to it), directly to an agent session — Claude Code or GitHub Copilot CLI — and have that agent perform the entire installation itself: locating the right directory, creating folders, naming the file correctly, fixing malformed frontmatter, and verifying the skill actually loads. Nothing here is written for a human to execute manually; every instruction below is addressed to the agent.

This works for **any** skill, not just one specific one — the agent should read the skill's own frontmatter to determine its name rather than assume one.

---

## Instructions for a Claude Code agent

You have been given a skill to install — either pasted inline as `SKILL.md` content, or as a path/URL to a file (which may currently have the wrong filename, e.g. `<something>-skill.md` instead of `SKILL.md`). Do the following without asking the user to do any of the file manipulation themselves:

1. **Read the skill content and extract its identity.** Find the YAML frontmatter between `---` markers at the top of the file. Locate the `name` field. If there is no `name` field, derive one from the `description` field or the source filename, using lowercase-with-hyphens. If there is no `description` field, do not proceed — a skill without a `description` cannot be auto-triggered, so add a clear, condition-based description yourself, following the pattern "Use when the user asks to [specific task]," and confirm your addition with the user before continuing.

2. **Determine install scope.** Default to **project scope** (`.claude/skills/<name>/SKILL.md` at the repository root) if you are running inside a git repository, since that makes the skill travel with the repo for anyone who clones it. Use **personal scope** (`~/.claude/skills/<name>/SKILL.md`) only if the user explicitly says they want it available across all their projects, or if you are not inside a git repository at all. If unsure which the user wants, ask this one question before proceeding — don't ask anything else.

3. **Create the correct directory structure.** Run the equivalent of:
   ```bash
   mkdir -p .claude/skills/<name>
   ```
   (or the `~/.claude/skills/<name>` personal-scope equivalent per step 2).

4. **Write the file as exactly `SKILL.md` inside that directory** — not the original filename, whatever it was. If a source file exists elsewhere in the repo under the wrong name/location, move it and remove the stray copy; don't leave a duplicate lying around at the old path.

5. **Validate the frontmatter before finishing.** Confirm the file has valid YAML between `---` markers, a `name` field matching the directory name exactly, and a non-empty `description`. Fix any mismatch yourself (e.g., if the directory is `static-training-content-writer` but the frontmatter says `name: my-skill`, correct the frontmatter to match) and tell the user what you changed and why.

6. **Verify it loads.** If you are running live in a Claude Code session, confirm the skill directory is visible in this session (Claude Code watches `.claude/skills/` for live changes without a restart, but a *brand-new top-level* skills directory that didn't exist when the session started requires a restart — tell the user to restart if that's the case). Then do one of:
   - Invoke it directly: `/<name>`
   - Or state a request matching its description and confirm it's the one that responds.

7. **Report back concisely**: the final file path, the invocation command (`/<name>`), and whether the skill is project- or personal-scoped. If you made any correction to the frontmatter or filename, name exactly what you changed.

8. **If this repo will also be used with GitHub Copilot**, mention to the user (don't do it unprompted) that the same `.claude/skills/<name>/SKILL.md` path is one of Copilot CLI's watched locations too, so no duplicate copy is needed unless they want one under `.github/skills/<name>/` as well.

---

## Instructions for a GitHub Copilot CLI agent

You have been given a skill to install — either pasted inline as `SKILL.md` content, or as a path/URL to a file (which may currently have the wrong filename or be sitting at the wrong location, e.g. a flat `<something>-skill.md` at a repo root). Do the following without asking the user to do any of the file manipulation themselves:

1. **Read the skill content and extract its identity.** Find the YAML frontmatter between `---` markers. Locate `name` (required) and `description` (required — this is the auto-detection trigger). If either is missing or malformed, fix it yourself: derive `name` from the intended skill folder name (lowercase, hyphen-separated), and write `description` as a condition ("Use when the user asks to..."), not a label. Tell the user what you added or corrected.

2. **Determine install scope and path.** Default to **project scope** if inside a git repository. Copilot CLI watches multiple project-level directories — prefer `.github/skills/<name>/SKILL.md`, but if the repo already has (or will also use) `.claude/skills/<name>/SKILL.md` for Claude Code, that same path is *also* watched by Copilot CLI — don't create a second copy in that case; one file at `.claude/skills/<name>/SKILL.md` satisfies both tools. Use `~/.copilot/skills/<name>/` only for personal, cross-project scope, or if not inside a git repository.

3. **Create the directory and place the file** as exactly `SKILL.md`:
   ```bash
   mkdir -p .github/skills/<name>
   ```
   (adjust path per step 2). Remove any stray copy left at an old filename/location.

4. **Reload and verify:**
   ```
   /skills reload
   /skills list
   ```
   Confirm `<name>` appears in the list. Then run:
   ```
   /skills info <name>
   ```
   and confirm the description matches what you expect.

5. **Test invocation** — either state a request matching the skill's description and confirm it auto-triggers, or invoke explicitly by naming the skill in your prompt (e.g. "Use the /<name> skill to...").

6. **Model check, only if the user asked for a specific model (e.g. Claude Opus):** run `/model` and check whether the requested model appears in the list. If it does, select it. If it does not appear, or selecting it doesn't visibly change the active model, tell the user plainly that this model isn't currently reliable inside Copilot CLI's picker, and that the Agents tab on github.com is the more consistent surface for selecting Claude Opus specifically — do not silently proceed on a different model without saying so.

7. **Report back concisely**: the final file path, confirmation it appears in `/skills list`, the invocation phrasing that works, and the active model if one was requested. Name any correction you made to the original file.

---

## Notes that apply to either agent

- Never leave two divergent copies of the same skill's content in the repo (e.g., one at the original wrong filename and one at the corrected path) — the original should be moved, not copied, unless the user asks to keep a mirror for the other tool at a genuinely different watched path.
- If the skill file's frontmatter is ambiguous enough that you're guessing at the `name` or `description`, say so explicitly rather than silently inventing one — a wrong `description` means the skill will trigger on the wrong prompts or never trigger at all.
- Do the file operations yourself. The point of these instructions is that the person handing you the skill shouldn't need to know a `.claude/skills/` path exists — you locate it, create it, and confirm it works.
