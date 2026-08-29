# design-evidence Phase 1 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Ship the publishable core of the design-evidence plugin: scaffold, the cited evidence library for forms/conversion and accessibility, and the design-review skill.

**Architecture:** A Claude Code plugin containing zero executable code — only markdown and JSON. A shared `evidence/` library of claims (each with a stable ID, an honesty-labeled strength, and at least one publicly reachable source URL) is consumed by a thin `design-review` skill via `evidence/INDEX.md`.

**Tech Stack:** Markdown, JSON (plugin manifests). No scripts, no dependencies, no build step.

**Spec:** `docs/superpowers/specs/2026-08-28-design-evidence-plugin-design.md` — read it before starting any task.

## Global Constraints

- The plugin ships no executable code: no scripts, no package.json, no build step. Markdown and JSON only.
- All prose (README, CONTRIBUTING, evidence files, SKILL.md) is plain, direct human writing. No emoji decoration, no marketing filler, no generated-sounding boilerplate.
- Every evidence claim carries at least one working, publicly reachable URL. A claim with no verifiable source does not ship.
- Strength labels are exactly one of: `research-backed`, `standard`, `convention`. Convention is never presented as research.
- Claim IDs follow `EV-FORM-NNN` / `EV-A11Y-NNN`, are stable, and are never reused. Gaps in numbering are acceptable (a dropped claim leaves a gap).
- Evidence prose is written in our own words from the fetched source. Never copy paywalled or copyrighted text.
- **Source verification is mandatory:** before writing any claim, WebFetch its URL and confirm the page actually supports the claim. If a URL is dead, find the current canonical location on the same domain (WebSearch). If the source does not support the claim, drop or replace the claim — do not soften the rule.
- Work happens directly in `C:\Users\xanda\Documents\GitHub\design-evidence` on `master`. Commit after every task.

---

### Task 1: Plugin scaffold

**Files:**
- Create: `.claude-plugin/plugin.json`
- Create: `.claude-plugin/marketplace.json`
- Create: `README.md`
- Create: `LICENSE`
- Create: `.gitignore`

**Interfaces:**
- Produces: plugin name `design-evidence` used by all later tasks; directory layout from the spec.

- [ ] **Step 1: Write `.claude-plugin/plugin.json`**

```json
{
  "name": "design-evidence",
  "version": "0.1.0",
  "description": "UI/UX best practices with cited sources. Design reviews that can show their evidence.",
  "author": {
    "name": "xanda"
  }
}
```

- [ ] **Step 2: Write `.claude-plugin/marketplace.json`**

```json
{
  "name": "design-evidence",
  "owner": {
    "name": "xanda"
  },
  "plugins": [
    {
      "name": "design-evidence",
      "source": "./",
      "description": "UI/UX best practices with cited sources. Design reviews that can show their evidence."
    }
  ]
}
```

- [ ] **Step 3: Write `README.md`**

Exact content (update the claim counts in later tasks if they change):

```markdown
# design-evidence

A Claude Code plugin for UI/UX work that can show its sources.

Most design advice from AI tools is confident and unsourced. This plugin
takes the opposite approach: it ships a curated library of design best
practices in which every claim carries a citation to a real, publicly
reachable source — WCAG, Nielsen Norman Group, Baymard Institute, GOV.UK
Design System research, platform interface guidelines. Claims are labeled
honestly: `research-backed` when there is published data, `standard` when a
spec requires it, and `convention` when it is common practice with no study
behind it.

## What you get

- **evidence/** — the knowledge base. Markdown files of claims, each with a
  stable ID (like `EV-FORM-003`), a strength label, and sources you can
  check yourself.
- **design-review** — a skill that reviews UI code, screens, or mockups and
  cites the evidence behind every finding. Recommendations it cannot back
  up are labeled as opinion.

More skills (quick demos, website blocks) are planned; see the specs in
`docs/superpowers/specs/`.

## Install

```
/plugin marketplace add xanda/design-evidence
/plugin install design-evidence
```

## Security posture

The plugin contains no executable code — no scripts, no dependencies, no
build step. Everything it installs is markdown and JSON you can read.

## Contributing

Claims live or die by their sources. See CONTRIBUTING.md for the claim
format and the bar a pull request has to meet.
```

- [ ] **Step 4: Write `LICENSE`** — the standard MIT License text, copyright line: `Copyright (c) 2026 xanda`.

- [ ] **Step 5: Write `.gitignore`**

```
.DS_Store
Thumbs.db
```

- [ ] **Step 6: Verify JSON manifests parse**

Run: `powershell -Command "Get-Content .claude-plugin/plugin.json -Raw | ConvertFrom-Json; Get-Content .claude-plugin/marketplace.json -Raw | ConvertFrom-Json"`
Expected: no error output, objects printed.

- [ ] **Step 7: Commit**

```bash
git add -A
git commit -m "feat: plugin scaffold (manifests, README, license)"
```

---

### Task 2: Claim format in CONTRIBUTING.md and INDEX.md skeleton

**Files:**
- Create: `CONTRIBUTING.md`
- Create: `evidence/INDEX.md`

**Interfaces:**
- Produces: the claim format every evidence task (3–6) must follow verbatim; the INDEX.md structure evidence tasks append to.

- [ ] **Step 1: Write `CONTRIBUTING.md`**

Exact content:

```markdown
# Contributing

This project accepts new claims, corrections, and better sources. The bar
is the same for maintainers and contributors: no source, no ship.

## The claim format

The claim is the atomic unit: one recommendation, one citation block. Every
claim in `evidence/` uses this structure exactly:

    ## EV-FORM-003: Top-aligned labels outperform left-aligned labels
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
- Executable code of any kind. This plugin ships markdown and JSON only.
```

- [ ] **Step 2: Write `evidence/INDEX.md`**

Exact content (evidence tasks replace the placeholder lines as files land):

```markdown
# Evidence index

Skills read this file first, then open only the files relevant to the task.
One line per file: path, scope, claim IDs.

## Forms and conversion

(populated by the forms evidence tasks)

## Accessibility

(populated by the accessibility evidence tasks)
```

- [ ] **Step 3: Verify format is greppable**

Run: `powershell -Command "Select-String -Path CONTRIBUTING.md -Pattern 'EV-FORM-003' | Measure-Object | Select-Object -ExpandProperty Count"`
Expected: `1` or more.

- [ ] **Step 4: Commit**

```bash
git add CONTRIBUTING.md evidence/INDEX.md
git commit -m "feat: claim format rules and evidence index skeleton"
```

---

### Task 3: Forms evidence — labels and validation

**Files:**
- Create: `evidence/forms/labels.md`
- Create: `evidence/forms/validation.md`
- Modify: `evidence/INDEX.md` (Forms section)

**Interfaces:**
- Consumes: claim format from `CONTRIBUTING.md` (Task 2) — follow it exactly.
- Produces: claims EV-FORM-001 through EV-FORM-009, cited by the design-review skill and test fixture.

Candidate claims. For each: WebFetch the URL, confirm the page supports the claim, then write the claim in the format from CONTRIBUTING.md with Evidence text drawn from what the fetched page actually says. If a URL has moved, WebSearch for its current location on the same domain. If a source does not support the claim, drop the claim (leave the ID unused) or find a qualifying replacement source.

`evidence/forms/labels.md`:

| ID | Claim | Strength | Candidate source |
|----|-------|----------|------------------|
| EV-FORM-001 | Top-aligned labels outperform left-aligned labels | research-backed | Penzo, "Label Placement in Forms", UXmatters 2006 — https://www.uxmatters.com/mt/archives/2006/07/label-placement-in-forms.php |
| EV-FORM-002 | Do not use placeholder text as the only label | research-backed | NN/g, "Placeholders in Form Fields Are Harmful" — https://www.nngroup.com/articles/form-design-placeholders/ |
| EV-FORM-003 | Keep labels visible at all times (avoid disappearing labels) | research-backed | Same NN/g placeholder research plus NN/g form design guidelines — https://www.nngroup.com/articles/web-form-design/ |
| EV-FORM-004 | Mark optional fields rather than required ones when most fields are required | research-backed | Baymard, "Marking Required vs. Optional fields" — https://baymard.com/blog/required-optional-form-fields |

`evidence/forms/validation.md`:

| ID | Claim | Strength | Candidate source |
|----|-------|----------|------------------|
| EV-FORM-005 | Validate inline after the user leaves a field, not on every keystroke | research-backed | NN/g, "How to Report Errors in Forms" — https://www.nngroup.com/articles/errors-forms-design-guidelines/ |
| EV-FORM-006 | Error messages must say what went wrong and how to fix it, in plain language | research-backed | NN/g, "Error Message Guidelines" — https://www.nngroup.com/articles/error-message-guidelines/ |
| EV-FORM-007 | Do not signal errors with color alone | standard | WCAG 2.2 SC 1.4.1 Use of Color — https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html |
| EV-FORM-008 | Preserve the user's input when showing an error | research-backed | GOV.UK Design System, error message guidance — https://design-system.service.gov.uk/components/error-message/ |
| EV-FORM-009 | On long forms, show an error summary at the top linking to each error | research-backed | GOV.UK Design System, error summary component (user-research backed) — https://design-system.service.gov.uk/components/error-summary/ |

- [ ] **Step 1: Verify all candidate sources.** WebFetch each URL above; record for each whether it supports the claim. Adjust strength labels honestly based on what the page actually contains (e.g. if GOV.UK guidance is design-system guidance without published data, label it `standard` or `convention`, not `research-backed`).
- [ ] **Step 2: Write `evidence/forms/labels.md`** — a one-paragraph file intro (what the file covers), then the verified claims in ID order, format per CONTRIBUTING.md.
- [ ] **Step 3: Write `evidence/forms/validation.md`** — same structure.
- [ ] **Step 4: Update `evidence/INDEX.md`** — replace the Forms placeholder with one line per file, e.g. `- evidence/forms/labels.md — label placement and visibility — EV-FORM-001..004` (list actual shipped IDs).
- [ ] **Step 5: Format lint.** Run: `powershell -Command "(Select-String -Path evidence/forms/*.md -Pattern '\*\*Strength:\*\* (research-backed|standard|convention)').Count; (Select-String -Path evidence/forms/*.md -Pattern '^## EV-FORM-').Count"`
Expected: the two numbers are equal (every claim has a valid strength label).
- [ ] **Step 6: Commit**

```bash
git add evidence/
git commit -m "feat: forms evidence - labels and validation (EV-FORM-001..009)"
```

---

### Task 4: Forms evidence — checkout and calls to action

**Files:**
- Create: `evidence/forms/checkout.md`
- Create: `evidence/forms/cta.md`
- Modify: `evidence/INDEX.md` (Forms section)

**Interfaces:**
- Consumes: claim format from `CONTRIBUTING.md`; ID sequence continues from Task 3.
- Produces: claims EV-FORM-010 through EV-FORM-016.

Same verification procedure as Task 3 (WebFetch every URL before writing; adjust or drop honestly).

`evidence/forms/checkout.md`:

| ID | Claim | Strength | Candidate source |
|----|-------|----------|------------------|
| EV-FORM-010 | Offer guest checkout; forced account creation causes abandonment | research-backed | Baymard, "Cart Abandonment Rate Statistics" (reasons survey) — https://baymard.com/lists/cart-abandonment-rate |
| EV-FORM-011 | Show all costs (shipping, tax, fees) as early as possible; surprise costs are the top abandonment reason | research-backed | Same Baymard abandonment statistics page |
| EV-FORM-012 | Minimize the number of form fields in checkout | research-backed | Baymard, "Checkout Flow Average Form Fields" — https://baymard.com/blog/checkout-flow-average-form-fields |
| EV-FORM-013 | Use a single-column layout for forms | research-backed | Baymard, "Avoid Multi-Column Forms" — https://baymard.com/blog/avoid-multi-column-forms |

`evidence/forms/cta.md`:

| ID | Claim | Strength | Candidate source |
|----|-------|----------|------------------|
| EV-FORM-014 | Button labels should describe the action, not say "Submit" or "Learn more" | research-backed | NN/g, "'Learn More' Links: You Can Do Better" — https://www.nngroup.com/articles/learn-more-links/ |
| EV-FORM-015 | One visually dominant primary action per screen; secondary actions styled subordinate | convention | Material Design, buttons guidance — https://m3.material.io/components/buttons/guidelines |
| EV-FORM-016 | Interactive controls must meet minimum target size (see EV-A11Y-009/010 for the normative values) | standard | WCAG 2.2 SC 2.5.8 Target Size (Minimum) — https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html |

- [ ] **Step 1: Verify all candidate sources** (WebFetch each; adjust strength labels or drop claims honestly).
- [ ] **Step 2: Write `evidence/forms/checkout.md`** — intro paragraph plus verified claims.
- [ ] **Step 3: Write `evidence/forms/cta.md`** — same. EV-FORM-016 must reference EV-A11Y-009 and EV-A11Y-010 as the normative source of the pixel values (written in Task 5's follow-up, Task 6 — a forward reference in text is fine).
- [ ] **Step 4: Update `evidence/INDEX.md`** with the two new files and their shipped IDs.
- [ ] **Step 5: Format lint.** Same command as Task 3 Step 5; the two counts must still be equal across `evidence/forms/*.md`.
- [ ] **Step 6: Commit**

```bash
git add evidence/
git commit -m "feat: forms evidence - checkout and CTAs (EV-FORM-010..016)"
```

---

### Task 5: Accessibility evidence — contrast and focus

**Files:**
- Create: `evidence/accessibility/contrast.md`
- Create: `evidence/accessibility/focus.md`
- Modify: `evidence/INDEX.md` (Accessibility section)

**Interfaces:**
- Consumes: claim format from `CONTRIBUTING.md`.
- Produces: claims EV-A11Y-001 through EV-A11Y-008.

Same verification procedure as Task 3. WCAG claims cite the Understanding documents; they are `standard` strength by definition.

`evidence/accessibility/contrast.md`:

| ID | Claim | Strength | Candidate source |
|----|-------|----------|------------------|
| EV-A11Y-001 | Body text needs a contrast ratio of at least 4.5:1 against its background | standard | WCAG 2.2 SC 1.4.3 — https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html |
| EV-A11Y-002 | Large text (24px+, or 18.5px+ bold) needs at least 3:1 | standard | Same SC 1.4.3 Understanding document |
| EV-A11Y-003 | UI component boundaries and graphical objects need at least 3:1 | standard | WCAG 2.2 SC 1.4.11 Non-text Contrast — https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html |
| EV-A11Y-004 | Never convey information by color alone | standard | WCAG 2.2 SC 1.4.1 — https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html |

`evidence/accessibility/focus.md`:

| ID | Claim | Strength | Candidate source |
|----|-------|----------|------------------|
| EV-A11Y-005 | Keyboard focus must be visibly indicated; never remove outlines without a replacement | standard | WCAG 2.2 SC 2.4.7 Focus Visible — https://www.w3.org/WAI/WCAG22/Understanding/focus-visible.html |
| EV-A11Y-006 | Focus order must follow the meaning and reading order of the page | standard | WCAG 2.2 SC 2.4.3 Focus Order — https://www.w3.org/WAI/WCAG22/Understanding/focus-order.html |
| EV-A11Y-007 | Keyboard users must never get trapped in a component | standard | WCAG 2.2 SC 2.1.2 No Keyboard Trap — https://www.w3.org/WAI/WCAG22/Understanding/no-keyboard-trap.html |
| EV-A11Y-008 | All functionality must be operable by keyboard alone | standard | WCAG 2.2 SC 2.1.1 Keyboard — https://www.w3.org/WAI/WCAG22/Understanding/keyboard.html |

- [ ] **Step 1: Verify all candidate sources** (WebFetch each Understanding page; confirm SC numbers and thresholds are as stated — copy thresholds from the page, not from memory).
- [ ] **Step 2: Write `evidence/accessibility/contrast.md`** — intro paragraph plus verified claims.
- [ ] **Step 3: Write `evidence/accessibility/focus.md`** — same.
- [ ] **Step 4: Update `evidence/INDEX.md`** Accessibility section with the two files and shipped IDs.
- [ ] **Step 5: Format lint.** Run the Task 3 Step 5 command with path `evidence/accessibility/*.md` and pattern `^## EV-A11Y-`; counts must be equal.
- [ ] **Step 6: Commit**

```bash
git add evidence/
git commit -m "feat: accessibility evidence - contrast and focus (EV-A11Y-001..008)"
```

---

### Task 6: Accessibility evidence — touch targets and semantics/ARIA

**Files:**
- Create: `evidence/accessibility/touch-targets.md`
- Create: `evidence/accessibility/aria.md`
- Modify: `evidence/INDEX.md` (Accessibility section)

**Interfaces:**
- Consumes: claim format; ID sequence continues from Task 5. EV-FORM-016 (Task 4) references EV-A11Y-009/010 — those IDs must exist with the normative target-size values.
- Produces: claims EV-A11Y-009 through EV-A11Y-016.

`evidence/accessibility/touch-targets.md`:

| ID | Claim | Strength | Candidate source |
|----|-------|----------|------------------|
| EV-A11Y-009 | Interactive targets must be at least 24x24 CSS px (WCAG AA minimum) | standard | WCAG 2.2 SC 2.5.8 Target Size (Minimum) — https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html |
| EV-A11Y-010 | Platform guidelines recommend larger targets: 44x44pt (Apple), 48x48dp (Material) | standard | Apple HIG — https://developer.apple.com/design/human-interface-guidelines/accessibility ; Material Design accessibility — https://m2.material.io/design/usability/accessibility.html |
| EV-A11Y-011 | Provide spacing between adjacent small targets so mis-taps hit nothing rather than the wrong thing | standard | Same SC 2.5.8 Understanding document (spacing exception) |

`evidence/accessibility/aria.md`:

| ID | Claim | Strength | Candidate source |
|----|-------|----------|------------------|
| EV-A11Y-012 | Prefer native HTML elements over ARIA roles (the first rule of ARIA) | standard | W3C, "Using ARIA", Rule 1 — https://www.w3.org/TR/using-aria/#rule1 |
| EV-A11Y-013 | Every input needs a programmatically associated label | standard | WCAG 2.2 SC 1.3.1 / 4.1.2 — https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships.html |
| EV-A11Y-014 | Informative images need meaningful alt text; decorative images need empty alt | standard | WCAG 2.2 SC 1.1.1 — https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html and W3C image tutorial — https://www.w3.org/WAI/tutorials/images/ |
| EV-A11Y-015 | Use a logical heading hierarchy; screen reader users navigate by headings | research-backed | WebAIM Screen Reader User Survey (headings as primary navigation) — https://webaim.org/projects/screenreadersurvey10/ |
| EV-A11Y-016 | Announce dynamic content updates with ARIA live regions | standard | W3C ARIA Authoring Practices Guide — https://www.w3.org/WAI/ARIA/apg/practices/ |

- [ ] **Step 1: Verify all candidate sources** (WebFetch each; for EV-A11Y-010 confirm the current pt/dp values on the actual pages; for EV-A11Y-015 confirm the survey actually reports heading navigation prevalence and cite the number).
- [ ] **Step 2: Write `evidence/accessibility/touch-targets.md`** — intro paragraph plus verified claims.
- [ ] **Step 3: Write `evidence/accessibility/aria.md`** — same.
- [ ] **Step 4: Update `evidence/INDEX.md`** with the two files and shipped IDs. At this point the index must list all six evidence files and contain no placeholder lines.
- [ ] **Step 5: Format lint.** Task 5 Step 5 command across `evidence/accessibility/*.md`; counts equal. Also run: `powershell -Command "Select-String -Path evidence/INDEX.md -Pattern 'populated by'"` — Expected: no matches.
- [ ] **Step 6: Commit**

```bash
git add evidence/
git commit -m "feat: accessibility evidence - targets and ARIA (EV-A11Y-009..016)"
```

---

### Task 7: design-review skill

**Files:**
- Create: `skills/design-review/SKILL.md`

**Interfaces:**
- Consumes: `evidence/INDEX.md` and the evidence files (Tasks 3–6); claim ID scheme.
- Produces: the skill users invoke; the behavior Task 8 verifies.

- [ ] **Step 1: Write `skills/design-review/SKILL.md`**

Exact content:

```markdown
---
name: design-review
description: Use when reviewing UI code, screens, mockups, or design decisions for usability, conversion, and accessibility problems - reports findings backed by cited evidence from this plugin's evidence library, and never invents sources
---

# Design Review

Review UI against the evidence library in this plugin. Every finding you
report must either cite a claim from the library or be labeled as opinion.

## Hard rules

- NEVER invent a claim ID, a source, a statistic, or a study. If the
  library has no claim for a finding, label the finding
  "opinion — no citation" and say so plainly.
- Cite claims by ID and source name, e.g. "(EV-FORM-002, NN/g)". Only cite
  IDs you have actually read in this session.
- Do not dump every rule you read. Report what is wrong with THIS UI,
  ordered by user impact.

## Workflow

1. Identify what you are reviewing: what kind of UI is it (form, checkout,
   dashboard, landing page, navigation), and in what form (code files, a
   screenshot, a description)? If you were not told what to review, ask.
2. Read `evidence/INDEX.md` in this plugin's directory. Pick the 2-4
   evidence files whose scope matches the UI. Read those files fully.
   Do not read evidence files that are irrelevant to the UI at hand.
3. Examine the UI systematically against each claim you read: labels,
   validation, layout, actions, contrast, keyboard access, semantics,
   target sizes. For code, read the actual markup and styles; do not guess.
4. Write the review.

## Output format

A readable review, not a rule dump:

- One short paragraph: what was reviewed and the overall state.
- Findings ordered by user impact, each with: what is wrong, where
  (file:line for code), what to do instead, and the citation
  "(EV-XXXX-NNN, Source)". A finding with no supporting claim is labeled
  "opinion — no citation".
- If something is done well and a claim supports it, one short "what's
  already right" list at the end — cited the same way.

Keep the whole review proportionate: a small component gets a short
review. Do not pad.
```

- [ ] **Step 2: Verify frontmatter and cross-references**

Run: `powershell -Command "Select-String -Path skills/design-review/SKILL.md -Pattern 'INDEX.md'; Select-String -Path skills/design-review/SKILL.md -Pattern '^name: design-review'"`
Expected: both patterns found.

- [ ] **Step 3: Commit**

```bash
git add skills/
git commit -m "feat: design-review skill"
```

---

### Task 8: Behavioral verification fixture and release checklist

**Files:**
- Create: `tests/fixtures/bad-form.html`
- Create: `tests/CHECKLIST.md`

**Interfaces:**
- Consumes: shipped claim IDs from Tasks 3–6, the design-review skill from Task 7.
- Produces: the pre-release verification assets named in the spec's Testing section.

- [ ] **Step 1: Write `tests/fixtures/bad-form.html`** — a small standalone signup form that deliberately violates specific shipped claims. Exact content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Sign up</title>
  <style>
    body { font-family: sans-serif; background: #ffffff; }
    form { width: 640px; display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
    input { border: 1px solid #eeeeee; padding: 2px; outline: none; }
    input:focus { outline: none; }
    .error { color: red; }
    button { background: #a8d5a8; color: #cfe8cf; border: none; padding: 3px 6px; font-size: 11px; }
  </style>
</head>
<body>
  <!-- Deliberate violations, for behavioral testing of the design-review
       skill. Expected findings are listed in tests/CHECKLIST.md. -->
  <form>
    <input type="text" placeholder="First name">
    <input type="text" placeholder="Last name">
    <input type="email" placeholder="Email">
    <input type="password" placeholder="Password">
    <span class="error">Invalid.</span>
    <button type="submit">Submit</button>
  </form>
</body>
</html>
```

- [ ] **Step 2: Write `tests/CHECKLIST.md`** — the pre-release behavioral checks. Exact content (adjust IDs only if earlier tasks shipped different ones):

```markdown
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

## Evidence library

5. Every URL in `evidence/` resolves (fetch each; fix or remove dead ones).
6. Format lint passes: the number of `**Strength:**` lines equals the
   number of `## EV-` headings in every evidence file.
```

- [ ] **Step 3: Run the self-check now (in-session approximation of checks 2, 3, 6).** Follow the design-review workflow against `tests/fixtures/bad-form.html`; write the review to the chat, then grep every cited ID: `powershell -Command "Select-String -Path evidence/*/*.md -Pattern '^## EV-' | ForEach-Object { $_.Line }"` and confirm each cited ID appears and the eight expected findings were made. If any expected finding was missed, tighten `skills/design-review/SKILL.md` (usually the workflow's step 3 list) and retry.
- [ ] **Step 4: Commit**

```bash
git add tests/
git commit -m "test: behavioral fixture and pre-release checklist"
```
