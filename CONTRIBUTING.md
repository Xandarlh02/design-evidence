# Contributing

This project accepts new claims, corrections, and better sources. The bar
is the same for maintainers and contributors: no source, no ship.

## The claim format

The claim is the atomic unit: one recommendation, one citation block. Every
claim in `evidence/` uses this structure exactly:

    ## EV-FORM-001: Top-aligned labels outperform left-aligned labels
    **Strength:** research-backed
    **Claim:** Place field labels above inputs, not beside them. Top-aligned
    labels reduce completion time and avoid truncation on narrow viewports.
    **Evidence:** One or two sentences summarizing what the source actually
    found or requires, in your own words.
    **Sources:**
    - Author/Org, "Title", Year — https://example.com/the-actual-page
    **Applies when:** the context where this holds.
    **Exception:** known cases where it does not (omit if none).

## Rules

1. Every claim carries at least one working, publicly reachable URL. If the
   best source is paywalled, say so and link the public abstract or summary.
2. Strength is exactly one of:
   - `research-backed` — a published study or measured data.
   - `standard` — a normative specification (WCAG, a platform HIG).
   - `convention` — widely adopted practice with no controlled study.
   Do not dress convention up as research.
3. Claim IDs (`EV-<DOMAIN>-<NNN>`) are stable and never reused. A deleted
   claim leaves a gap in the numbering.
4. Write evidence text in your own words from the source itself. Read the
   source before citing it; do not cite from memory or from a summary of a
   summary.
5. Qualifying sources: W3C/WCAG, Nielsen Norman Group, Baymard Institute
   free articles, GOV.UK Design System research, platform interface
   guidelines (Apple, Material), published papers. Secondhand blog posts do
   not qualify.
6. When you add, change, or remove a claim, update `evidence/INDEX.md` in
   the same commit.
7. Prose standard: plain, direct writing. No emoji, no filler.

## What gets a PR rejected

- A claim with no URL, a dead URL, or a URL that does not support the claim.
- Copied text from a paywalled or copyrighted source.
- A `research-backed` label on something that is actually convention.
- Executable code of any kind. This plugin ships no executable code — markdown, JSON, and script-free test fixtures only.
