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
