# Pre-release behavioral checklist

Run these in a fresh Claude Code session with the plugin installed, before
tagging a release. A failed check means a SKILL.md or evidence file needs
tightening — fix and rerun.

## design-review

1. Ask for a design review of `tests/fixtures/bad-form.html`.
   The review must:
   - cite the placeholder-as-label problem (EV-FORM-002),
   - cite the multi-column layout problem (EV-FORM-013),
   - cite the vague error message problem (EV-FORM-006),
   - cite color-only error signaling (EV-FORM-007 or EV-A11Y-004),
   - cite the removed focus outline (EV-A11Y-005),
   - cite insufficient contrast on the button (EV-A11Y-001),
   - cite the generic "Submit" label (EV-FORM-014),
   - cite missing programmatic labels (EV-A11Y-013).
2. Every claim ID cited in the review must exist in `evidence/`:
   spot-check each cited ID with a grep.
3. The review must contain no claim ID that does not exist in `evidence/`.
4. Ask a design question the library does not cover (e.g. "should my logo
   be on the left or right?"). The answer must be labeled as opinion or
   convention, with no fabricated citation.

## Install

5. In a fresh Claude Code session (no plugin pre-loaded), run:
   `/plugin marketplace add xandarlh02/design-evidence`
   then `/plugin install design-evidence`.
   Both commands must succeed without errors, and the design-review skill
   must appear in the skill list (e.g. via `/skills` or by confirming the
   skill is invocable).

## Evidence library

6. Every URL in `evidence/` resolves (fetch each; fix or remove dead ones).
7. Format lint passes: the number of `**Strength:**` lines equals the
   number of `## EV-` headings in every evidence file.

## design-review — layout pass

8. Ask for a design review of `tests/fixtures/bad-landing.html`. The review must:
   - flag the weak/absent visual hierarchy or missing dominant focal point (cite EV-LAYOUT-001 or EV-LAYOUT-002),
   - flag the over-long / justified body text (cite EV-LAYOUT-007 or EV-LAYOUT-012),
   - raise at least one Nielsen heuristic finding (cite an EV-HEUR-0NN id),
   - cite no claim ID that does not exist in evidence/.

## seo-helper

9. Ask seo-helper to AUDIT tests/fixtures/bad-seo-landing.html. The review must:
   - flag missing/duplicate title and absent meta description (cite EV-SEO-001 and EV-SEO-002),
   - flag missing or multiple h1 elements and non-semantic div structure instead of landmarks (cite EV-SEO-003 and EV-SEO-004),
   - flag images with no alt attribute (cite EV-SEO-008),
   - flag the absent value proposition above the fold and the three equally-weighted competing CTAs (cite EV-CONV-001 and EV-CONV-003),
   - cite no claim ID that does not exist in evidence/.
10. Ask seo-helper to GENERATE a landing page for a sample product. The output must:
    - be a single self-contained HTML file,
    - make no external request except the pinned Tailwind CDN (https://cdn.tailwindcss.com/3.4.16),
    - contain HTML citation comments that reference only real claim IDs (spot-check each with grep),
    - be labeled a throwaway mockup.
