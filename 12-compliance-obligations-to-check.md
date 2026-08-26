# Module: AI-Integrated SDLC
## Submodule 12 — Compliance Obligations to Check

*"Generated code announces nothing. It arrives in your editor with no manifest entry, no version, and no declared license."*

---

### Who this is for

This one is written to speak directly to security, legal-adjacent, and management — the audience that has to answer "are we exposed?" — while giving engineers the exact things to check before code merges. Product should read the data-governance section: what gets typed into a prompt is a compliance decision, not just a productivity one.

---

### Learning objectives

- Apply the EU AI Act's engineering-relevant obligations against the actual 2026–2028 deadline timeline
- Know why AI-generated code creates a license and IP exposure that standard SBOM tooling doesn't catch
- Apply concrete CI/CD gates that catch license and provenance issues before merge, not after release
- Classify what should never be sent to a hosted AI coding tool, and when a DPA is mandatory
- Treat compliance evidence as a byproduct of normal delivery, not a separate retrospective audit

---

### 1. The EU AI Act timeline that's already live, not hypothetical

Several obligations are already in force, not upcoming: the AI literacy duty and prohibited-practices rules (Article 4/5) took effect February 2, 2025, and transparency rules (Article 50) are enforced as of August 2, 2026 — meaning disclosure of AI interaction and machine-readable marking of AI-generated content are current requirements, not 2027 planning items. Machine-readable marking for existing generative systems has a grace window ending December 2, 2026. High-risk regimes are deferred further out — December 2, 2027 for standalone systems, August 2, 2028 for embedded ones — which gives more runway, but not zero urgency, since documentation and risk-registry practices take time to stand up. *(Source: [Codacy — The Engineering Manager's EU AI Act Compliance Checklist](https://blog.codacy.com/the-engineering-managers-eu-ai-act-compliance-checklist-2026))*

The seven-step engineering checklist worth adopting directly: maintain a version-controlled inventory of AI systems/models with a documented risk-tier classification; run role-specific AI literacy sessions with dated records; disclose AI interaction at first user contact and mark AI-generated content; for anything high-risk, keep a living risk register with a named human oversight owner and override-and-stop controls; record whether you're a provider or integrator for any general-purpose model you use; pin model and prompt versions under version control and extend incident response to cover AI-specific failure modes; and store ADR-style decision records linking literacy, transparency, and risk-classification evidence together. The principle underneath all seven: enforce at the point of change — PRs and CI/CD — so evidence is a byproduct of normal delivery instead of a scramble before an audit.

---

### 2. Why AI-generated code is an IP and license blind spot

A declared dependency shows up in a manifest with a name, version, and license a scanner can check. Generated code doesn't — it lands in the editor as plain text with none of that provenance, and if a model reproduces licensed code (especially copyleft, like GPL, which requires source disclosure on distribution), the enterprise can inherit that obligation without anyone noticing it happened. A standard SBOM doesn't close this gap either: it records what you assembled from known sources, with no field for code that was generated rather than sourced. And once shipped, this isn't fixable retroactively — "a licensing defect is a legal condition attached to your software, and you cannot scan your way out of one you have already shipped." *(Source: [The IP Problem Hiding in AI-Generated Code](https://www.cloudapper.ai/enterprise-ai/ai-generated-code-open-source-license-risk-enterprise/))* The mitigation has to happen during development: configure coding assistants to flag or block suggestions matching public repositories, and run license-aware scanning against your own first-party source — not only your declared dependencies.

---

### 3. Concrete CI/CD gates that actually catch this before merge

Four gates, each cheap relative to the exposure they prevent: **dependency + snippet scanning** (a tool like FOSSA runs both dependency-based license scanning and snippet matching against a corpus of known open-source code, adding roughly 3–6 minutes to CI, catching verbatim and near-verbatim reproductions including from AI output); **local structural scanning** (ScanCode run locally, failing the build if GPL/LGPL/AGPL/EUPL/CDDL licenses appear in non-test source files); **structural pattern matching** (a tool like ast-grep catching reproduced algorithm structures that textual matching alone would miss); and an **SBOM validation gate** that specifically blocks a main-branch release when it contains AI-generated components with no license review recorded. A practical escalation rule worth adopting: any PR where AI-generated commits exceed roughly 40% of the diff and targets main gets an automatic `legal-review-required` label that branch protection won't allow merging past until a reviewer with the authority to do so removes it. *(Source: [AI-Generated Code and Open Source License Compliance](https://www.systemshardening.com/articles/cicd/ai-code-license-compliance/))* Enforcing `Co-authored-by` trailers via a pre-commit hook makes AI-generated code traceable after the fact, which is what turns "we think this was AI-assisted" into an actual, checkable record.

---

### 4. What never goes into a hosted AI tool, and when a DPA is mandatory

Absolute categories to keep out of any prompt or context window, hosted or not: hardcoded credentials and secrets (even expired ones — they reveal key format and naming conventions an attacker can use), customer personal data embedded in test fixtures or logs, code covered by an NDA or a genuine trade secret, and cryptographic private material. A quick, real habit worth instituting: scan a snippet for `key`, `secret`, `password`, `token`, `credential`, `private` before it's ever pasted into a chat or agent context.

Tool tier matters directly here: GitHub Copilot Business/Enterprise and Cursor with telemetry disabled don't train on submitted code; individual-tier plans often do unless a person actively opts out. A Data Processing Agreement is mandatory the moment code can touch EU personal data, customer records, employee data, or user activity logs — and an individual-tier tool is simply not a compliant path for that category of code, regardless of how convenient it is. *(Source: [AI Policy Desk — AI Coding Tools Governance Policy 2026](https://www.aipolicydesk.com/blog/ai-coding-tools-governance-policy-github-copilot-cursor-2026))*

---

### 5. Where this connects

The security-guardrails category in Submodule 4's AGENTS.md template is the natural home for the "never send this" list — enforced structurally rather than relying on every engineer remembering it. Submodule 1's dual-harness pattern gets a compliance rationale here too: human code review of AI-generated output is explicitly named as a required control, not an optional nicety, before anything reaches production. And a compliance gap discovered a third time — the same category of secret leaking into a prompt, say — is exactly a Submodule 2 Compound moment: it belongs in a hook or a scanning rule, not a reminder in Slack.

---

### Checkpoint

Pick one AI coding tool currently in use on your team. Check its actual tier and training settings — not what you assume they are — and check whether a DPA is in place if any code touching customer or personal data has ever gone through it. Separately, run a license scan against one recent AI-assisted PR and see whether anything would have tripped the gates described above.

---

### References

- [Codacy — The Engineering Manager's EU AI Act Compliance Checklist (2026)](https://blog.codacy.com/the-engineering-managers-eu-ai-act-compliance-checklist-2026)
- [The IP Problem Hiding in AI-Generated Code](https://www.cloudapper.ai/enterprise-ai/ai-generated-code-open-source-license-risk-enterprise/)
- [AI-Generated Code and Open Source License Compliance: The Copilot Copyright Problem](https://www.systemshardening.com/articles/cicd/ai-code-license-compliance/)
- [AI Policy Desk — AI Coding Tools Governance Policy 2026](https://www.aipolicydesk.com/blog/ai-coding-tools-governance-policy-github-copilot-cursor-2026)
- [Augment Code — The 2026 EU AI Act and AI-Generated Code](https://www.augmentcode.com/guides/eu-ai-act-2026)
