---
name: seo-helper
description: Use when creating or auditing an SEO or marketing landing page - audits an existing page or generates a self-contained landing-page mockup, with every structural and SEO choice backed by a cited claim from this plugin's evidence library, and never invents sources
---

# SEO Helper

Audit an existing landing page against the evidence library, or generate a
self-contained landing-page mockup with every structural choice cited. Every
recommendation you make must either cite a claim from the library or be
labeled as opinion.

## Hard rules

- NEVER invent a claim ID, a source, a statistic, or a study. If the
  library has no claim for a finding, label the finding
  "opinion — no citation" and say so plainly.
- Cite claims by ID and source name, e.g. "(EV-SEO-001, Google Search
  Central)". Only cite IDs you have actually read in this session.
- Do not dump every rule you read. In Audit mode, report what is wrong with
  THIS page, ordered by user impact.

## Two modes

This skill operates in one of two modes:

- **Audit** — you are reviewing an existing page (code, screenshot, or
  description) and want a cited critique.
- **Generate** — you want a new self-contained landing-page mockup produced
  from the evidence.

The mode is chosen from the user's request. If the request does not make the
mode clear, ask which mode is wanted before proceeding.

## Audit workflow

1. Identify the page: what kind of marketing page is it, and in what form
   (code, screenshot, description)?
2. Read `${CLAUDE_PLUGIN_ROOT}/evidence/INDEX.md`. Then read the following
   evidence files in full using their full paths under
   `${CLAUDE_PLUGIN_ROOT}/evidence/`:
   - `evidence/seo/on-page.md` (EV-SEO-001..005)
   - `evidence/seo/technical.md` (EV-SEO-006..010)
   - `evidence/conversion/landing.md` (EV-CONV-001..007)
   - `evidence/layout/hierarchy.md` (EV-LAYOUT-001..003)
   - `evidence/layout/typography.md` (EV-LAYOUT-007..009)
   - `evidence/layout/scanning.md` (EV-LAYOUT-010..012)
   Also read `evidence/layout/spacing.md` (EV-LAYOUT-004..006) and
   `evidence/ux-heuristics/heuristics.md` (EV-HEUR-001..010) when reviewing
   a whole page.
3. Examine the page systematically against each claim you read: title and
   meta description presence and quality, heading outline, semantic landmark
   use, image alt text, mobile-readiness signals visible in code, value
   proposition placement, CTA count and visual hierarchy, copy scannability,
   and social proof. For code, read the actual markup; do not guess.
4. Write the review.

## Generate workflow

1. Read `${CLAUDE_PLUGIN_ROOT}/evidence/INDEX.md`. Then read these evidence
   files in full using their full paths under `${CLAUDE_PLUGIN_ROOT}/evidence/`:
   - `evidence/seo/on-page.md`
   - `evidence/seo/technical.md`
   - `evidence/conversion/landing.md`
   - `evidence/layout/hierarchy.md`
   - `evidence/layout/spacing.md`
   - `evidence/layout/typography.md`
   - `evidence/layout/scanning.md`
   - `evidence/ux-heuristics/heuristics.md`
2. Produce one self-contained HTML file. Requirements:
   - Use the pinned Tailwind Play CDN as the sole external resource:
     `<script src="https://cdn.tailwindcss.com/3.4.16"></script>`
     Make no other external requests. No fonts, no icons, no analytics.
   - Structure the page to satisfy the evidence: single benefit-focused H1
     and value proposition visible without scrolling (EV-CONV-001); one
     clearly dominant primary CTA (EV-CONV-003); semantic landmarks —
     header, nav, main, footer — rather than div soup (EV-SEO-004);
     descriptive title and meta description (EV-SEO-001, EV-SEO-002); logical
     heading outline (EV-SEO-003); descriptive alt text on all images
     (EV-SEO-008); readable line length and heading hierarchy
     (EV-LAYOUT-007, EV-LAYOUT-001).
   - Annotate each major block with an HTML comment citing the claim that
     motivated the structural choice, e.g.:
     `<!-- single primary CTA per EV-CONV-003 -->`
     If a choice has no backing claim, the comment says:
     `<!-- opinion — no citation -->`
   - End the file with a comment listing every claim ID applied.
   - Label the file at the top as a throwaway mockup, not production code.

## Output format (Audit mode)

A readable review, not a rule dump:

- One short paragraph: what was reviewed and the overall state.
- Findings ordered by user impact, each with: what is wrong, where
  (file:line for code when available), what to do instead, and the citation
  "(EV-XXXX-NNN, Source)". A finding with no supporting claim is labeled
  "opinion — no citation".
- If something is done well and a claim supports it, one short "what's
  already right" list at the end — cited the same way.

Keep the whole review proportionate: a small page gets a short review.
Do not pad.
