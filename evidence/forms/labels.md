# Forms evidence: label placement and visibility

This file covers how to position and display field labels in forms. The claims address label alignment, the role of placeholder text, label persistence, and how to mark required and optional fields. Each claim is drawn from published eye-tracking research, NN/g usability guidelines, or Baymard Institute benchmark data.

## EV-FORM-001: Top-aligned labels outperform left-aligned labels
**Strength:** research-backed
**Claim:** Place field labels directly above their input fields. Top-aligned labels let users take in the label and the field in a single eye movement, reducing completion time compared to labels positioned to the left of fields.
**Evidence:** Matteo Penzo's 2006 eye-tracking study measured saccade times between labels and fields across four placement conditions. Labels placed above inputs produced saccade durations of roughly 50 ms, while labels to the left of fields produced durations around 500 ms — an order-of-magnitude difference. The study also found that right-aligned left-of-field labels halved the number of fixations compared to left-aligned placements.
**Sources:**
- Matteo Penzo, "Label Placement in Forms", UXmatters, 2006 — https://www.uxmatters.com/mt/archives/2006/07/label-placement-in-forms.php
**Applies when:** single-column forms or any form where completion speed matters.
**Exception:** Extremely long desktop forms with many fields may tolerate left-aligned labels to expose more labels at once; the Penzo data does not cover that layout.

## EV-FORM-002: Do not use placeholder text as the only label
**Strength:** research-backed
**Claim:** Always provide a persistent visible label outside the input field. Never rely on placeholder text alone to identify what a field expects.
**Evidence:** NN/g's article on placeholder usability identifies seven failure modes: placeholder text disappears on focus, straining short-term memory; users cannot review their answers before submission; keyboard-navigation users never see the placeholder text vanish; eyetracking shows users scan past pre-filled-looking fields; and some placeholders require manual deletion before typing. The article also flags poor contrast and inconsistent screen reader support as accessibility problems.
**Sources:**
- Nielsen Norman Group, "Placeholders in Form Fields Are Harmful", 2014 — https://www.nngroup.com/articles/form-design-placeholders/
**Applies when:** all form fields regardless of length or context.

## EV-FORM-003: Keep labels visible at all times
**Strength:** research-backed
**Claim:** Labels must remain visible while the user is filling in a field. Do not use patterns — such as floating or disappearing labels — that hide the label text once the user starts typing.
**Evidence:** NN/g's placeholder research directly documents that disappearing label text strains short-term memory, prevents answer verification before submission, and makes error recovery difficult because users no longer see the field description when an error message appears. Their separate form-design article cites Seckler et al.'s finding that forms following usability guidelines — including persistent, clearly positioned labels — achieved 78% one-try submissions versus 42% for non-compliant forms.
**Sources:**
- Nielsen Norman Group, "Placeholders in Form Fields Are Harmful", 2014 — https://www.nngroup.com/articles/form-design-placeholders/
- Nielsen Norman Group, "Web Form Design", 2016 — https://www.nngroup.com/articles/web-form-design/
**Applies when:** all form fields.
**Exception:** Floating-label patterns that keep the label visible in a smaller position above the input (rather than hiding it entirely) may be acceptable if contrast and legibility are maintained.

## EV-FORM-004: Mark both required and optional fields explicitly
**Strength:** research-backed
**Claim:** Mark both required and optional fields with explicit text rather than marking only one group. Relying on users to infer which fields are required from the absence of a marker causes confusion and validation errors.
**Evidence:** Baymard Institute's large-scale e-commerce benchmark found that 37% of sites marked only optional fields. In testing, 32% of users encountered a validation error because they did not complete a required field, and at one major retailer 44% of users stalled at a form section where only optional fields were labelled. Baymard concludes that both required and optional fields should be explicitly marked to let users progress without having to infer requirements from context.
**Sources:**
- Baymard Institute, "Marking Required vs. Optional Fields", 2019 — https://baymard.com/blog/required-optional-form-fields
**Applies when:** forms with a mix of required and optional fields.
