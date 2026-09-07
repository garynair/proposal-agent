# CLAUDE.md — Proposal Agent Project Instructions

This file orients any agent (or session) working in this folder. It describes the pipeline, the folder contract, and how the two step files relate to each other. Read this first before running `step1_content.md` or `step2_proposal.md`.

## What this project does

Turns five raw ABC Electronics discovery/pricing/research documents into a McKinsey-style consulting proposal deck (PPTX), via a two-step, file-mediated pipeline. Each step is a self-contained agent spec — it reads specific inputs and writes one specific output. Steps do not skip ahead or reach into each other's inputs.

## Folder contract

| Folder | Role | Contents |
|---|---|---|
| `Input/` | Read-only source material | `00_Workshop_Exercise_Brief.docx`, `01_Discovery_Meeting.txt`, `02_Solution_Recommendation.txt`, `03_Industry_Research.pdf`, `04_Pricing_Rate_Card.csv`, `05_Proposal_Deck_Input_Guide.docx` |
| `Content/` | Intermediate distilled content | `content.md` — produced by Step 1, consumed by Step 2 |
| `Output/` | Final deliverable | `.pptx` proposal deck — produced by Step 2 |
| `README.md` | Workshop brief (human-facing context, not agent instructions) | — |

Rule: Step 2 must never read the raw `Input/` files directly. It only reads `Content/content.md`. This keeps the pipeline auditable — anyone can check `content.md` to see exactly what facts fed the deck before a single slide is built, and re-running Step 2 alone (e.g., to change deck styling) doesn't risk re-interpreting the source documents differently.

## Pipeline

```
Input/01, 02, 03, 04  ──┐
                         ├─► [STEP 1: step1_content.md] ─► Content/content.md ─► [STEP 2: step2_proposal.md] ─► Output/*.pptx
Input/05 (structure)  ──┘
```

**Step 1 — Content Distillation** (`step1_content.md`)
Reads the four source documents (01–04) and uses `Input/05_Proposal_Deck_Input_Guide.docx` purely as the structural blueprint (it defines the 12 slides and what each one needs — it is not itself a data source). Extracts, computes, and organizes the content slide-by-slide into `Content/content.md`.

**Step 2 — Deck Generation** (`step2_proposal.md`)
Reads `Content/content.md` only. Produces a polished, high-end consulting-style PowerPoint deck in `Output/`, using the `pptx` skill.

## Execution order

1. Run Step 1 first. Verify `Content/content.md` exists and looks complete/correct before proceeding — this is the cheapest place to catch a bad number or missing fact, before it's baked into slide design.
2. Run Step 2 only after Step 1's output is reviewed (or explicitly approved to proceed without review).
3. Steps can be re-run independently: re-running Step 2 alone (e.g., "make the deck more visual") does not require re-running Step 1, as long as `content.md` hasn't changed. Re-running Step 1 (e.g., new pricing CSV) means Step 2 should be re-run too.

## Standards for both steps

- No fabrication. If a required field isn't in the source documents, flag it explicitly (e.g., `[NOT PROVIDED — confirm with client]`) rather than inventing a plausible-sounding number.
- Keep client-specific facts (from Discovery/Solution/Pricing) clearly distinguished from third-party industry benchmarks (from the Industry Research report). Never present a generic industry benchmark as if it were ABC Electronics' own measured result.
- Tone: enterprise consulting — confident, concise, benefit-oriented, evidence-based.
