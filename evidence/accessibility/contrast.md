# Accessibility evidence: colour contrast

This file covers WCAG 2.2 contrast requirements for text, user interface components, and graphical objects, plus the prohibition on colour as a sole means of conveying information. Each claim cites the relevant W3C Understanding document; all are normative Level A or AA requirements under WCAG 2.2.

## EV-A11Y-001: Body text needs a contrast ratio of at least 4.5:1
**Strength:** standard
**Claim:** Text smaller than 18 point (non-bold) or 14 point bold must have a contrast ratio of at least 4.5:1 against its background.
**Evidence:** WCAG 2.2 SC 1.4.3 (Level AA) sets 4.5:1 as the minimum contrast ratio for normal-sized text. The criterion defines normal text as anything below the large-text threshold: 18 pt (approximately 24 px) for regular weight and 14 pt (approximately 18.5 px) for bold. Computed ratios must not be rounded, so 4.499:1 does not meet the threshold.
**Sources:**
- W3C, "Understanding SC 1.4.3: Contrast (Minimum)", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html
**Applies when:** any text content rendered by the author against a background colour, on web or native interfaces targeting WCAG 2.2 AA conformance.
**Exception:** Inactive UI components, purely decorative text, logotypes, and text embedded in images containing significant other visual content are exempt.

## EV-A11Y-002: Large text needs a contrast ratio of at least 3:1
**Strength:** standard
**Claim:** Large-scale text — at least 18 point (approximately 24 px) for regular weight, or at least 14 point (approximately 18.5 px) for bold — requires a minimum contrast ratio of 3:1 against its background.
**Evidence:** WCAG 2.2 SC 1.4.3 (Level AA) permits a relaxed 3:1 ratio for large-scale text because larger letterforms remain legible at lower contrast. The Understanding document states that 18 pt and 14 pt are equivalent to approximately 24 px and 18.5 px respectively, based on a 1 pt = 1.333 px conversion. The no-rounding rule applies: 2.999:1 would not meet the threshold.
**Sources:**
- W3C, "Understanding SC 1.4.3: Contrast (Minimum)", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html
**Applies when:** text styled at or above the large-text size thresholds defined in SC 1.4.3.
**Exception:** Same exemptions as EV-A11Y-001 apply.

## EV-A11Y-003: UI component boundaries and graphical objects need at least 3:1
**Strength:** standard
**Claim:** Visual information that identifies a user interface component or its state, and parts of graphics required to understand the content, must have a contrast ratio of at least 3:1 against adjacent colours.
**Evidence:** WCAG 2.2 SC 1.4.11 Non-text Contrast (Level AA) extends contrast requirements beyond text to two categories: the visual boundary or indicator needed to identify interactive components and their states, and the portions of graphics whose meaning depends on their colour. The 3:1 ratio is measured against the immediately adjacent colour. Inactive or disabled components are exempt; computed ratios must not be rounded.
**Sources:**
- W3C, "Understanding SC 1.4.11: Non-text Contrast", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html
**Applies when:** borders, focus rings, icons, charts, and any other non-text visual element whose meaning the user must be able to perceive.
**Exception:** Inactive UI components and graphics where a specific presentation is essential to the information conveyed are exempt.

## EV-A11Y-004: Never convey information by colour alone
**Strength:** standard
**Claim:** Colour must not be the sole visual means of communicating information, indicating an action, prompting a response, or distinguishing a visual element.
**Evidence:** WCAG 2.2 SC 1.4.1 Use of Color (Level A) requires that any meaning carried by colour also be expressed through a second visual channel — such as a text label, icon, pattern, or underline. Errors, required-field markers, chart categories, and link text that rely on colour differences alone all fail this criterion. The criterion applies to all authored content regardless of the medium.
**Sources:**
- W3C, "Understanding SC 1.4.1: Use of Color", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html
**Applies when:** any context where colour is used to signal meaning, including form validation states, data visualisations, and inline links.
