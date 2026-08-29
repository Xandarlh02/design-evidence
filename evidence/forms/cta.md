# Forms evidence: calls to action and button design

This file covers how to label, style, and size calls to action and interactive controls. The claims address button label specificity, visual hierarchy between primary and secondary actions, and minimum touch target size. Sources include NN/g usability guidance, the GOV.UK Design System, and WCAG 2.2.

## EV-FORM-014: Button labels should describe the action, not say "Submit" or "Learn more"
**Strength:** convention
**Claim:** Write button and link labels that describe the specific outcome of the action. Generic labels such as "Submit", "Click here", and "Learn more" give users no information about what will happen, creating uncertainty and accessibility barriers for screen reader users.
**Evidence:** NN/g's article on "Learn More" links argues from UX principles and real-world examples that generic labels reduce information scent — users cannot predict what they will get by clicking — and create specific problems for screen reader users who navigate by link text alone and hear a list of identically-named links with no distinguishing context. The article provides practical rewrites but does not present quantitative data from controlled studies.
**Sources:**
- Nielsen Norman Group, Katie Sherwin, "'Learn More' Links: You Can Do Better", 2015 — https://www.nngroup.com/articles/learn-more-links/
**Applies when:** all buttons, links, and calls to action.

## EV-FORM-015: One visually dominant primary action per screen; secondary actions styled subordinate
**Strength:** convention
**Claim:** Include at most one visually dominant primary button per page or screen. Secondary actions should be styled to appear clearly less prominent than the primary action so that users understand the intended next step.
**Evidence:** The GOV.UK Design System states that sites should use a single default button for the main call to action on a page, and explicitly warns against using multiple default buttons because doing so reduces their impact and makes it harder for users to know what to do next. Secondary buttons use a distinct, visually subdued style to differentiate them. The system notes that pages with too many calls to action make it hard for users to identify the right next step.
**Sources:**
- GOV.UK Design System, "Button component", 2024 — https://design-system.service.gov.uk/components/button/
**Applies when:** any screen or form with more than one available action.
**Exception:** Wizard or step-by-step flows that genuinely offer equally weighted paths (such as "Save and continue" alongside "Save as draft") may require two similarly prominent actions; in that case, differentiate through label specificity rather than visual dominance alone.

## EV-FORM-016: Interactive controls must meet minimum target size (see EV-A11Y-009/010 for the normative values)
**Strength:** standard
**Claim:** Interactive controls must present a pointer target of at least 24 by 24 CSS pixels. The normative pixel values for this requirement and its spacing exception are specified in EV-A11Y-009 and EV-A11Y-010.
**Evidence:** WCAG 2.2 Success Criterion 2.5.8, Target Size (Minimum), at Level AA, requires that the size of the target for pointer inputs is at least 24 by 24 CSS pixels. A spacing exception allows smaller rendered targets provided a 24 CSS pixel diameter circle centred on the target does not intersect other targets. The requirement is independent of the page zoom factor. Five further exceptions exist for inline text links, user-agent-controlled controls, and targets where size is essential to the presentation. The Understanding document on this page is informative, but it explains a normative WCAG 2.2 Level AA criterion.
**Sources:**
- W3C Web Accessibility Initiative, "Understanding SC 2.5.8: Target Size (Minimum) (Level AA)", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
**Applies when:** all interactive controls on pointer-input interfaces (web, hybrid, and touch-capable desktop).
**Exception:** Inline links within a block of text, controls whose size is determined by the user agent and not modified by the author, and controls where a specific presentation is essential to the information being conveyed are exempt from the minimum size requirement.
