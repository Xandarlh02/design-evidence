# design-evidence — layout/UX evidence, holistic review, and seo-helper

Date: 2026-08-31
Status: pending owner review

## What this is

An expansion of the design-evidence plugin in two directions the owner asked
for:

1. Make the existing `design-review` skill judge **whole-page layout and
   UI/UX**, not just component-level details. The skill was catching small
   things (a placeholder used as a label, a low-contrast button) but had no
   basis to say "this layout has no visual hierarchy" or "this flow violates
   a basic usability heuristic" — because the evidence library had no layout
   or heuristics domains. This adds them and upgrades the review workflow to
   use them.
2. Add a new **`seo-helper`** skill that helps create and audit SEO and
   marketing landing pages, held to the same evidence-cited standard as the
   rest of the plugin.

Both build on the plugin's existing architecture unchanged: thin skills over
a shared, cited evidence library. No new architectural pattern is introduced.
The typography/layout and navigation domains were already anticipated as
"Phase 2" in the original design spec (2026-08-28); this realises the layout
portion and adds SEO/conversion, which were not previously planned.

## Decisions made during brainstorming

- `design-review` stays a single skill; it gains a holistic layout pass
  rather than being split.
- The SEO capability is a **separate skill** (`seo-helper`), not folded into
  design-review, because it both audits and *generates* — a distinct job.
- `seo-helper` does both: audit an existing page, or generate a landing-page
  mockup.
- Generated output is a **self-contained HTML file** styled with the pinned
  Tailwind CDN — matching the plugin's existing output convention and its
  "no executable code inside the plugin" rule. Generated files are throwaway
  mockups, labeled as such, and are the only place third-party code appears.
- Review depth for layout: build a focused **layout/visual-hierarchy** domain
  plus **Nielsen's 10 usability heuristics** as an evidence-backed lens —
  enough to review a whole page, without committing to the full
  navigation/IA/dashboards domain in this pass.
- The hard discipline is unchanged and non-negotiable: never invent a claim
  ID, source, statistic, or study; label anything the library cannot support
  as opinion; honest strength labels (`research-backed` / `standard` /
  `convention`).

## New evidence domains

Four new claim prefixes are introduced. All follow the existing claim format
(`## EV-<PREFIX>-<NNN>`, `**Strength:**`, `**Claim:**`, `**Evidence:**`,
`**Sources:**`, `**Applies when:**`, optional `**Exception:**`) and the
sourcing bar in CONTRIBUTING.md. Claim counts below are targets; a claim that
cannot be backed by a qualifying, fetchable source is dropped rather than
shipped, so final counts may be lower.

### EV-LAYOUT — layout and visual hierarchy (~12 claims)

Files under `evidence/layout/`:

- `hierarchy.md` — establishing scanning order through size/weight/contrast;
  a single dominant focal point per view; hierarchy that matches task
  priority.
- `spacing.md` — whitespace and proximity (Gestalt grouping); grouping
  related controls; a consistent spacing scale.
- `typography.md` — a limited modular type scale; comfortable line length /
  measure (~45–75 characters); line-height and body legibility.
- `scanning.md` — F-pattern / layer-cake scanning behaviour; front-loading
  important words; left-alignment of body text for LTR reading.

Primary sources: Nielsen Norman Group (F-pattern, hierarchy, whitespace),
GOV.UK Design System / Service Manual, WCAG 1.4.8 (visual presentation) and
1.4.10 (reflow), Baymard where applicable. Claims that are professional
consensus without a controlled study are labeled `convention`.

### EV-HEUR — usability heuristics (10 claims)

File `evidence/ux-heuristics/heuristics.md`: Nielsen's 10 usability
heuristics, one claim each (`EV-HEUR-001` … `EV-HEUR-010`). Sourced to the
NN/g "10 Usability Heuristics for User Interface Design" article. Strength:
`convention` — these are expert-distilled heuristics, not measured effects,
and will be labeled honestly as such rather than dressed up as research. Their
value is as a holistic checklist the review can apply to a whole screen.

### EV-SEO — on-page and technical SEO (~10 claims)

Files under `evidence/seo/`:

- `on-page.md` — descriptive, unique `<title>`; useful meta description; one
  clear `<h1>` and a logical heading outline; semantic landmark structure;
  descriptive link text.
- `technical.md` — mobile-friendly / responsive rendering; Core Web Vitals
  (LCP/CLS/INP) as ranking-relevant performance; descriptive image `alt` and
  image optimisation; structured data where a content type supports it;
  canonicalisation and crawlability basics.

Primary sources: Google Search Central documentation (SEO Starter Guide,
title-link and meta-description guidance, structured-data intro), web.dev /
Core Web Vitals, WCAG for the alt-text and heading overlaps. Google's own
guidance is authoritative platform documentation; claims drawn from a
normative spec (WCAG) are `standard`, claims from Google's guidance are
labeled `convention` unless they restate a spec.

### EV-CONV — landing-page conversion (~7 claims)

File `evidence/conversion/landing.md`:

- message match between the ad/link and the landing headline;
- a benefit-led headline that states the value proposition;
- a single primary call to action / controlled attention ratio;
- an above-the-fold value proposition;
- credible social proof;
- scannable copy (short blocks, meaningful subheads);
- directional / visual cues leading to the CTA.

Primary sources: NN/g (attention, scanning, value proposition), Baymard,
GOV.UK research. Much CRO/landing-page content on the web is vendor marketing
that does not clear the sourcing bar; claims that cannot be sourced to a
qualifying study are either labeled `convention` (where they are genuine
professional consensus) or dropped. This domain is expected to carry the most
`convention` labels, and that will be stated plainly.

## Skill changes

### design-review (upgraded)

The hard rules and output discipline are unchanged. The workflow gains an
explicit **whole-view layout pass**:

- When the thing under review is a full screen or page (not an isolated
  component), the skill first evaluates the layout as a whole — visual
  hierarchy, spacing and grouping, reading/scan flow, information
  architecture — and runs the Nielsen-10 lens (`EV-HEUR`) over the screen,
  before dropping to component-level checks.
- Findings from the layout pass are reported in the same impact-ordered
  format with the same citation rules. A layout problem with no supporting
  claim is still labeled "opinion — no citation".
- The evidence-selection step is extended: full-page reviews pull
  `EV-LAYOUT` and `EV-HEUR` in addition to the domain-specific files.

The intent is that a user can point the skill at a repo or a screenshot and
get back what is wrong with the *layout and overall UX*, not only field-level
nits — while still never inventing a source.

### seo-helper (new)

`skills/seo-helper/SKILL.md`. Two modes, chosen from the request:

- **Audit** — mirrors design-review over `EV-SEO`, `EV-CONV`, and
  `EV-LAYOUT`. Reviews an existing landing page (code, screenshot, or URL
  description), reports SEO and conversion problems ordered by impact, each
  cited by claim ID and source. Same hard rules.
- **Generate** — produces one self-contained HTML landing page: pinned
  Tailwind CDN, no other external requests, opens directly in a browser. The
  skill reads the relevant evidence first, and every structural choice is
  annotated with an HTML comment citing the claim that motivated it
  (e.g. `<!-- single primary CTA per EV-CONV-003 -->`). The file is labeled a
  throwaway mockup, not production code. The skill never invents a claim to
  justify a block; if a choice has no backing claim, the comment says so.

The skill description triggers on requests to create, build, or audit SEO or
marketing landing pages.

## Supporting updates

- `evidence/INDEX.md` — add the four new domains with scope notes and claim
  IDs, in the existing one-line-per-file format.
- `README.md` — list the `seo-helper` skill and the new evidence domains;
  keep the "sources you can check" framing.
- `CONTRIBUTING.md` — add `EV-LAYOUT`, `EV-HEUR`, `EV-SEO`, `EV-CONV` to the
  domain/prefix conventions; sourcing bar is otherwise unchanged.
- `tests/CHECKLIST.md` — add behavioral checks: a full-page review must
  produce at least one layout/hierarchy or heuristic finding and cite an
  `EV-LAYOUT`/`EV-HEUR` ID; a `seo-helper` generate run must emit a single
  self-contained file whose only external request is the pinned Tailwind CDN
  and whose citation comments reference only real claim IDs; a `seo-helper`
  audit must cite `EV-SEO`/`EV-CONV` and invent nothing.
- `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json` —
  version bump to `0.2.0`; descriptions updated to mention layout/UX review
  and SEO landing pages.
- A fixture for the new checks: a deliberately weak landing page under
  `tests/fixtures/` (script-free HTML) exercising missing `<h1>`, buried CTA,
  no value proposition, and poor hierarchy.

## Sequencing

Authoring ~39 cited claims from fetched sources is the bulk of the work. It is
sequenced into small, independently-valuable commits, matching the existing
git history's cadence (evidence lands in batches of a few claims, each with a
follow-up fix pass if a source does not hold up):

1. EV-LAYOUT (hierarchy + spacing), then (typography + scanning).
2. EV-HEUR (Nielsen 10).
3. design-review workflow upgrade + INDEX + a full-page fixture and checklist
   entries. **The layout-review capability is publishable at this point**,
   independent of the SEO work.
4. EV-SEO (on-page, then technical).
5. EV-CONV (landing).
6. `seo-helper` skill (audit + generate), fixture, checklist, README,
   manifests, version bump.

Each evidence step ends with the URL/format lint (every URL resolves; count
of `**Strength:**` equals count of `## EV-` headings per file) before moving
on.

## Testing

Behavioral, as with the existing skill (a prompt-based plugin is verified by
running it, not by unit tests). New checklist items are listed under
"Supporting updates". The existing bad-form checks remain. A failed check
means a SKILL.md or evidence file needs tightening; fix and rerun.

## Out of scope

- The navigation / IA / dashboards evidence domain (still deferred; the
  holistic review leans on EV-HEUR for IA-level observations for now).
- Framework-aware generation (React/Vue/Next output). Generation is
  self-contained HTML only; a user can ask Claude to translate it.
- The `quick-demo` and `blocks` skills from the original spec (unchanged,
  still planned separately).
- Any runtime scripts, MCP servers, or live web retrieval inside the plugin.
- Automated rank-tracking, keyword-volume, or backlink SEO tooling — this is
  on-page and content SEO guidance only, held to the evidence bar.
