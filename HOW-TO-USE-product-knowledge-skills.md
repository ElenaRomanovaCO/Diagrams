# How to use the product knowledge skills (for humans)

This package gives Copilot a memory of your product: what was decided, what is required, what is risky, who owns what. Everything is stored as markdown files in the repo under `knowledge/`, so you can read, search and review it like code.

You talk to Copilot in plain English in **VS Code → Copilot Chat → Agent mode**.

## One-time setup

1. Unzip `product-knowledge-skills` on the machine with your repo. You can install it into the product's code repo (requirements next to code) or into a separate "product-knowledge" repo. Both work; the code repo lets `spec-gap-issues` also check the implementation.
2. Open the repo in VS Code, Copilot Chat, Agent mode.
3. Paste `COPILOT-INSTALL-PROMPT.md` (fill in `<PATH>`). Copilot creates the empty knowledge base, runs a **dry run** on a made-up standup so you can see what an ingest produces, cleans it up, and then asks for your first real transcript.

## The two folders to know

- `knowledge/raw/` — original sources, saved once and never edited: transcripts, interview answers, documents.
- `knowledge/wiki/` — what Copilot compiled from them: one page per feature, plus lists of decisions, requirements, risks, open questions, action items, people (role only), a glossary, weekly digests. `index.md` is the table of contents; `log.md` records everything that happened.

Rule that keeps it honest: any number, date, quote or name on a wiki page must exist word-for-word in a raw file. "Lint the wiki" checks this.

## What each skill is for, in one line

| You want to... | Say something like... | Skill |
|---|---|---|
| Save a meeting and pull out what matters | "ingest this transcript" (paste it, or give the file) | transcript-ingest |
| Save any other source, or ask what you know | "add this PDF to the wiki" / "what do we know about exports?" / "lint the wiki" | karpathy-llm-wiki |
| See the week: shipped, blocked, slipping, recurring | "standup digest for this week" | standup-digest |
| Justify an initiative to the business | "write the BRD for self-serve onboarding" | brd |
| Define what a feature does | "write the PRD for CSV export" | prd |
| Get backlog-ready stories with acceptance criteria | "stories for CSV export" | stories |
| Check the backlog matches the PRD; create missing issues | "sync issues with the PRD" | spec-gap-issues |

## Typical flows

**After every meeting (two minutes)**

Paste the transcript and say "ingest this". Copilot saves it, updates the wiki, and shows a short digest: decisions, new requirements (with ids like `REQ-export-03`), risks, open questions with suggested owners, action items. Glance at it; if something is wrong, say so and it fixes the wiki. If a term was used two ways, it asks which one is right.

**Friday**

"Standup digest." You get: what was completed, what is blocked and since when, promises that slipped, topics that keep coming up (usually a missing decision), and work happening that no requirement covers.

**Starting an initiative**

"Write the BRD for <name>." If the wiki already has enough, it writes it straight away, citing the meetings. If not, it asks a few numbered questions; your answers are saved as a source so the BRD is still traceable. Review scope and metrics first; that is where BRDs go wrong.

**Defining a feature**

"Write the PRD for <feature>." Same idea: grounded in the wiki and the BRD, requirements get stable ids (`FR-`, `NFR-`), user stories get Given/When/Then. Review user stories and non-goals first. Then "stories for <feature>" and, when you are happy, "sync issues with the PRD" — it shows a table of what is missing and creates issues only for the rows you approve.

**Any time**

"What do we know about X?" — answered from the wiki with links to the pages. "Lint the wiki" — finds broken links, unverifiable numbers, contradictions.

## Chained or handpicked?

Both. Each skill works alone: you can write a PRD without a BRD, or ingest transcripts for months without ever writing a document. The chain transcript → digest → BRD → PRD → stories → issues is the suggested order, and Copilot offers the next step; you decide.

## Traceability

Ids follow the work end to end: `REQ-` (wiki) → `BR-` (BRD) → `FR-`/`NFR-` (PRD) → `ST-` (stories) → issue number. Pick any ticket and you can walk back to the meeting where it was said. Ids are never renumbered; withdrawn requirements are marked, not deleted.

## Working with the SDLC package

If both packages are in the same repo: glossary terms from meetings get proposed for `CONTEXT.md`, important decisions get proposed as ADRs, and `to-tickets` can slice a PRD into engineering tickets. If only this package is installed, those mentions are simply ignored.

## Good habits

- Ingest promptly; a transcript ingested the same day gets the right date and context.
- Answer the open questions the digest raises; unanswered questions are what turn into rework.
- Review generated documents as drafts. Nothing is committed until you commit it.
- Keep people pages to role and ownership. The skills are told not to record anything personal.
