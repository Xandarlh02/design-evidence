# Forms evidence: inline validation and error messages

This file covers when and how to present validation feedback in forms. The claims address validation timing, error message content, accessibility of error indicators, input preservation, and error summaries on long forms. Sources include NN/g usability guidelines, WCAG 2.2, and the GOV.UK Design System.

## EV-FORM-005: Validate after the user leaves a field, not on every keystroke
**Strength:** convention
**Claim:** Trigger error messages when the user moves focus away from a field (on blur), not while they are still typing. For complex inputs such as passwords, real-time feedback showing what has been satisfied is acceptable.
**Evidence:** NN/g's form error guidelines recommend avoiding error display until the user has finished with a field and moved to the next one. The same article notes that for complex fields — such as new passwords — keystroke-level success indicators help users understand requirements without repeated guessing. No measured research data is cited; the guidance rests on reasoning about user friction and recovery.
**Sources:**
- Nielsen Norman Group, "How to Report Errors in Forms: 10 Design Guidelines", 2022 — https://www.nngroup.com/articles/errors-forms-design-guidelines/
**Applies when:** form fields with format or content requirements.
**Exception:** Real-time feedback on password-strength or character-count indicators is acceptable and encouraged when it shows what conditions have been met rather than flagging failures mid-entry.

## EV-FORM-006: Error messages must say what went wrong and how to fix it
**Strength:** convention
**Claim:** Write error messages in plain language that identifies the problem and gives a concrete corrective action. Avoid jargon, error codes, and blame-focused phrasing.
**Evidence:** NN/g's error message guidelines require that messages describe the issue concisely and offer constructive advice for recovery. The article grounds these requirements in Nielsen's heuristic 9 — "Help Users Recognize, Diagnose, and Recover from Errors" — but does not cite empirical studies measuring outcomes. The guidance is consistent expert-derived practice rather than controlled-study findings.
**Sources:**
- Nielsen Norman Group, "Error Message Guidelines", 2001 — https://www.nngroup.com/articles/error-message-guidelines/
**Applies when:** any form field or system action that can produce an error state.

## EV-FORM-007: Do not signal errors with color alone
**Strength:** standard
**Claim:** Error states must be communicated through a visual means in addition to color — such as an icon, border-style change, or text label — so that users who cannot distinguish colors can still identify which fields have errors.
**Evidence:** WCAG 2.2 Success Criterion 1.4.1 (Use of Color, Level A) prohibits using color as the only visual means of conveying information, indicating an action, or distinguishing an element. The Understanding document explicitly identifies "identifying required or error fields using color differences only" as a failure of this criterion.
**Sources:**
- W3C, "Understanding SC 1.4.1: Use of Color (WCAG 2.2)", 2023 — https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html
**Applies when:** all form error states, required-field indicators, and any status information conveyed visually.

## EV-FORM-008: Preserve the user's input when showing an error
**Strength:** convention
**Claim:** When a form submission fails validation, do not clear the fields. Display the error messages alongside the values the user entered so they can see what was wrong and correct it without re-entering data.
**Evidence:** The GOV.UK Design System's error message guidance explicitly states that form fields must not be cleared when errors are shown, and that both passing and failing answers should be kept. The rationale given is that retained input lets users see what went wrong, edit their previous answer, and avoid re-entering information. The guidance is described as tested with users in live services, but no specific study data is published on this particular practice.
**Sources:**
- GOV.UK Design System, "Error message", 2024 — https://design-system.service.gov.uk/components/error-message/
**Applies when:** any form that performs server-side or deferred validation before navigating away.

## EV-FORM-009: Show an error summary at the top of the form when validation fails
**Strength:** convention
**Claim:** When a form submission produces any validation error, display a summary at the top of the page listing every error with a link to the affected field. Always show this summary when there are errors, including when there is only one.
**Evidence:** The GOV.UK Design System's error summary component prescribes this pattern as established design-system practice — an always-visible summary headed "There is a problem", with each item linking to its field. The design system states the component should always be used with its error message component. No research data is cited on the page; the community discussion on GitHub remains open for further validation.
**Sources:**
- GOV.UK Design System, "Error summary", 2024 — https://design-system.service.gov.uk/components/error-summary/
**Applies when:** any form that performs validation — the error summary must be shown whenever there is at least one validation error, regardless of form length.
