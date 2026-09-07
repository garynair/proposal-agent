# Step 2 — Proposal Deck Generation Agent

## Purpose

Turn `Content/content.md` into a polished, high-end management-consulting-style PowerPoint deck, saved to `Output/`. This step does not read `Input/` — if something looks missing or wrong, that's a Step 1 problem to fix upstream, not something to patch here by going back to the raw sources.

## Input

`Content/content.md` only — the slide-by-slide content brief produced by Step 1 (12 sections, one per slide, including tables, computed figures, and any `[NOT PROVIDED]` flags).

## Before building: read the skill

Use the `pptx` skill. Read its `SKILL.md` before writing any code, and follow its build process (python-pptx, template/layout conventions, etc.) rather than improvising slide XML by hand.

## Design direction — "McKinsey-style" consulting deck

**Visual system**
- Palette: deep navy / charcoal + white, with a single accent color (e.g. a bright teal or amber) used sparingly for emphasis (key numbers, callouts, the accent bar). No more than 3 colors total plus greys.
- Typography: one clean sans-serif family throughout (e.g. Calibri, Arial, or similar available font). Slide titles are short, bold, and state the takeaway — not a generic label. Example: not "Investment" but "Total investment of $27K delivers a fully automated support stack in 6 weeks."
- Layout: generous white space, left-aligned text blocks, consistent margins. Avoid dense paragraphs — bullets are short (3–8 words where possible), supporting detail lives in speaker notes if needed, not crammed onto the slide.
- Consistent header/footer on every slide: small client/project label top-left or top-right, page number and "Confidential" footer bottom.
- Every slide's title should be the argument, not the topic (a hallmark of top-tier consulting decks): the reader should be able to read only the 12 titles in sequence and follow the entire proposal narrative.

**Slide-by-slide build notes**

1. **Title** — Clean cover slide: project title, ABC Electronics, prepared-by/date, one-line value proposition as a subtitle.
2. **Executive Summary** — 3–4 short takeaway statements (current state → solution → value → timeline), not a wall of text. Consider a simple 4-box or horizontal-flow layout.
3. **Client Business Overview** — Metric/value table or a row of 3 stat callouts (300 tickets/day, 8 agents, 3 channels) rendered as large-number "stat cards" rather than a plain table.
4. **Current Challenges** — Challenge/Impact table, or icon + text rows, one per pain point.
5. **Proposed AI Solution** — Grid or row of 5–7 module cards, one per component, short label + one-line description each.
6. **Solution Architecture** — Build an actual left-to-right flow diagram using shapes/arrows (Customer → Channels → AI Agent → Knowledge Base → Business Systems → Human Agent), not a text description. This is the one slide where a simple diagram matters more than prose.
7. **Scope & Deliverables** — Deliverable/Description table, clean two-column layout.
8. **Implementation Roadmap** — Horizontal timeline/Gantt-style bar across 6 weeks with phase labels, not just a table — this is a standard consulting-deck visual and should look like one.
9. **Investment** — Category/Cost table (Software, Implementation, Training, Support, Total) plus a simple stacked or horizontal bar chart showing the cost breakdown visually. Bold/accent-color the Total row.
10. **Business Benefits & ROI** — Before/After table with the accent color highlighting the "After" column. Where content.md includes industry-benchmark ROI figures, present them in a visually distinct callout box labeled "Industry Benchmark" (not blended into the client's own Before/After table) — do not let the deck imply these are ABC Electronics' guaranteed results.
11. **Risks & Assumptions** — Two-column layout: Risks left, Assumptions right, short bullets.
12. **Next Steps** — Simple numbered sequence (5 steps) plus a closing contact/questions line.

**What to do with `[NOT PROVIDED]` flags**
If `content.md` contains any `[NOT PROVIDED — confirm with client]` markers, keep them visible on the slide in a muted/italic style rather than silently dropping them or inventing a placeholder value — the deck should make it obvious to a human reviewer what still needs client input before this goes out the door.

## Output

Save the deck to `Output/` as a single `.pptx` file, named `ABC_Electronics_AI_Customer_Support_Proposal.pptx`. Roughly 12 slides (one per section in `content.md`); do not pad with extra slides not grounded in the content brief.

## Quality check before finishing

- Every number on every slide should trace back to something in `content.md` — no new figures introduced at build time.
- Read the deck back slide-by-slide (title-only pass) and confirm the 12 titles alone tell a coherent story.
- Confirm industry-benchmark figures (Slide 10) are visually distinguishable from client-specific figures.
