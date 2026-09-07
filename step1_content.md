# Step 1 — Content Distillation Agent

## Purpose

Read the four raw source documents and distill their content into one organized file, `Content/content.md`, structured slide-by-slide according to the blueprint in `Input/05_Proposal_Deck_Input_Guide.docx`. This is preparation work only — no slide design, no PowerPoint. The output is a content brief a deck-builder (Step 2) can work from without re-reading the source documents.

## Inputs

| File | Role |
|---|---|
| `Input/01_Discovery_Meeting.txt` | Client discovery transcript: current process, volumes, channels, pain points, goals |
| `Input/02_Solution_Recommendation.txt` | Recommended AI modules, implementation phases, success metrics |
| `Input/03_Industry_Research.pdf` | Market sizing, benchmarks, third-party ROI case study — supporting evidence only |
| `Input/04_Pricing_Rate_Card.csv` | Line-item pricing — source for the Investment slide |
| `Input/05_Proposal_Deck_Input_Guide.docx` | **Structure only.** Defines the 12 slides and what each requires. Do not treat as a data source. |

## Process

1. Read all five files in full.
2. Work through the 12 slides defined in the guide, one at a time. For each slide, pull only the facts that belong there from 01/02/03/04 — do not blend content across slides.
3. Where a slide requires a computed or rolled-up figure (see Investment rules below), compute it and show the arithmetic, not just the result.
4. Where the guide expects a table, produce the table in `content.md` (Markdown table), not a paragraph.
5. If something the guide asks for isn't present anywhere in 01–04, write `[NOT PROVIDED — confirm with client]` in that spot. Do not invent numbers, dates, or names.
6. Keep client facts and industry-research benchmarks visibly separate (see Guardrails).

## Slide-by-slide mapping

**Slide 1 — Title**
Project title (author a concise, benefit-oriented title, e.g. "AI Customer Support Automation for ABC Electronics"), client name (ABC Electronics), prepared by (`[NOT PROVIDED — confirm with client]` unless a firm/consultant name exists in the source docs), date (use current date), one-line value proposition (synthesize from Discovery goals + Solution Recommendation).

**Slide 2 — Executive Summary**
Synthesize: current state (300 queries/day across WhatsApp/email/web, 8 agents, 4–6 hr response times), proposed solution (AI Customer Support Agent — FAQ, order tracking, returns, escalation, analytics), expected value (from Solution Recommendation's success metrics), implementation duration (from the 5-phase roadmap in doc 02 — roll up to a total, e.g. ~6 weeks per Slide 8 guide).

**Slide 3 — Client Business Overview**
Industry (online/consumer electronics retail), products/services, support channels (WhatsApp, Website Chat, Email, Phone per doc 01 — reconcile against the guide's example table which lists WhatsApp/Email/Web), daily ticket volume (300, from doc 01), number of support agents (8, from doc 01). Build the Metric/Value table as shown in the guide.

**Slide 4 — Current Challenges**
Pull the bulleted pain points from doc 01 (slow response 4–6 hrs, repetitive questions, no after-hours support, difficult cross-channel tracking) and pair each with a business impact (poor CX, high workload, missed opportunities, poor visibility) as a Challenge / Business Impact table.

**Slide 5 — Proposed AI Solution**
Describe each of the 7 recommended components from doc 02 (AI FAQ Agent, Order Tracking Assistant, Returns & Refund Assistant, Human Escalation Workflow, Website Chatbot, WhatsApp AI Assistant, Daily Support Analytics Dashboard) in one line each — what it does and which client pain point it addresses. Note: the guide lists 5 modules; include all 7 from doc 02 and note the guide's list is illustrative, not exhaustive.

**Slide 6 — Solution Architecture**
Describe the flow: Customer → Website / WhatsApp / Email → AI Agent → Knowledge Base → Business Systems → Human Agent (if escalation needed). Note integration points implied by doc 02 (order tracking system, knowledge base, WhatsApp API, website chat, analytics dashboard).

**Slide 7 — Scope & Deliverables**
Build the Deliverable / Description table per the guide (Knowledge Base, AI Agent, Integrations, Dashboard, Training), populated using doc 02's components and doc 04's line items as evidence of what's included.

**Slide 8 — Implementation Roadmap**
Use doc 02's 5 phases (Knowledge Base, AI Chatbot, WhatsApp Integration, Dashboard & Reporting, User Training) mapped onto the guide's 6-week table (Discovery / Development / Integration / Testing / Go-Live). Reconcile any mismatch between doc 02's phase names and the guide's week labels explicitly rather than silently picking one.

**Slide 9 — Investment**
Roll up `Input/04_Pricing_Rate_Card.csv` into the guide's Category / Cost table (Software, Implementation, Training, Support, Total) using this fixed mapping so the categorization is deterministic and repeatable:

| Guide Category | CSV `Category` values included | Line items |
|---|---|---|
| Software | `Module` | AI FAQ Agent, Returns & Refund Agent |
| Training | `Session` | Staff Training |
| Support | `Month`, `Year` | Hypercare Support (30 Days), Annual Support & Maintenance |
| Implementation | `Project`, `Integration`, `Channel`, `Workflow`, `Dashboard`, `Week` | Discovery Workshop, Business Process Assessment, Knowledge Base Creation, Order Tracking Integration, Website Chatbot, WhatsApp Integration, Email Automation, Human Escalation Workflow, Analytics Dashboard, User Acceptance Testing, Project Management |

Sum each bucket from `Line_Total_USD`, then sum all four for Total Project Investment. Show the bucket totals and the grand total in `content.md`; Step 2 will render the table, it should not need to re-derive the arithmetic.

**Slide 10 — Business Benefits & ROI**
Populate the Before/After table using client-specific figures only: Response Time (4–6 hrs → <5 min, from docs 01/02), Automation Rate (0% → 80%, from doc 02), Manual Work (High → Reduced, from doc 01 goals), Customer Satisfaction (Current → Improved, qualitative — no fabricated score). For "estimated annual savings and ROI," doc 04/01/02 contain no client-specific savings figures — do not compute a client dollar ROI from thin air. Instead, cite the Industry Research benchmarks (Section 4 of doc 03: $220K total estimated benefit / $55K illustrative project cost / 300% ROI, and the 40–60% automation, 3–6 month payback, 20–50% agent productivity gains) explicitly labeled as **industry benchmark, not a client-specific projection**.

**Slide 11 — Risks & Assumptions**
Use the guide's list directly (Risks: knowledge base quality, integration dependencies, user adoption; Assumptions: timely system access, stakeholder availability, approved FAQ content) — these aren't contradicted by anything in 01–04, so carry them through as-is unless the source docs suggest additions.

**Slide 12 — Next Steps**
Use the guide's sequence (Project approval, Contract signing, Discovery workshop, Knowledge collection, Project kickoff, Questions & Contact Information). Note: doc 04 already prices a "Discovery Workshop" as a line item — flag this if it creates ambiguity about whether discovery has already happened or is a proposed next step, rather than silently resolving it.

## Guardrails

- **Client fact vs. industry benchmark:** every figure in the deck must be traceable to either (a) a client-specific source (docs 01, 02, 04) or (b) the industry research report (doc 03). Label doc 03 figures as benchmarks in `content.md` so Step 2 can visually distinguish them (e.g., a "supporting evidence" callout rather than presenting them as ABC Electronics' results).
- **No invented numbers.** If precision isn't available, use the range given in the source (e.g., "4–6 hours," not a fabricated single average).
- **Traceability.** Tag each slide section with its source document(s) in a short parenthetical, e.g. `(Source: 01, 02)`, so a reviewer can spot-check quickly.

## Output

Write to `Content/content.md`. Structure: one `##` heading per slide (`## Slide 1 — Title`, etc.), in order, with the content/tables/flags described above. This file is the single input Step 2 is allowed to read.
