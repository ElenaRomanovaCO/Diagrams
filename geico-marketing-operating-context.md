# Research prompt --- GEICO marketing operating context

**Purpose:** we are building a demo of a marketing-orchestration
platform for GEICO and we do not have their RFP. We need a well-grounded
picture of how their marketing organisation actually works, what hurts,
and where they are going --- so the demo shows *their* problem rather
than a generic one.

**What this is for and not for:** findings shape demo content and
framing. They do not become requirements, and nothing here may be stated
to GEICO as a fact about their organisation. Separate evidence (sourced,
dated, quoteable) from inference (your reasoning) on every point.

## Copy everything below into the research agent

You are researching **GEICO's marketing organisation** --- how it
operates, what it struggles with, and where it is heading. The output
will be used to make a software demo feel relevant to GEICO's actual
world. It will not be shown to GEICO as a claim about them.

### Ground rules

1.  **Public sources only.** Nothing behind a login or paywall.
2.  **Cite everything.** Every factual claim gets a URL and a date.
3.  **Label each finding `EVIDENCE` or `INFERENCE`.** Evidence =
    something a source actually says. Inference = your reasoning from
    it. Never blur them.
4.  **Recency matters.** Prefer the last 24 months. Flag anything older
    than 3 years as possibly stale.
5.  **Say when you find nothing.** "No public information" is a valuable
    and honest result. Do not fill gaps with plausible-sounding
    generalities --- a confident guess is worse than a blank here,
    because it will be built on.
6.  Where GEICO-specific information is genuinely unavailable, you may
    substitute **large US personal-lines insurers as a comparison
    class** --- but label it clearly as class-level, not GEICO-specific.

## 1. The marketing organisation

-   How is GEICO's marketing organised? Brand vs performance vs
    lifecycle/CRM? In-house vs agency? Which agencies of record, and
    since when?
-   Roughly how large? Any public org changes, reorganisations, or
    leadership changes in marketing in the last 2--3 years?
-   Who are the named marketing leaders (CMO and direct reports), and
    what have they said publicly about how they want marketing to work?
    Quote them.
-   Any public signal about how many external agency collaborators touch
    their work?

## 2. Marketing spend and volume --- the scale of the problem

-   GEICO's annual advertising/marketing spend, most recent figures,
    with trend.
-   Roughly how much creative do they produce? Campaign volume, channel
    count, number of concurrent campaigns, seasonal peaks?
-   How does this compare to Progressive, State Farm, Allstate?
-   *Why we care:* volume is what makes review rounds and consolidated
    feedback a real problem instead of a theoretical one.

## 3. Technology estate --- highest priority section

-   **What work-management tool does GEICO use?** Adobe Workfront,
    Wrike, Asana, monday.com, Smartsheet, Jira, something homegrown?
    Look at job postings naming the tools, vendor case studies,
    conference talks, LinkedIn skills on GEICO marketing-ops roles,
    press releases.
-   **What marketing technology do they use generally** --- Adobe
    Experience Cloud, Salesforce, Braze, Adobe Workfront/GenStudio,
    in-house platforms?
-   Any public relationship with Adobe specifically?
-   What do their marketing-operations, martech, and
    marketing-technology job postings ask for? These are the single
    richest public signal about the real estate --- list the tools with
    dates.
-   *Why we care:* our ingest currently reads Workfront exports. If they
    use something else, the demo's opening move changes.

## 4. Pain points and stated direction

-   What has GEICO said publicly about marketing efficiency, speed to
    market, creative production, review cycles, or operating-model
    change?
-   Any public commentary on AI in their marketing --- adoption,
    governance, restrictions?
-   Berkshire Hathaway context: what does its cost discipline mean for
    how GEICO buys and runs marketing technology?
-   GEICO ran a significant technology modernisation/transformation in
    recent years --- what is publicly known about its goals and where
    marketing sits in it?
-   Any public statements about agency relationships, in-housing, or
    consolidation?

## 5. Regulatory and compliance context

-   What compliance constraints govern insurance marketing in the US?
    State-by-state advertising rules, disclosure requirements, filing
    obligations.
-   What does that imply about who must approve marketing content before
    it ships --- legal, compliance, state-specific reviewers?
-   Are there public examples of insurance marketing compliance failures
    and what they cost?
-   *Why we care:* this is what makes "a named person approves, and the
    approval is recorded" a legal necessity rather than a nice-to-have.
    It may be the strongest argument in the whole demo, and it is the
    part we currently understand least.

## 6. Competitive and market position

-   GEICO's market position and recent trajectory in personal auto ---
    share, growth, profitability.
-   Recent strategic shifts affecting marketing: spend changes,
    positioning changes, the status of the gecko and long-running
    campaign assets.
-   What are Progressive/State Farm/Allstate doing in marketing
    technology that GEICO would be measured against?

## 7. The specific questions we most need answered

Answer these directly, and say plainly when the answer is unknown:

1.  **Is Adobe Workfront in GEICO's estate?** Evidence, not inference.
    If unknown, say so.
2.  **Who approves marketing creative at GEICO, and does
    compliance/legal sit in that path?**
3.  **How many review rounds does insurance marketing creative typically
    go through, at GEICO or in the industry?**
4.  **What is GEICO's stated position on AI in marketing?**
5.  **What would a realistic GEICO marketing brief contain** --- fields,
    approvers, compliance elements? Any public template or industry
    equivalent.

## Output format

``` text
## Finding
[EVIDENCE | INFERENCE] · confidence: high / medium / low
Claim: <one sentence>
Source: <URL> (published <date>)
Detail: <2–4 sentences>
Why it matters for the demo: <one sentence>
```

Then close with:

**What we now know** --- the confident picture. **What we still don't
know** --- explicitly, especially the seven questions above. **What
surprised you** --- anything contradicting the assumption that this is a
large, conventional, agency-heavy marketing organisation.

## What good looks like

-   The Workfront question answered with evidence, or clearly marked
    unanswerable.
-   Enough about the compliance approval path to make a review workflow
    that an insurance marketer would recognise as theirs.
-   Real numbers on spend and creative volume.
-   Direct quotes from GEICO leadership about how they want marketing to
    work.

**A short, honest result beats a long, padded one.** We will build on
this, so a confident guess is more damaging here than a gap.
