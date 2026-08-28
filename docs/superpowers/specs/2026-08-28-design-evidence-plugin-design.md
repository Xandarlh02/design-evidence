# design-evidence — plugin design

Date: 2026-08-28
Status: approved by owner, pending implementation planning

## What this is

A public Claude Code plugin for UI/UX and design work. Its core is a curated
knowledge base of design best practices in which every claim is backed by a
named, publicly reachable source. Three skills consume that knowledge base: a
design reviewer, a quick demo builder, and a website block library.

The differentiator is credibility. Existing design plugins (for example
ui-ux-pro-max) ship large curated datasets with no sources. This plugin never
states a best practice it cannot cite, and it labels honestly how strong the
evidence is. A user can audit every claim on GitHub.

"design-evidence" is a working name; the owner may rename before publishing.

## Decisions made during brainstorming

- Core identity: the evidence-backed knowledge base. The skills exist to
  demonstrate and apply it.
- Evidence model: curated static library, written in the plugin's own words,
  researched from real sources at authoring time. No live retrieval at use time.
- V1 consumer skills: design-review, quick-demo, blocks. (A design-guide
  generator was considered and deferred.)
- Knowledge base domains at launch: forms and conversion; accessibility;
  typography, color, and layout; navigation, IA, and dashboards.
- Output stack for generated demos and blocks: self-contained HTML, styled
  with Tailwind loaded from a pinned CDN URL.
- Security constraint: the plugin itself contains no executable code. No
  scripts, no package.json, no build step, no dependencies. Everything a user
  installs is text they can read. Generated demo/block files are the only
  place third-party code (the pinned Tailwind CDN) appears.
- Architecture: shared evidence library plus thin consumer skills
  (approach A), with stable claim IDs borrowed from the indexed-dataset
  approach but implemented as plain text, not scripts.
- Writing standard: all documentation, README files, and evidence prose are
  written in plain, direct human prose. No emoji decoration, no marketing
  filler, no generated-sounding boilerplate.

## Repository structure

```
design-evidence/
├── .claude-plugin/
│   ├── plugin.json          # name, version, description
│   └── marketplace.json     # installable via /plugin marketplace add
├── skills/
│   ├── design-review/SKILL.md
│   ├── quick-demo/SKILL.md
│   └── blocks/SKILL.md
├── evidence/
│   ├── INDEX.md             # topic → file map; the only file skills always read
│   ├── forms/               # labels.md, validation.md, checkout.md, cta.md
│   ├── accessibility/       # contrast.md, focus.md, touch-targets.md, aria.md
│   ├── typography-layout/   # type-scale.md, line-length.md, spacing.md, color.md
│   └── navigation-dashboards/  # menus.md, ia.md, dashboards.md, data-viz.md
├── blocks/                  # standalone HTML block files
├── docs/superpowers/specs/  # this document
├── README.md
└── CONTRIBUTING.md
```

The file lists inside `evidence/` are indicative; exact filenames are settled
during implementation. Every evidence file follows the claim format below.

## Evidence format

The claim is the atomic unit: one recommendation, one citation block.

```markdown
## EV-FORM-003: Top-aligned labels outperform left-aligned labels
**Strength:** research-backed
**Claim:** Place field labels above inputs, not beside them. Top-aligned
labels reduce form completion time and eliminate label-truncation issues
on narrow viewports.
**Evidence:** Eye-tracking research by Matteo Penzo (2006, UXmatters) found
top-aligned labels required the fewest fixations; Baymard Institute's
checkout studies reach the same conclusion for e-commerce forms.
**Sources:**
- Penzo, "Label Placement in Forms", UXmatters, 2006 — <url>
- Baymard Institute, "Form Field Usability" (free article) — <url>
**Applies when:** standard data-entry forms.
**Exception:** dense enterprise grids where vertical space is scarce.
```

Rules that make the promise enforceable:

1. Every claim carries at least one working, publicly reachable URL. If the
   best source is paywalled, the claim says so and links the public abstract
   or summary. A claim with no source does not ship.
2. Strength labels are honest and limited to three values:
   - `research-backed` — a published study or measured data.
   - `standard` — a normative specification (WCAG, a platform HIG).
   - `convention` — widely adopted practice with no controlled study,
     stated as such.
   Convention is never dressed up as research.
3. Claim IDs are stable (`EV-<DOMAIN>-<NNN>`), cited by the skills, and never
   reused after a claim is deleted.

`evidence/INDEX.md` lists every evidence file with a one-line scope note and
the claim IDs it contains. Skills grep the index, then read only the two or
three files relevant to the task, keeping context small.

## Skills

### design-review

Reviews existing UI: a file, a folder, a screenshot, or a pasted mockup.
Workflow: identify the kind of UI, grep `evidence/INDEX.md` for relevant
domains, read those evidence files, review the code against the claims, and
report findings ordered by impact. Every finding cites its claim ID and
source. A finding the evidence base cannot support is labeled as opinion with
no citation; the skill is explicitly forbidden from inventing sources. Output
is a readable review in chat, not a rule dump.

### quick-demo

Turns a description into a clickable multi-screen mockup: one self-contained
HTML file per screen, plain-JS navigation between screens, Tailwind from the
pinned CDN. The skill reads the relevant evidence files before writing code.
Each generated file ends with an HTML comment listing the claims that shaped
it (for example "labels top-aligned per EV-FORM-003"). Demos are labeled
throwaway mockups, not production code.

### blocks

A curated library in `blocks/`: hero, pricing table, nav bar, form, dashboard
shell, stats cards, footer, and similar. Each block is a single HTML file
that renders standalone and is copy-pasteable, with a short header comment
citing the evidence behind its structure. The skill helps the user pick,
customize, and combine blocks. Quality over quantity: v1 ships roughly 8–10
excellent blocks.

## Curation process

Evidence files are authored with research discipline, not from memory:

- Every claim starts from fetching and reading the actual source during
  authoring. The plugin works offline; the authoring process does not.
- Qualifying sources: W3C/WCAG, Nielsen Norman Group, Baymard Institute free
  articles, GOV.UK Design System research, platform HIGs (Apple, Material),
  published papers. Secondhand blog summaries do not qualify.
- Paywalled research may be cited and summarized in the plugin's own words,
  never copied.
- Before each release, a link check confirms every URL resolves. This may be
  a one-off script run by the maintainer; it never ships in the plugin.
- CONTRIBUTING.md holds pull requests to the same bar: claim, strength
  label, and reachable source, or the PR is rejected.

## Phasing

1. Phase 1 — repo scaffold, evidence format, forms and accessibility domains
   (roughly 15–20 claims each), and the design-review skill. Publishable on
   its own.
2. Phase 2 — typography/layout and navigation/dashboards domains, and the
   quick-demo skill.
3. Phase 3 — the blocks library and skill, README and marketplace polish,
   public launch.

Each phase gets its own implementation plan.

## Testing

A prompt-based plugin is verified behaviorally, not with unit tests. Each
skill has a checklist of trial invocations run in a scratch project before a
release, with expected properties. Examples:

- A review of a known-bad form must cite at least EV-FORM-003 and the
  relevant contrast claim, and must not cite a claim ID that does not exist.
- A quick-demo output must be a single file per screen with no external
  requests other than the pinned Tailwind CDN.
- Every block file must render correctly when opened directly in a browser.

A failed check means the SKILL.md instructions need tightening; fixes are
made and the checklist is rerun.

## Out of scope for v1

- Design-guide generator skill (deferred, candidate for a later phase).
- React/Vue variants of blocks (users can ask Claude to translate a block,
  guided by the same evidence).
- Any runtime scripts, search tooling, or MCP servers inside the plugin.
- Live web retrieval during skill use.
