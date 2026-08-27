Write a standalone .md training submodule on a technical/professional topic that reads as one system across a growing set of files — researched, sourced, audience-aware, and structured to convert cleanly to slides later. Use when asked to create training content, a training module/submodule, course content, an enablement doc, or a learning module as a markdown file (not a live interactive lesson, not a slide deck file itself).

Static Training Content Writer

A methodology for producing single-file, static (.md) training content — one file per topic/submodule — of consistent, high quality across a growing set. Adapted from the pedagogical shape of interactive multi-session teaching skills (e.g. the "teach" pattern: mission → sources → lesson → feedback loop), translated for output that is written once and read many times rather than delivered turn-by-turn.

Use this skill whenever asked to build training/enablement/course content as markdown, especially when the request implies a set of related topics (a module with submodules, a curriculum, a series) that should feel like one coherent body of work rather than independently-written documents.

Before writing anything: lock four parameters

Do not start drafting until these are known — ask if they're genuinely ambiguous, infer confidently and state the assumption if the session is unattended:

Audience — who reads this, and what do they already know? A mixed audience (e.g. engineers + management + a specific function like security or product) needs each submodule to open with who should focus where, not a single generic tone.
Depth per unit — a target word count and section count range (this skill's default: 900–1,400 words, 8–12 headed sections — enough for one worked example and one checkpoint without becoming a paper). Confirm before the first draft; hold it constant across the set.
Visual policy — tables/comparisons only (no diagrams), inline diagrams (e.g. Mermaid), or placeholder callouts for a design team. Pick one and apply it consistently; don't mix policies across files in the same set.
What "current" means — if the topic is fast-moving (a technology, a practice, a tool landscape), confirm that "latest patterns" research is in scope, not just foundational explanation.
The four-step loop per topic
1. Research before drafting — every claim needs a real source

Search for the topic's current state before writing a word of content. A "latest pattern" or "2026 development" claim with no traceable source is not usable — either find where it's actually documented (a vendor doc, a named tool's own page, a dated blog post, a benchmark) or don't include the claim. Prefer sources that are: named and dated, specific rather than a listicle summary, and — where possible — the primary source (the tool's own docs) over a secondary summary of it. Do 2–4 targeted searches per topic; fetch the 2–4 most substantive results rather than skimming ten shallow ones. Concrete, quotable mechanics (a workflow's actual steps, a named tool's actual behavior, a real number) beat generic claims every time — "teams report faster reviews" is worthless; "cut a task from 26 tool calls to 14" is usable.

2. Draft using the fixed template

Every unit in the set uses the same skeleton, so the set reads as one course:

Title + one-line hook — a sentence that states the core tension or reframe of the topic, not a description of what the file covers.
"Who this is for" — 2–4 sentences routing different readers to different sections. Don't write one tone for an assumed-homogeneous audience if the real audience is mixed.
Learning objectives — 4–6 bullets, each a concrete, checkable capability ("apply X," "distinguish Y from Z," "know when to use A vs B") — not vague exposure claims ("understand the landscape").
Numbered sections, one idea each — this is the single most important structural rule, taken directly from the source pedagogy's "one lesson = one tightly-scoped thing." A section header should map to exactly one idea a reader could restate back. Where a comparison is genuinely useful, use a table — but don't force one in every section just to satisfy a formatting habit; a table with no real comparative content is worse than none.
A closing checkpoint, not a summary — end on a question or task that forces application ("pull up your last 10 PRs and check X," not "in summary, X matters"). This is the direct descendant of the source pedagogy's feedback-loop principle: a lesson closes by requiring the learner to do something, not just recall something.
References — every named source, linked, matching what was actually fetched during research. No source, no claim.
3. Cross-link deliberately as the set grows

Once more than one unit exists, each new one should reference at least one earlier unit by name where a real connection exists (a shared vocabulary term, a pattern that recurs, a workflow stage that's genuinely upstream/downstream). Don't force a connection that isn't real. The goal is that by the last unit in a set, a reader can see the whole thing as one system with recurring threads — not a stack of unrelated documents that happen to share a header format.

4. Verify before delivering

Before sending each file, check: word count against the agreed target (a simple wc -w); every "latest/current/2026-style" claim traces to a link in the References section; the "who this is for" framing actually reflects the audience decided in setup; the checkpoint is an application task, not a recap; and — if a visual policy was set — that it was followed consistently with prior units in the set.

Explicit anti-patterns

Don't write a generic industry-trends essay with no concrete mechanics — a reader should come away able to do something, not just describe a landscape. Don't pad a section to hit a word count with restated content — a unit that naturally runs shorter than the target is better than one padded to match it. Don't force a table, diagram, or checklist into a section where the content isn't actually comparative or sequential — structure should follow the content, not the reverse. Don't write every unit's tone identically if the audience decision calls for different framing per unit (e.g., a security-heavy topic should read differently than a product-process topic, even within the same set). Don't let "current/latest" claims go unsourced — this is the single most common way training content quietly goes stale or wrong.

Delivering the set

Deliver each unit as its own file as soon as it's done — don't batch the whole set until the end; a person reviewing as you go can redirect earlier and cheaper. Name files so their order and topic are obvious from the filename alone (e.g. 01-topic-name.md, 02-next-topic.md). After a first unit or two, it's worth explicitly checking with whoever commissioned the set whether the template, depth, and tone are landing before continuing through the rest — c
