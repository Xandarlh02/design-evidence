# design-evidence

A Claude Code plugin for UI/UX work that can show its sources.

Most design advice from AI tools is confident and unsourced. This plugin
takes the opposite approach: it ships a curated library of design best
practices in which every claim carries a citation to a real, publicly
reachable source — WCAG, Nielsen Norman Group, Baymard Institute, GOV.UK
Design System research, platform interface guidelines, Google Search Central,
and web.dev. Claims are labeled honestly: `research-backed` when there is
published data, `standard` when a spec requires it, and `convention` when it
is common practice with no study behind it.

## What you get

- **evidence/** — the knowledge base. Markdown files of claims, each with a
  stable ID (like `EV-FORM-003`), a strength label, and sources you can
  check yourself. Domains covered: forms, accessibility, layout and visual
  hierarchy, usability heuristics, SEO, and landing-page conversion.
- **design-review** — a skill that reviews UI code, screens, or mockups and
  cites the evidence behind every finding. Recommendations it cannot back
  up are labeled as opinion.
- **seo-helper** — a skill that either audits an existing marketing or landing
  page for SEO and conversion problems (with citations), or generates a
  self-contained HTML landing-page mockup with every structural choice
  annotated by its backing claim. Generated pages are throwaway mockups, not
  production code.

## Install

```
/plugin marketplace add xandarlh02/design-evidence
/plugin install design-evidence
```

## Security posture

The plugin contains no executable code — no scripts, no dependencies, no
build step. It installs markdown, JSON, and script-free HTML test fixtures you can read.

## Contributing

Claims live or die by their sources. See CONTRIBUTING.md for the claim
format and the bar a pull request has to meet.
