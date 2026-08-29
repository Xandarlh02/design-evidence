# Accessibility evidence: touch targets

This file covers the requirements and platform guidance for pointer and touch target sizing. The claims address the WCAG 2.2 AA minimum size, the larger targets recommended by Apple and Google, and the spacing mechanism that allows undersized targets to pass the criterion when surrounded by sufficient clearance.

## EV-A11Y-009: Interactive targets must be at least 24x24 CSS px (WCAG AA minimum)
**Strength:** standard
**Claim:** Every target for pointer input must be at least 24 by 24 CSS pixels in both dimensions, or be surrounded by sufficient spacing so that a 24-pixel-diameter circle centred on the target does not overlap any other target.
**Evidence:** WCAG 2.2 SC 2.5.8 Target Size (Minimum) is a Level AA requirement. It states that the size of the target for pointer inputs must be at least 24 by 24 CSS pixels; where a target falls short of that size it may still pass if a 24 CSS pixel diameter circle centred on the target's bounding box does not intersect any other target or circle. Exceptions include inline targets within a run of text, user-agent-controlled elements, and targets where an equivalent control on the same page meets the criterion.
**Sources:**
- W3C, "Understanding SC 2.5.8: Target Size (Minimum)", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
**Applies when:** all pointer-operable UI components on web interfaces claiming WCAG 2.2 AA conformance.
**Exception:** Inline targets within sentences or blocks of text where the target size is constrained by line-height; elements whose size and position are entirely controlled by the user agent; targets that have an equivalent control elsewhere on the page that meets the criterion; and targets where size is essential to conveying the information (such as map pins at geographic locations).

## EV-A11Y-010: Platform guidelines recommend larger targets: 44x44pt (Apple), 48x48dp (Material)
**Strength:** standard
**Claim:** Apple Human Interface Guidelines recommend a minimum tappable area of 44 by 44 points for all controls; Material Design guidelines recommend a minimum touch target of 48 by 48 density-independent pixels.
**Evidence:** Apple's UI Design Tips page states: "Create controls that measure at least 44 points x 44 points so they can be accurately tapped with a finger." Google's Android accessibility help page states that interactive elements should have "a width and height of at least 48dp, as described in the Material Design Accessibility guidelines," and recommends making "touch targets at least 48x48dp, separated by 8dp of space or more." The Material 48dp target produces a physical size of approximately 9mm regardless of screen density. The W3C Understanding document for SC 2.5.5 links to both Apple and Material Design guidance in its Related Resources section but does not quote their specific measurements.
**Sources:**
- Apple, "Human Interface Guidelines: Accessibility" — https://developer.apple.com/design/human-interface-guidelines/accessibility
- Apple, "UI Design Tips" — https://developer.apple.com/design/tips/
- Material Design, "Accessibility: Layout and typography" — https://m2.material.io/design/usability/accessibility.html
- Google, "Make apps more accessible — Android Accessibility Help" — https://support.google.com/accessibility/android/answer/7101858
**Applies when:** iOS and iPadOS interfaces (Apple 44pt guideline) and Android interfaces (Material 48dp guideline).

## EV-A11Y-011: Provide spacing between adjacent small targets so mis-taps hit nothing rather than the wrong thing
**Strength:** standard
**Claim:** When interactive targets cannot reach 24 by 24 CSS pixels in size, place them far enough apart that a 24-pixel-diameter circle centred on each target does not overlap any neighbouring target or its own spacing circle.
**Evidence:** The spacing mechanism in SC 2.5.8 permits undersized targets to pass if they are sufficiently separated: for each undersized target, an imaginary 24 CSS pixel diameter circle is drawn centred on the target's bounding box, and the criterion passes only if that circle does not intersect another target or the spacing circle of any other adjacent undersized target. This means adequate clearance channels mis-taps into inactive space rather than triggering an adjacent control.
**Sources:**
- W3C, "Understanding SC 2.5.8: Target Size (Minimum)", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
**Applies when:** any row or cluster of closely spaced interactive controls — icon-only toolbars, pagination controls, inline action links — where individual target dimensions fall below 24 by 24 CSS pixels.
**Exception:** If the target meets the 24 by 24 CSS pixel size requirement directly, no spacing analysis is needed; the spacing mechanism is only required for genuinely undersized targets.
