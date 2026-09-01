# Layout/UX Evidence, Holistic Review, and seo-helper — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add layout/visual-hierarchy and usability-heuristics evidence so `design-review` can judge whole-page UI/UX, and add a new `seo-helper` skill that audits or generates evidence-cited SEO/marketing landing pages.

**Architecture:** No new architectural pattern. This extends the existing plugin: a shared, cited evidence library (`evidence/`) consumed by thin skills (`skills/*/SKILL.md`). Four new claim prefixes (`EV-LAYOUT`, `EV-HEUR`, `EV-SEO`, `EV-CONV`) are authored to the existing claim format and sourcing bar; the review skill gains a holistic layout pass; the new skill reads that evidence and either reviews a page or generates one self-contained HTML mockup.

**Tech Stack:** Markdown (evidence + skills), JSON (plugin manifests), script-free HTML fixtures. Generated landing pages are self-contained HTML with the pinned Tailwind CDN. No executable code ships in the plugin. Authoring tools: WebFetch (fetch/verify sources), Bash git-bash (format lint, commits).

**Spec:** `docs/superpowers/specs/2026-08-31-layout-heuristics-and-seo-design.md`

## Global Constraints

Copied verbatim from the spec and the existing CONTRIBUTING.md / claim format. Every task implicitly includes these.

- **No source, no ship.** Every claim carries at least one working, publicly reachable URL. Fetch and read the source before writing the claim; write the Evidence line in your own words from what the source actually says. Never cite from memory or from a summary of a summary. A claim whose fetched source does not support it is dropped, not shipped.
- **Never invent** a claim ID, source, statistic, or study.
- **Strength is exactly one of:** `research-backed` (published study / measured data), `standard` (a normative spec — WCAG, a platform HIG), `convention` (widely adopted practice, no controlled study). Do not dress convention up as research. When a candidate source turns out weaker than the target strength below, downgrade the label honestly.
- **Qualifying sources only:** W3C/WCAG, Nielsen Norman Group, Baymard free articles, GOV.UK Design System/Service Manual, platform interface guidelines (Apple, Material), Google Search Central official docs, web.dev, published papers, Butterick's Practical Typography (free web book). Secondhand blog/vendor-marketing posts do not qualify.
- **Claim format, exactly:**
  ```
  ## EV-<PREFIX>-<NNN>: <one-line title>
  **Strength:** <research-backed | standard | convention>
  **Claim:** <the recommendation, imperative, 1-3 sentences>
  **Evidence:** <what the source found/requires, your own words, 1-3 sentences>
  **Sources:**
  - Author/Org, "Title", Year — https://url
  **Applies when:** <context where this holds>
  **Exception:** <known cases where it does not — omit the line if none>
  ```
- **Claim IDs** (`EV-<PREFIX>-<NNN>`) are stable, sequential, never reused. A dropped claim leaves a numbering gap; do not renumber.
- **Update `evidence/INDEX.md` in the same commit** as any claim add/change/remove (CONTRIBUTING rule 6).
- **Prose standard:** plain, direct writing. No emoji, no marketing filler, no generated-sounding boilerplate.
- **Author/owner** in any manifest or attribution is `xandarlh02`.

### Format lint (the per-file "test" for every evidence task)

After writing an evidence file, run this in the Bash tool (git-bash) and confirm the two numbers are equal and match the number of claims you wrote:

```bash
f=evidence/<path>.md
echo "headings: $(grep -c '^## EV-' "$f")  strength: $(grep -c '^\*\*Strength:\*\*' "$f")"
```

Expected: `headings` == `strength` == the claim count for that file. If they differ, a claim is malformed — fix before committing.

### URL check (the per-file source "test")

For each URL in the file, fetch it with WebFetch and confirm it resolves and supports the claim. If a URL is dead or does not support the claim, replace the source or drop the claim. Do not commit a file with an unverified URL.

---

## Task 1: Layout evidence — visual hierarchy

**Files:**
- Create: `evidence/layout/hierarchy.md`
- Modify: `evidence/INDEX.md`

**Interfaces:**
- Produces: claim IDs `EV-LAYOUT-001`, `EV-LAYOUT-002`, `EV-LAYOUT-003` (cited later by `design-review` and `seo-helper`).

Author three claims. For each: fetch the candidate source(s), confirm support, write to the claim format, set the honest strength.

- [ ] **Step 1: Fetch sources**
  - EV-LAYOUT-001 & 002 candidate: NN/g, "Visual Hierarchy in UX: Definition" — https://www.nngroup.com/articles/visual-hierarchy-ux-definition/
  - EV-LAYOUT-003 candidate: NN/g, "Principle of Common Region" — https://www.nngroup.com/articles/common-region/ (grouping via a shared container/hierarchy). If it does not support a single-focal-point claim, fall back to the visual-hierarchy article above.

  Fetch each with WebFetch and read what it actually claims before writing.

- [ ] **Step 2: Write `evidence/layout/hierarchy.md`**

  File intro paragraph (1-3 sentences) describing scope, then:
  - `## EV-LAYOUT-001: Establish a clear visual hierarchy` — Strength `convention`. Claim: use size, weight, colour, and contrast so the most important element is seen first and the eye moves through the screen in priority order. Applies when: any screen with more than a few elements.
  - `## EV-LAYOUT-002: Give each view one dominant focal point` — Strength `convention`. Claim: make a single element clearly dominant per view; competing equal-weight elements flatten the hierarchy and slow scanning. Applies when: landing pages, hero sections, primary task screens.
  - `## EV-LAYOUT-003: Match visual prominence to task priority` — Strength `convention`. Claim: the most visually prominent element should be the highest-priority action or information, not decoration. Applies when: any task-oriented UI.

  Write each `**Evidence:**` line from the fetched source in your own words. If the source only supports a weaker or narrower statement, narrow the claim to fit.

- [ ] **Step 3: Update `evidence/INDEX.md`**

  Under the "Accessibility" section add a new `## Layout and visual hierarchy` section (place it after Forms, before Accessibility, to group conversion-adjacent topics — or after Accessibility; either is fine, keep sections alphabetical-ish and consistent). Add one line:
  ```
  - evidence/layout/hierarchy.md — visual hierarchy, single focal point, prominence matches task priority — EV-LAYOUT-001, EV-LAYOUT-002, EV-LAYOUT-003
  ```

- [ ] **Step 4: Format lint + URL check**

  Run the format lint (expect headings == strength == 3). Fetch every URL in the file; confirm each resolves and supports its claim.

- [ ] **Step 5: Commit**
  ```bash
  git add evidence/layout/hierarchy.md evidence/INDEX.md
  git commit -m "feat: layout evidence - visual hierarchy (EV-LAYOUT-001..003)"
  ```

---

## Task 2: Layout evidence — spacing and grouping

**Files:**
- Create: `evidence/layout/spacing.md`
- Modify: `evidence/INDEX.md`

**Interfaces:**
- Produces: `EV-LAYOUT-004`, `EV-LAYOUT-005`, `EV-LAYOUT-006`.

- [ ] **Step 1: Fetch sources**
  - EV-LAYOUT-004 & 005 candidate: NN/g, "Proximity Principle in Visual Design" — https://www.nngroup.com/articles/gestalt-proximity/
  - EV-LAYOUT-006 candidate (spacing scale as consistency): NN/g, "Design Consistency" — https://www.nngroup.com/articles/consistency-and-standards/ ; or GOV.UK Design System spacing guidance — https://design-system.service.gov.uk/styles/spacing/ . Fetch and use whichever actually supports "use a single consistent spacing scale".

- [ ] **Step 2: Write `evidence/layout/spacing.md`**
  - `## EV-LAYOUT-004: Group related elements with proximity` — Strength `research-backed` if the NN/g proximity article cites the Gestalt research; otherwise `convention`. Claim: place related controls and content close together and separate unrelated groups with more space; proximity communicates relationship before any label is read. Applies when: forms, toolbars, card layouts, any grouped content.
  - `## EV-LAYOUT-005: Use whitespace to separate, not borders alone` — Strength `convention`. Claim: prefer adequate spacing over heavy dividers/boxes to structure a layout; sufficient whitespace reduces clutter and improves comprehension. Applies when: content-dense pages. Exception: data tables and dense enterprise grids where space is scarce.
  - `## EV-LAYOUT-006: Use a single consistent spacing scale` — Strength `convention`. Claim: derive margins and padding from one limited spacing scale rather than ad-hoc values; consistent rhythm is easier to scan and signals quality. Applies when: any multi-component UI.

- [ ] **Step 3: Update `evidence/INDEX.md`**
  ```
  - evidence/layout/spacing.md — proximity grouping, whitespace over borders, consistent spacing scale — EV-LAYOUT-004, EV-LAYOUT-005, EV-LAYOUT-006
  ```

- [ ] **Step 4: Format lint + URL check** (expect 3)

- [ ] **Step 5: Commit**
  ```bash
  git add evidence/layout/spacing.md evidence/INDEX.md
  git commit -m "feat: layout evidence - spacing and grouping (EV-LAYOUT-004..006)"
  ```

---

## Task 3: Layout evidence — typography and readability

**Files:**
- Create: `evidence/layout/typography.md`
- Modify: `evidence/INDEX.md`

**Interfaces:**
- Produces: `EV-LAYOUT-007`, `EV-LAYOUT-008`, `EV-LAYOUT-009`.

- [ ] **Step 1: Fetch sources**
  - EV-LAYOUT-007 (line length / measure) candidate: Butterick, "Line length", Practical Typography — https://practicaltypography.com/line-length.html (recommends ~45–90 chars, 2–3 alphabets). Co-source: W3C WCAG 2.1 "Understanding SC 1.4.8 Visual Presentation" — https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation.html (width no more than 80 characters).
  - EV-LAYOUT-008 (line spacing / leading) candidate: same WCAG 1.4.8 Understanding page (line spacing at least 1.5 within paragraphs).
  - EV-LAYOUT-009 (limited type scale) candidate: Butterick, "Summary of key rules" / "Font recommendations" — https://practicaltypography.com/summary-of-key-rules.html ; use it for "use a small number of sizes/weights". If it does not support that phrasing, label `convention` with the general Butterick body-text guidance.

- [ ] **Step 2: Write `evidence/layout/typography.md`**
  - `## EV-LAYOUT-007: Keep body line length in a readable range` — Strength `standard` (WCAG 1.4.8 is normative for the 80-char ceiling) — state the ~45–75/80 character range and cite both sources; note WCAG 1.4.8 is a AAA success criterion. Applies when: paragraphs of running text. Exception: single-line inputs, captions, data cells.
  - `## EV-LAYOUT-008: Use adequate line spacing for body text` — Strength `standard`. Claim: set paragraph line-height to at least ~1.5× the font size for running text. Cite WCAG 1.4.8. Applies when: body copy.
  - `## EV-LAYOUT-009: Limit the type scale` — Strength `convention`. Claim: use a small, deliberate set of font sizes and weights to build hierarchy; unlimited sizes read as noise. Applies when: any UI with text hierarchy.

- [ ] **Step 3: Update `evidence/INDEX.md`**
  ```
  - evidence/layout/typography.md — readable line length, line spacing, limited type scale — EV-LAYOUT-007, EV-LAYOUT-008, EV-LAYOUT-009
  ```

- [ ] **Step 4: Format lint + URL check** (expect 3; verify the WCAG anchor and both Butterick pages resolve)

- [ ] **Step 5: Commit**
  ```bash
  git add evidence/layout/typography.md evidence/INDEX.md
  git commit -m "feat: layout evidence - typography and readability (EV-LAYOUT-007..009)"
  ```

---

## Task 4: Layout evidence — scanning and alignment

**Files:**
- Create: `evidence/layout/scanning.md`
- Modify: `evidence/INDEX.md`

**Interfaces:**
- Produces: `EV-LAYOUT-010`, `EV-LAYOUT-011`, `EV-LAYOUT-012`.

- [ ] **Step 1: Fetch sources**
  - EV-LAYOUT-010 (F-pattern) candidate: NN/g, "F-Shaped Pattern of Reading on the Web: Misunderstood, But Still Relevant" — https://www.nngroup.com/articles/f-shaped-pattern-reading-web-content/
  - EV-LAYOUT-011 (front-load important words) candidate: NN/g, "How Users Read on the Web" — https://www.nngroup.com/articles/how-users-read-on-the-web/
  - EV-LAYOUT-012 (left-alignment / no justified text) candidate: WCAG 1.4.8 Understanding (text not justified) — https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation.html ; co-source Butterick — https://practicaltypography.com/text-alignment.html

- [ ] **Step 2: Write `evidence/layout/scanning.md`**
  - `## EV-LAYOUT-010: Design for F-pattern scanning` — Strength `research-backed`. Claim: users scan text-heavy pages in an F/layer-cake pattern; put the most important content top and left and in the first words of headings and paragraphs. Applies when: content pages, search results, articles. Exception: pages designed to interrupt scanning with strong visual hierarchy can redirect gaze.
  - `## EV-LAYOUT-011: Front-load the important words` — Strength `research-backed`. Claim: start headings, links, and paragraphs with the information-carrying words; users read the first two words and skip the rest. Applies when: headings, links, list items, body copy.
  - `## EV-LAYOUT-012: Left-align running text; avoid justified text` — Strength `standard` (WCAG 1.4.8 prohibits justified for the AAA criterion). Claim: left-align body text for LTR reading and avoid full justification, which creates uneven "rivers" of space that impede reading. Applies when: running body text. Exception: short centred display text (a single headline) is fine.

- [ ] **Step 3: Update `evidence/INDEX.md`**
  ```
  - evidence/layout/scanning.md — F-pattern scanning, front-loading key words, left-alignment over justified — EV-LAYOUT-010, EV-LAYOUT-011, EV-LAYOUT-012
  ```

- [ ] **Step 4: Format lint + URL check** (expect 3)

- [ ] **Step 5: Commit**
  ```bash
  git add evidence/layout/scanning.md evidence/INDEX.md
  git commit -m "feat: layout evidence - scanning and alignment (EV-LAYOUT-010..012)"
  ```

---

## Task 5: Usability heuristics evidence — Nielsen's 10

**Files:**
- Create: `evidence/ux-heuristics/heuristics.md`
- Modify: `evidence/INDEX.md`

**Interfaces:**
- Produces: `EV-HEUR-001` … `EV-HEUR-010` (the holistic lens `design-review` applies to whole screens).

- [ ] **Step 1: Fetch source**

  NN/g, "10 Usability Heuristics for User Interface Design", 1994/updated — https://www.nngroup.com/articles/ten-usability-heuristics/ . One article covers all ten; fetch and read each heuristic's summary before writing.

- [ ] **Step 2: Write `evidence/ux-heuristics/heuristics.md`**

  Intro paragraph noting these are expert-distilled heuristics (labeled `convention`), useful as a whole-screen checklist. Then one claim per heuristic, all Strength `convention`, all citing the single NN/g URL, each `**Applies when:** any interactive UI` (adjust per heuristic if the source scopes it):
  - `## EV-HEUR-001: Visibility of system status`
  - `## EV-HEUR-002: Match between the system and the real world`
  - `## EV-HEUR-003: User control and freedom`
  - `## EV-HEUR-004: Consistency and standards`
  - `## EV-HEUR-005: Error prevention`
  - `## EV-HEUR-006: Recognition rather than recall`
  - `## EV-HEUR-007: Flexibility and efficiency of use`
  - `## EV-HEUR-008: Aesthetic and minimalist design`
  - `## EV-HEUR-009: Help users recognize, diagnose, and recover from errors`
  - `## EV-HEUR-010: Help and documentation`

  For each, write the `**Claim:**` as an actionable directive and `**Evidence:**` as NN/g's definition in your own words.

- [ ] **Step 3: Update `evidence/INDEX.md`**

  Add section `## Usability heuristics`:
  ```
  - evidence/ux-heuristics/heuristics.md — Nielsen's 10 usability heuristics as a whole-screen review lens — EV-HEUR-001, EV-HEUR-002, EV-HEUR-003, EV-HEUR-004, EV-HEUR-005, EV-HEUR-006, EV-HEUR-007, EV-HEUR-008, EV-HEUR-009, EV-HEUR-010
  ```

- [ ] **Step 4: Format lint + URL check** (expect headings == strength == 10; the one URL resolves)

- [ ] **Step 5: Commit**
  ```bash
  git add evidence/ux-heuristics/heuristics.md evidence/INDEX.md
  git commit -m "feat: usability heuristics evidence - Nielsen 10 (EV-HEUR-001..010)"
  ```

---

## Task 6: Upgrade design-review with a whole-view layout pass

This task makes the layout capability usable and is the first shippable milestone.

**Files:**
- Modify: `skills/design-review/SKILL.md`
- Create: `tests/fixtures/bad-landing.html`
- Modify: `tests/CHECKLIST.md`

**Interfaces:**
- Consumes: `EV-LAYOUT-001..012`, `EV-HEUR-001..010` (Tasks 1–5).

- [ ] **Step 1: Edit `skills/design-review/SKILL.md` — workflow step 2 (evidence selection)**

  Extend the existing step 2 so that when the target is a full screen/page (not an isolated component), the skill also reads `evidence/layout/*` and `evidence/ux-heuristics/heuristics.md`. Keep the "don't read irrelevant files" instruction. Exact replacement text for the file-selection sentence:
  > Pick the 2–4 evidence files whose scope matches the UI. When you are reviewing a whole screen or page (not a single isolated component), also read the `evidence/layout/` files and `evidence/ux-heuristics/heuristics.md`, because layout and heuristics apply to the page as a whole.

- [ ] **Step 2: Edit `skills/design-review/SKILL.md` — add a holistic pass to the workflow**

  Insert a new workflow step before the current "Examine the UI systematically…" step:
  > **Whole-view layout pass (full pages only).** Before component-level checks, evaluate the screen as a whole: is there a clear visual hierarchy and a single dominant focal point (EV-LAYOUT-001, EV-LAYOUT-002)? Are related elements grouped and is spacing consistent (EV-LAYOUT-004, EV-LAYOUT-006)? Does the reading/scan order match task priority (EV-LAYOUT-003, EV-LAYOUT-010, EV-LAYOUT-011)? Run the Nielsen-10 lens (EV-HEUR-001..010) over the screen and note any heuristic the UI violates. Report these with the same citation rules as everything else; a layout problem with no supporting claim is still "opinion — no citation".

  Renumber subsequent steps.

- [ ] **Step 3: Verify the description still fits**

  Confirm the frontmatter `description` still reads correctly (it already says "usability, conversion, and accessibility problems" and "layout"); no change required unless it now misrepresents scope. Leave it unless wrong.

- [ ] **Step 4: Create `tests/fixtures/bad-landing.html`**

  A script-free, self-contained HTML landing page with deliberate whole-page problems for the review to catch: no `<h1>` (or multiple competing `<h1>`s), a buried/low-prominence primary CTA competing with several equal-weight buttons, no clear value proposition above the fold, body text in a full-width single line (>100 chars), justified text, and cramped/undifferentiated spacing. No inline scripts. Add an HTML comment at top: `<!-- deliberately bad landing page fixture for design-review layout pass; not production code -->`.

- [ ] **Step 5: Add checklist entries to `tests/CHECKLIST.md`**

  Under a new `## design-review — layout pass` heading:
  ```
  8. Ask for a design review of `tests/fixtures/bad-landing.html`. The review must:
     - flag the weak/absent visual hierarchy or missing dominant focal point (cite EV-LAYOUT-001 or EV-LAYOUT-002),
     - flag the over-long / justified body text (cite EV-LAYOUT-007 or EV-LAYOUT-012),
     - raise at least one Nielsen heuristic finding (cite an EV-HEUR-0NN id),
     - cite no claim ID that does not exist in evidence/.
  ```

- [ ] **Step 6: Behavioral verification**

  In a scratch session with the plugin, run checklist item 8 against the new fixture. Confirm the review cites at least one real `EV-LAYOUT` id and one real `EV-HEUR` id and invents nothing. If it does not, tighten the SKILL.md wording and rerun. (If running the skill live is not available in this session, verify by reading the updated SKILL.md end-to-end and confirming every claim ID it references exists via grep.)

  ```bash
  for id in EV-LAYOUT-001 EV-LAYOUT-002 EV-LAYOUT-003 EV-LAYOUT-004 EV-LAYOUT-006 EV-LAYOUT-007 EV-LAYOUT-010 EV-LAYOUT-011 EV-LAYOUT-012; do grep -rq "## $id:" evidence/ && echo "$id ok" || echo "$id MISSING"; done
  for n in 001 002 003 004 005 006 007 008 009 010; do grep -rq "## EV-HEUR-$n:" evidence/ && echo "EV-HEUR-$n ok" || echo "EV-HEUR-$n MISSING"; done
  ```
  Expected: all `ok`.

- [ ] **Step 7: Commit**
  ```bash
  git add skills/design-review/SKILL.md tests/fixtures/bad-landing.html tests/CHECKLIST.md
  git commit -m "feat: design-review whole-view layout pass + landing fixture"
  ```

---

## Task 7: SEO evidence — on-page

**Files:**
- Create: `evidence/seo/on-page.md`
- Modify: `evidence/INDEX.md`

**Interfaces:**
- Produces: `EV-SEO-001` … `EV-SEO-005`.

- [ ] **Step 1: Fetch sources**
  - Titles: Google Search Central, "Influencing your title links in search results" — https://developers.google.com/search/docs/appearance/title-link
  - Meta description / snippets: Google, "Control your snippets in search results" — https://developers.google.com/search/docs/appearance/snippet
  - Headings / structure & overall on-page: Google, "SEO Starter Guide" — https://developers.google.com/search/docs/fundamentals/seo-starter-guide
  - Descriptive link text: same SEO Starter Guide (link-text section); co-source WCAG 2.4.4 Link Purpose — https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html

- [ ] **Step 2: Write `evidence/seo/on-page.md`**
  - `## EV-SEO-001: Write a unique, descriptive title for each page` — Strength `convention` (Google guidance). Claim: give every page a unique `<title>` that accurately describes its content; it becomes the primary search result link. Applies when: every indexable page.
  - `## EV-SEO-002: Write a useful meta description` — Strength `convention`. Claim: provide a concise, accurate meta description summarising the page; Google may use it as the snippet. Applies when: pages you want to control the snippet for. Exception: Google may generate its own snippet regardless.
  - `## EV-SEO-003: Use one clear H1 and a logical heading outline` — Strength `convention` (Google) — where the heading-hierarchy point overlaps WCAG it may be `standard`; label per what you cite. Claim: structure content with a single descriptive `<h1>` and properly nested headings so both users and crawlers understand the page. Applies when: content pages.
  - `## EV-SEO-004: Use semantic HTML landmarks` — Strength `convention`. Claim: use real semantic elements (`header`, `nav`, `main`, `footer`, headings) rather than generic `div`s so content structure is machine-readable. Applies when: any page. (If the SEO Starter Guide does not cover landmarks specifically, source this to the WCAG info-and-relationships criterion https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html and label `standard`.)
  - `## EV-SEO-005: Write descriptive link text` — Strength `standard` (WCAG 2.4.4) with Google co-source. Claim: link text should describe the destination; avoid "click here" / bare URLs. Applies when: all links.

- [ ] **Step 3: Update `evidence/INDEX.md`**

  Add section `## SEO and marketing`:
  ```
  - evidence/seo/on-page.md — page titles, meta descriptions, heading outline, semantic landmarks, descriptive link text — EV-SEO-001, EV-SEO-002, EV-SEO-003, EV-SEO-004, EV-SEO-005
  ```

- [ ] **Step 4: Format lint + URL check** (expect 5)

- [ ] **Step 5: Commit**
  ```bash
  git add evidence/seo/on-page.md evidence/INDEX.md
  git commit -m "feat: seo evidence - on-page (EV-SEO-001..005)"
  ```

---

## Task 8: SEO evidence — technical

**Files:**
- Create: `evidence/seo/technical.md`
- Modify: `evidence/INDEX.md`

**Interfaces:**
- Produces: `EV-SEO-006` … `EV-SEO-010`.

- [ ] **Step 1: Fetch sources**
  - Mobile-first: Google, "Mobile-first indexing best practices" — https://developers.google.com/search/docs/crawling-indexing/mobile/mobile-sites-mobile-first-indexing
  - Core Web Vitals: web.dev, "Web Vitals" — https://web.dev/articles/vitals ; and Google, "Understanding page experience" — https://developers.google.com/search/docs/appearance/page-experience
  - Image alt + optimisation: Google, "Google Images best practices" — https://developers.google.com/search/docs/appearance/google-images ; co-source WCAG 1.1.1 Non-text Content — https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html
  - Structured data: Google, "Intro to structured data markup" — https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data
  - Canonicalisation: Google, "Consolidate duplicate URLs" — https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls

- [ ] **Step 2: Write `evidence/seo/technical.md`**
  - `## EV-SEO-006: Make pages mobile-friendly` — Strength `convention` (Google). Claim: serve responsive, mobile-usable pages; Google predominantly uses the mobile version for indexing and ranking. Applies when: every indexable page.
  - `## EV-SEO-007: Meet Core Web Vitals thresholds` — Strength `convention` (Google/web.dev guidance, with measured field-data backing — cite the specific LCP/CLS/INP thresholds from the source). Claim: optimise loading (LCP), interactivity (INP), and visual stability (CLS) to the "good" thresholds; page experience is a ranking consideration. Applies when: production pages. 
  - `## EV-SEO-008: Provide descriptive alt text and optimised images` — Strength `standard` (WCAG 1.1.1 for alt) + Google co-source for optimisation. Claim: give informative images descriptive `alt` and serve appropriately sized/compressed image files. Applies when: pages with images. Exception: purely decorative images take empty `alt=""`.
  - `## EV-SEO-009: Add structured data where the content type supports it` — Strength `convention`. Claim: mark up eligible content (products, articles, FAQs, breadcrumbs) with valid schema.org structured data to enable rich results. Applies when: pages whose content maps to a supported type. Exception: do not mark up content not visible on the page.
  - `## EV-SEO-010: Set a canonical URL for duplicate/near-duplicate pages` — Strength `convention`. Claim: designate a canonical URL when the same content is reachable at multiple URLs, to consolidate ranking signals. Applies when: sites with duplicate/parameterised URLs.

- [ ] **Step 3: Update `evidence/INDEX.md`**
  ```
  - evidence/seo/technical.md — mobile-friendliness, Core Web Vitals, image alt/optimisation, structured data, canonicalisation — EV-SEO-006, EV-SEO-007, EV-SEO-008, EV-SEO-009, EV-SEO-010
  ```

- [ ] **Step 4: Format lint + URL check** (expect 5; verify the Core Web Vitals thresholds you quote match the fetched web.dev page)

- [ ] **Step 5: Commit**
  ```bash
  git add evidence/seo/technical.md evidence/INDEX.md
  git commit -m "feat: seo evidence - technical (EV-SEO-006..010)"
  ```

---

## Task 9: Conversion evidence — landing pages

Expected to carry the most `convention` labels. Drop any claim you cannot source to a qualifying article rather than shipping a vendor-marketing citation.

**Files:**
- Create: `evidence/conversion/landing.md`
- Modify: `evidence/INDEX.md`

**Interfaces:**
- Produces: `EV-CONV-001` … `EV-CONV-007` (fewer if any are dropped for lack of a qualifying source; leave the numbering gap).

- [ ] **Step 1: Fetch sources**
  - Value proposition above the fold: NN/g, "The Fold Manifesto: Why the Page Fold Still Matters" — https://www.nngroup.com/articles/page-fold-manifesto/ ; and NN/g, "Value Proposition" content if available.
  - Scannable copy: NN/g, "How Users Read on the Web" — https://www.nngroup.com/articles/how-users-read-on-the-web/ (reuse; cite here too).
  - Message match / information scent: NN/g, "Information Scent" — https://www.nngroup.com/articles/information-scent/ (supports link↔destination continuity; underlies message match).
  - Single primary CTA: NN/g on primary vs secondary actions / call-to-action buttons — search NN/g and fetch the relevant article; if none qualifies, label the claim `convention` and cite the closest NN/g visual-hierarchy source, or drop it.
  - Social proof: NN/g on testimonials/social proof if a qualifying article exists; otherwise cite Cialdini's public summary or drop. Do not cite a vendor CRO blog.
  - Directional cues: source to NN/g visual-hierarchy/gaze research or drop.

- [ ] **Step 2: Write `evidence/conversion/landing.md`** (write only the claims you could source; keep IDs sequential to what you keep)
  - `## EV-CONV-001: Lead with a benefit-focused value proposition above the fold` — Strength `convention`/`research-backed` per source. Claim: state what the page offers and why it matters in the first viewport; users decide quickly whether to stay. Applies when: landing/marketing pages.
  - `## EV-CONV-002: Match the headline to the source message` — Strength `convention`. Claim: the landing headline should continue the promise of the ad/link/search result that brought the user; a break in scent increases bounce. Applies when: campaign/ad landing pages.
  - `## EV-CONV-003: Feature a single primary call to action` — Strength `convention`. Claim: give the page one clear primary action, visually dominant over secondary links; competing CTAs dilute conversion. Applies when: goal-driven landing pages. Exception: pages serving genuinely distinct audiences may need two clearly-ranked paths.
  - `## EV-CONV-004: Make copy scannable` — Strength `research-backed` (NN/g reading research). Claim: use short paragraphs, meaningful subheads, and front-loaded key words; users scan rather than read. Applies when: any marketing copy.
  - `## EV-CONV-005: Provide credible social proof` — Strength `convention`. Claim: include specific, credible evidence (named testimonials, real numbers, recognisable logos) near decision points. Applies when: pages asking for signup/purchase. (Drop if unsourceable.)
  - `## EV-CONV-006: Guide the eye toward the CTA` — Strength `convention`. Claim: use visual hierarchy, whitespace, and directional cues so the layout leads to the primary action (ties to EV-LAYOUT-001). Applies when: landing pages. (Drop if unsourceable.)
  - `## EV-CONV-007: Reduce form friction on conversion pages` — Strength `research-backed`. Claim: ask for the fewest fields necessary; each added field lowers completion. Cite the existing forms evidence sources or Baymard directly. Cross-reference `EV-FORM-012`. Applies when: landing pages with a form.

- [ ] **Step 3: Update `evidence/INDEX.md`** (list only the IDs you kept)
  ```
  - evidence/conversion/landing.md — value proposition, message match, single primary CTA, scannable copy, social proof, directional cues, form friction — EV-CONV-001, EV-CONV-002, EV-CONV-003, EV-CONV-004, EV-CONV-005, EV-CONV-006, EV-CONV-007
  ```

- [ ] **Step 4: Format lint + URL check** (headings == strength == number kept; every URL a qualifying source)

- [ ] **Step 5: Commit**
  ```bash
  git add evidence/conversion/landing.md evidence/INDEX.md
  git commit -m "feat: conversion evidence - landing pages (EV-CONV-...)"
  ```

---

## Task 10: The seo-helper skill (audit + generate) and release wiring

**Files:**
- Create: `skills/seo-helper/SKILL.md`
- Create: `tests/fixtures/bad-seo-landing.html`
- Modify: `tests/CHECKLIST.md`
- Modify: `README.md`
- Modify: `CONTRIBUTING.md`
- Modify: `.claude-plugin/plugin.json`
- Modify: `.claude-plugin/marketplace.json`

**Interfaces:**
- Consumes: `EV-SEO-001..010`, `EV-CONV-001..007`, `EV-LAYOUT-001..012` (Tasks 1–4, 7–9).

- [ ] **Step 1: Write `skills/seo-helper/SKILL.md`**

  Frontmatter:
  ```
  ---
  name: seo-helper
  description: Use when creating or auditing an SEO or marketing landing page - audits an existing page or generates a self-contained landing-page mockup, with every structural and SEO choice backed by a cited claim from this plugin's evidence library, and never invents sources
  ---
  ```

  Body sections, mirroring the discipline of `design-review`:
  - **Hard rules** (copy the intent of design-review's hard rules): never invent a claim ID/source/statistic/study; cite by ID and source name; a recommendation with no backing claim is labeled "opinion — no citation"; only cite IDs read this session.
  - **Two modes.** State that the skill either **audits** an existing page or **generates** a mockup, chosen from the user's request; if unclear, ask which.
  - **Audit workflow:** identify the page (code/screenshot/description); read `${CLAUDE_PLUGIN_ROOT}/evidence/INDEX.md`, then read `evidence/seo/on-page.md`, `evidence/seo/technical.md`, `evidence/conversion/landing.md`, and the relevant `evidence/layout/*`; examine the page against each claim (title, meta, headings, semantics, mobile/performance signals visible in code, value proposition, CTA, hierarchy, copy scannability); write an impact-ordered review with citations, same format as design-review.
  - **Generate workflow:** read the same evidence first; produce **one self-contained HTML file** using the pinned Tailwind CDN and no other external requests; structure the page to satisfy the evidence (single benefit-led H1 and value proposition above the fold per EV-CONV-001; one primary CTA per EV-CONV-003; semantic landmarks and heading outline per EV-SEO-003/004; descriptive `<title>` and meta description per EV-SEO-001/002; readable measure and hierarchy per EV-LAYOUT-007/001). Annotate each major block with an HTML comment citing the claim that motivated it, e.g. `<!-- single primary CTA per EV-CONV-003 -->`. If a choice has no backing claim, the comment says "opinion — no citation". End the file with a comment listing the claims applied. Label the file a throwaway mockup, not production code.
  - **Output format** for audits: a readable review, not a rule dump; findings ordered by user impact; a short "what's already right" list at the end if applicable — same as design-review.
  - Use the pinned Tailwind CDN URL exactly as the plugin's convention specifies. If no prior generated file exists to copy the pinned URL from, state the pinned version explicitly in the SKILL.md (e.g. a specific `cdn.tailwindcss.com` pin or the versioned Play CDN) so generation is reproducible and reviewable.

- [ ] **Step 2: Create `tests/fixtures/bad-seo-landing.html`**

  A script-free landing page with deliberate SEO + conversion faults: missing/duplicate `<title>`, no meta description, no `<h1>` or several `<h1>`s, `div` soup instead of landmarks, images with no `alt`, no clear value proposition, three equally-weighted CTAs, and wall-of-text copy. Top comment marks it as a bad fixture, not production code. No scripts.

- [ ] **Step 3: Add checklist entries to `tests/CHECKLIST.md`**

  Under `## seo-helper`:
  ```
  9. Ask seo-helper to AUDIT tests/fixtures/bad-seo-landing.html. The review must:
     - flag missing <title>/meta description (cite EV-SEO-001/EV-SEO-002),
     - flag missing/duplicate <h1> or non-semantic structure (cite EV-SEO-003/EV-SEO-004),
     - flag missing image alt (cite EV-SEO-008),
     - flag the absent value proposition or competing CTAs (cite EV-CONV-001/EV-CONV-003),
     - cite no claim ID that does not exist in evidence/.
  10. Ask seo-helper to GENERATE a landing page for a sample product. The output must:
     - be a single self-contained HTML file,
     - make no external request except the pinned Tailwind CDN,
     - contain HTML citation comments that reference only real claim IDs (spot-check each with grep),
     - be labeled a throwaway mockup.
  ```

- [ ] **Step 4: Update `README.md`**

  In "What you get", add a bullet for `seo-helper` (audits or generates SEO/marketing landing pages, cites evidence, generation is a throwaway self-contained HTML mockup). In the evidence description, mention the new domains (layout & visual hierarchy, usability heuristics, SEO, landing-page conversion). Remove or update the "More skills (quick demos, website blocks) are planned" line only if it now reads wrong; keep it truthful.

- [ ] **Step 5a: Update `CONTRIBUTING.md`**

  CONTRIBUTING.md currently describes claim IDs generically as `EV-<DOMAIN>-<NNN>` with `EV-FORM` examples and does not enumerate prefixes, so no list needs editing. Confirm the "Qualifying sources" list (rule 5) already covers the new sources used here — it lists W3C/WCAG, NN/g, Baymard, GOV.UK, platform HIGs, published papers. Add **Google Search Central official docs, web.dev, and Butterick's Practical Typography (free web book)** to that qualifying-sources sentence, since the new domains rely on them. Make only that addition.

- [ ] **Step 5: Bump manifests to 0.2.0**

  `.claude-plugin/plugin.json`: set `"version": "0.2.0"` and update `description` to mention layout/UX review and SEO landing pages. `.claude-plugin/marketplace.json`: update the plugin `description` to match. Keep author/owner `xandarlh02`.

- [ ] **Step 6: Behavioral + format verification**

  Confirm every claim ID referenced in the new SKILL.md exists:
  ```bash
  grep -oE 'EV-(SEO|CONV|LAYOUT|HEUR|FORM|A11Y)-[0-9]+' skills/seo-helper/SKILL.md | sort -u | while read id; do grep -rq "## $id:" evidence/ && echo "$id ok" || echo "$id MISSING"; done
  ```
  Expected: all `ok`. Confirm the two fixtures contain no `<script>`:
  ```bash
  grep -l '<script' tests/fixtures/bad-seo-landing.html tests/fixtures/bad-landing.html || echo "no scripts - good"
  ```
  Expected: `no scripts - good`. Validate both JSON manifests parse:
  ```bash
  python -c "import json,sys; [json.load(open(f)) for f in ['.claude-plugin/plugin.json','.claude-plugin/marketplace.json']]; print('json ok')"
  ```
  If a live plugin session is available, run checklist items 9 and 10.

- [ ] **Step 7: Commit**
  ```bash
  git add skills/seo-helper/SKILL.md tests/fixtures/bad-seo-landing.html tests/CHECKLIST.md README.md CONTRIBUTING.md .claude-plugin/plugin.json .claude-plugin/marketplace.json
  git commit -m "feat: seo-helper skill (audit + generate), fixtures, v0.2.0"
  ```

---

## Self-review notes (for the executor)

- **Source risk is real.** Several candidate URLs are best-guesses at canonical NN/g / Google pages. The rule is absolute: if the fetched page does not exist or does not support the claim, replace the source or drop the claim — never keep the citation to hit a target count. It is correct and expected for this plan to ship fewer than 39 claims.
- **Strength honesty.** Where a target strength above says `standard`/`research-backed` but the source you actually fetch only supports `convention`, use `convention`. The label follows the source, not the plan.
- **INDEX in the same commit.** Every evidence task updates `evidence/INDEX.md` in its own commit (CONTRIBUTING rule 6). Do not batch index updates into Task 6/10.
- **Milestone.** After Task 6 the layout-review capability is complete and publishable independent of the SEO work; consider a checkpoint there.
