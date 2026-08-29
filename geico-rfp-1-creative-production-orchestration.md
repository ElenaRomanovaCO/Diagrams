# Request for Proposal (Example/Illustrative)
## Marketing Creative Production & Workflow Orchestration Platform

**Document status:** This is an EXAMPLE RFP, written for internal demo-preparation purposes. It is not a real GEICO document. GEICO has not issued a public RFP on this topic; this draft is constructed by projecting a plausible RFP from publicly available evidence about GEICO's marketing organization (see "Grounding & Rationale" section at the end of each requirement, and the companion file `geico-research-subset-top2-priorities.md` for full sourcing). Do not present this to GEICO as an actual document they produced.

**Issuing organization (illustrative):** GEICO Marketing Operations
**RFP focus area:** Problem #1 of 5 identified in prior research — creative production volume outrunning current process capacity
**Prepared:** 2026-08-29

---

## 1. Background and Context

GEICO's marketing organization produced its largest creative slate on record in 2025: 8 campaigns spanning 7 lines of business (auto, home, boat, motorcycle, RV, renters, and two commercial-auto segments), comprising approximately 60 video/streaming/OLV spots, 54 social ads, 50 audio executions, and roughly 600 supporting mid- and lower-funnel assets — produced primarily through a single long-tenured creative agency of record (The Martin Agency, partner since the late 1990s) alongside a separate media agency of record (IPG Mediabrands, since 2023).

GEICO's own marketing leadership has described this volume, in public statements, as taking "incredible effort both internally and externally." [Source: LBBOnline, July 29, 2025, https://lbbonline.com/news/Behind-GEICO-Largest-Creative-Slate-Gecko; MarketingDive, July 29, 2025, https://www.marketingdive.com/news/geico-stretches-marketing-reach-with-8-campaigns-across-7-offerings/754128/]

GEICO installed a new Chief Marketing Officer (Arianna Orpello, effective January 5, 2026), following a CMO vacancy of roughly one year. [Source: GEICO press release, October 7, 2025, https://www.geico.com/about/pressreleases/2025/20251007/] New marketing leadership is evaluating how the organization scales creative output across an expanding number of product lines and campaign cycles without a proportional increase in headcount or review bottlenecks.

## 2. Purpose and Objectives

GEICO Marketing Operations seeks proposals from qualified vendors for a marketing workflow orchestration and creative production management platform. The objective is to:

1. Provide a single system of record for managing concurrent, multi-line creative campaigns (currently spanning at least 7 product lines simultaneously).
2. Reduce the manual coordination burden currently placed on marketing, brand, and creative leadership when managing high-volume campaign cycles.
3. Improve visibility into asset status, version history, and review-stage bottlenecks across internal teams and external agency partners (creative AOR and media AOR).
4. Support scaling creative output in future cycles without a proportional increase in process overhead or creative-team headcount.

## 3. Scope of Work

### 3.1 Core capabilities required
- Centralized campaign and asset intake, covering multiple concurrent product lines and campaign types (brand, product-specific, seasonal/promotional).
- Workflow templating by campaign type, with configurable review stages (creative, brand, legal/compliance — see companion RFP on compliance for detailed requirements).
- Real-time status visibility across internal marketing teams and external agency collaborators (minimum: one creative agency of record, one media agency of record).
- Version control and asset history for creative deliverables across channels (TV/streaming, OLV, social, audio, out-of-home, digital).
- Reporting on cycle time by campaign, by asset type, and by review stage, to identify recurring bottlenecks.
- Integration capability with existing marketing execution tools. Note: public evidence suggests GEICO's marketing/creative team currently uses Wrike operationally (per two independent 2025 job postings; see companion research file for detail) — vendor should describe integration or migration approach for a Wrike-based environment, and should not assume an Adobe Workfront environment, which no public evidence supports.
- Support for high-volume asset production: recent GEICO campaigns have run into the hundreds of individual assets (approx. 600 supporting assets in the 2025 cycle) across a compressed production window.

### 3.2 Out of scope (for this RFP)
- Media buying/placement (handled by GEICO's existing media agency of record relationship).
- Compliance rules-engine and regulatory approval logging — covered under the companion RFP, "Marketing Compliance Approval & Audit Trail Platform," where legal/compliance-specific requirements are detailed in full.

## 4. Functional Requirements

| # | Requirement | Priority |
|---|---|---|
| F1 | Support at least 8 concurrent campaigns across 7+ product lines without workflow conflicts | Must-have |
| F2 | Configurable multi-stage review workflows (creative → brand → legal/compliance → final) | Must-have |
| F3 | External agency collaborator access with permission controls (no full internal-system access required) | Must-have |
| F4 | Asset-level version history and rollback | Must-have |
| F5 | Dashboard-level visibility for marketing leadership showing campaign status across all active lines of business | Must-have |
| F6 | Cycle-time analytics by stage, campaign, and asset type | Should-have |
| F7 | API or native integration path with Wrike (or comparable current tooling, to be confirmed with vendor during discovery) | Must-have |
| F8 | Support for seasonal/peak production windows without performance degradation | Should-have |
| F9 | Template library for recurring campaign types to reduce campaign setup time | Should-have |
| F10 | Mobile or lightweight access for stakeholder approvals outside the core creative team | Nice-to-have |

## 5. Evaluation Criteria

| Criterion | Weight |
|---|---|
| Demonstrated ability to reduce campaign cycle time (case studies/reference data required) | 30% |
| Integration/migration approach for existing marketing tooling | 20% |
| Scalability across multiple concurrent product lines | 20% |
| Total cost of ownership over 3 years | 15% |
| Vendor implementation timeline and support model | 10% |
| References from comparable-scale enterprise marketing organizations | 5% |

## 6. Grounding & Rationale (why each requirement exists)

- **Why "concurrent multi-line campaigns" is a Must-have (F1):** GEICO ran 8 campaigns across 7 lines of business simultaneously in 2025 — this is now the demonstrated ceiling of current output, not a hypothetical future state. [LBBOnline, MarketingDive, July 29, 2025]
- **Why external agency access matters (F3):** GEICO's structure is a two-agency model (creative AOR: Martin Agency; media AOR: IPG Mediabrands since Feb 2023), not an in-house-only or fully agency-outsourced model — any platform must manage hand-offs across this specific structure, not assume either extreme. [MediaPost, Feb 23, 2023, https://www.mediapost.com/publications/article/382813/ipgs-mediabrands-wins-14-billion-geico-media-re.html]
- **Why Wrike integration is flagged as Must-have, not Workfront (F7):** Two independent, dated GEICO job postings (Graphic Designer II, cached July 2025; Manager, Creative Studio, cached November 2025) name Wrike as an operational tool ("provides regular project status updates via Wrike"). No public source — case study, press release, or conference session — connects GEICO to Adobe Workfront. This is evidence, not certainty, but it should shape vendor discovery questions, not be assumed away.
- **Why cycle-time reduction carries the highest evaluation weight (30%):** This is the single most quantifiable, defensible ROI argument available (see Section 7 below) and it's the dimension GEICO's own team has already flagged as painful in their own words.

## 7. Illustrative ROI Benchmarks (industry-wide, not GEICO-specific)

These are third-party, publicly available vendor-commissioned studies — cited for realistic ROI framing, not as GEICO-confirmed figures:

- **Wrike** (the tool GEICO's marketing/creative team most plausibly uses today): a Forrester Total Economic Impact™ study (commissioned by Wrike, published August 23, 2023) found a composite enterprise customer achieved **396% ROI over 3 years**, **$9.78M net present value**, **payback within 6 months**, a **90% reduction in low-value initiatives**, and consolidation/retirement of 300 seats in legacy project-management tools. [Source: https://www.wrike.com/blog/forrester-tei-study-2023/ and https://www.wrike.com/forrester-tei-study-2023/]
- **Adobe Workfront** (comparator, in case GEICO's tooling differs from current public evidence): a separate Forrester TEI study found **285% ROI over 3 years**, **$22M+ in productivity savings**, and **payback in under 3 months** for a 20,000-person composite B2C enterprise. [Source: https://business.adobe.com/blog/the-latest/forrester-how-enterprises-hit-285-roi]

**Caveat:** Both studies are vendor-commissioned (Forrester TEI methodology, funded by the vendor being studied) — treat the specific percentages as vendor-favorable illustrations of category-level ROI potential, not independent, GEICO-specific projections. Use them to frame realistic ranges in vendor conversations, not as guaranteed outcomes.

## 8. Submission Requirements (illustrative)

Respondents should provide:
1. Executive summary and understanding of GEICO's stated challenge (concurrent multi-line campaign management at scale).
2. Technical approach and integration plan, explicitly addressing compatibility with a Wrike-based (or to-be-confirmed) existing environment.
3. Case studies from enterprise clients managing 5+ concurrent product lines or campaign types.
4. Pricing model (subscription/seat-based/usage-based) with 3-year TCO projection.
5. Implementation timeline and change-management approach for creative/brand teams and external agency partners.
6. Named references, ideally from regulated or multi-line consumer brands.

## 9. Indicative Timeline (illustrative)

| Milestone | Timing |
|---|---|
| RFP issued | Week 0 |
| Vendor questions due | Week 2 |
| Proposals due | Week 5 |
| Vendor demos/shortlist | Weeks 6–8 |
| Award decision | Week 10 |
| Implementation kickoff | Week 12 |

---

*Companion documents: `geico-rfp-2-marketing-efficiency-expense-ratio.md` (cost/ROI-focused RFP) and `geico-research-subset-top2-priorities.md` (full sourced research backing both RFPs).*
