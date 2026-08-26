# Module: AI-Integrated SDLC
## Submodule 5 — Threat Modeling and Security Scoping

*"STRIDE was built for systems with fixed boundaries. An agent redraws its own boundaries every time it calls a new tool."*

---

### Who this is for

This one is written to speak to security directly, in depth — not a watered-down version. Engineers need the practical checklist and where it plugs into their workflow; management needs the quarterly-review and named-owner discipline; product should understand why "we added an AI feature" now triggers a scoping step, not just a security sign-off at the end.

---

### Learning objectives

- Explain the four specific ways classical STRIDE threat modeling breaks down for agentic systems
- Name the new threat categories agentic systems introduce, and one documented real-world example
- Apply the layered MAESTRO + MITRE ATLAS + NIST AI RMF approach at a practical level
- Use the eight-step threat-modeling workflow and know where AI tooling (like AWS Security Agent) fits into it
- Apply the OWASP Agentic Top 10 as a scoping checklist, with a defined quarterly review cadence

---

### 1. Why STRIDE alone isn't enough anymore

STRIDE assumes a system with relatively stable boundaries. Autonomous agents don't have that — they expand their own attack surface dynamically every time they call a new tool or write to memory. Four specific gaps show up in practice: **goal hijacking has no STRIDE category** — an agent misusing its own legitimate capabilities isn't spoofing or tampering, it's doing exactly what it was told, just toward the wrong end; **component-level analysis misses multi-step attacks** — the EchoLeak vulnerability (CVSS 9.3) looked compliant when each component was reviewed individually, only becoming visible across the full chain; **trust boundaries are probabilistic, not fixed** — an instruction like "never share sensitive data" is a soft control, and documented tool-poisoning attacks evaded output-based safety checks in 95% of tested cases; and **memory creates persistence threats with no classical equivalent** — poisoned memory has shown injection success rates above 95% in research settings. *(Source: [Augment Code — AI/Agentic Threat Modeling](https://www.augmentcode.com/guides/ai-agentic-threat-modeling))*

---

### 2. New threat categories to scope for explicitly

| Category | What it is |
|---|---|
| Prompt injection (direct & indirect) | Malicious instructions smuggled into input or retrieved content |
| Memory poisoning | Corrupting an agent's persistent memory across sessions |
| Tool misuse / goal hijacking | Agent uses legitimate tools toward an unintended end |
| Agent impersonation | One agent in a multi-agent system spoofing another |
| Supply chain via hallucinated dependencies | Agent references a package/library that doesn't exist or is squatted |

These sit alongside — not instead of — the OWASP Agentic Top 10 below, which is the broader scoping checklist.

---

### 3. The layered framework: don't replace STRIDE, stack on top of it

The current best-documented approach layers three frameworks rather than picking one: **MAESTRO** decomposes the system into seven layers (foundation models, data operations, agent frameworks, infrastructure, observability, security/compliance, tools/integrations), each with its own threat catalog; **MITRE ATLAS** supplies 84 documented adversary techniques grounded in real incidents, including 14 agentic-specific methods like "AI Agent Context Poisoning"; and **NIST AI RMF** sits above both — MAESTRO threats inform its Map function, ATLAS validates coverage during Measure, and Manage defines the runtime policy and human-approval points. *(Source: [Augment Code — AI/Agentic Threat Modeling](https://www.augmentcode.com/guides/ai-agentic-threat-modeling))*

---

### 4. The practical eight-step workflow

Decompose the system including agent-specific nodes (runtime, memory, retrieval, tools, approval paths, audit trails). Inventory the stack against MAESTRO's seven layers. Define trust boundaries explicitly for tool responses, RAG retrievals, and inter-agent messages. Enumerate threats layer by layer, then hunt specifically for cross-layer chains. Map each threat to an ATLAS technique to validate it against real adversary behavior. Score using the OWASP Agentic Vulnerability Scoring System. Plan mitigations across four defense layers — input security, model security, tool security, monitoring. Map the results into NIST AI RMF functions, with explicit human-approval points defined for production data access, financial transactions, external communications, and sub-agent spawning. Critically: keep this continuous — update the threat model with every pull request and track the threat delta, rather than treating it as a one-time exercise at project kickoff.

---

### 5. Where AI tooling now does part of this for you

AWS Security Agent's threat-modeling capability (public preview, June 2026) analyzes design documents or source code directly, understands the application architecture, and identifies threats with recommended mitigations using STRIDE — automating what used to be a fully manual whiteboard exercise. It integrates directly into Kiro and Claude Code, so a threat model can be generated from a spec during initial design rather than bolted on afterward, and security teams can run it as a pre-deployment gate against design docs and source independently. *(Source: [AWS — Security Agent Threat Modeling](https://aws.amazon.com/about-aws/whats-new/2026/06/aws-security-agent-threat-modeling/))* Treat this as a first pass, not a replacement for the layered analysis above — it accelerates STRIDE-level coverage, not the agent-specific gaps in Section 1.

---

### 6. OWASP Agentic Top 10, as your scoping checklist

Prompt injection/jailbreaking, sensitive information disclosure, privilege escalation, model denial of service, supply chain vulnerabilities, insecure output handling, memory poisoning, unauthorized code execution, overreliance on agent autonomy, and multi-step tool-chaining attacks. Each maps to an architectural control, not a prompt filter — which is exactly why the security-guardrails category from Submodule 4's AGENTS.md template exists: those controls need to be enforced structurally, not just documented. *(Source: [OWASP Agentic Top 10](https://danielsmithdevelopment.com/articles/agentic-ai-security-governance-and-owasp-agentic))*

Pair this with a mandatory **quarterly review**, owned by a named individual, covering nine areas: supply chain image verification, admission control, identity/zero-trust validation, network containment, monitoring alert tuning, data protection and logging, backup/recovery testing, threat model currency, and documentation currency. A review with no named owner reliably doesn't happen on schedule.

---

### 7. Where this connects

A threat category discovered during review that recurs a third time is, again, a Submodule 2 "Compound" moment — it becomes a line in the AGENTS.md security-guardrails section (Submodule 4), enforced on every future generation instead of re-discovered per feature.

---

### Checkpoint

Take one feature currently in flight that touches an AI agent or tool call. Run it through the OWASP Agentic Top 10 list above and flag which categories apply. For each one that does, name the specific architectural control (not a policy statement) that would catch it.

---

### References

- [Augment Code — AI/Agentic Threat Modeling](https://www.augmentcode.com/guides/ai-agentic-threat-modeling)
- [AWS — Security Agent Threat Modeling (public preview)](https://aws.amazon.com/about-aws/whats-new/2026/06/aws-security-agent-threat-modeling/)
- [OWASP Agentic Top 10 & Quarterly Review](https://danielsmithdevelopment.com/articles/agentic-ai-security-governance-and-owasp-agentic)
- [ASTRIDE: Security Threat Modeling Platform for Agentic-AI Applications](https://arxiv.org/abs/2512.04785)
- [Forrester's Agentic Development Security (ADS) framework](https://www.augmentcode.com/guides/agentic-development-security)
