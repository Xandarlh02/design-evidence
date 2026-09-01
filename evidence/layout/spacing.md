# Layout evidence: spacing and grouping

This file covers how proximity, whitespace, and a consistent spacing scale structure a layout so users can scan and act efficiently. The claims address grouping related elements through proximity, using whitespace rather than heavy dividers to separate content, and maintaining a single spacing scale across components. All claims are drawn from NN/g published guidelines and the GOV.UK Design System; none have been measured in controlled studies, so the honest strength label is `convention`.

## EV-LAYOUT-004: Group related elements with proximity
**Strength:** convention
**Claim:** Place related controls and content close together and separate unrelated groups with more space. Proximity communicates relationship before any label is read — users perceive nearby elements as sharing functionality or meaning, and elements spaced apart as belonging to separate groups.
**Evidence:** NN/g's "Proximity Principle in Visual Design" states that "items close together are likely to be perceived as part of the same group — sharing similar functionality or traits" and that proximity "is one of the most important grouping principles and can overpower competing visual cues such as similarity of color or shape." The article describes Gestalt proximity principles as established knowledge from the first half of the 20th century but does not cite specific academic papers or named researchers; the article is a practitioner guide, not a primary research citation. It illustrates the principle through concrete product examples: a form chunked into three groups of four fields appears less daunting than twelve undifferentiated fields, and a misplaced Add button near unrelated navigation controls was routinely missed by users.
**Sources:**
- Nielsen Norman Group, "Proximity Principle in Visual Design" — https://www.nngroup.com/articles/gestalt-proximity/
**Applies when:** forms, toolbars, card layouts, any grouped content.

## EV-LAYOUT-005: Use whitespace to separate, not borders alone
**Strength:** convention
**Claim:** Prefer adequate spacing over heavy dividers or boxes to structure a layout. Whitespace alone can communicate groupings and boundaries; sufficient spacing reduces clutter and improves comprehension without adding visual noise.
**Evidence:** NN/g's "Proximity Principle in Visual Design" states that "using varying amounts of whitespace to either unite or separate elements is key to communicating meaningful groupings." The article shows that groupings remain "discernible even without viewing the actual text," demonstrating that spatial distance is sufficient to communicate structure independently of borders or rules. It also notes that "whitespace around well-designed headings signals which paragraphs they are associated with" — again without any dividing line. The article does not mention borders or dividers at all, implying they are not required when spacing is used deliberately.
**Sources:**
- Nielsen Norman Group, "Proximity Principle in Visual Design" — https://www.nngroup.com/articles/gestalt-proximity/
**Applies when:** content-dense pages.
**Exception:** data tables and dense enterprise grids where available space is scarce and explicit row rules aid alignment.

## EV-LAYOUT-006: Use a single consistent spacing scale
**Strength:** convention
**Claim:** Derive all margins and padding from one limited spacing scale rather than ad-hoc values. Consistent spacing rhythm is easier to scan and signals care in execution; it also simplifies maintenance because components share a common set of values.
**Evidence:** The GOV.UK Design System's spacing guidance defines two predefined scales — a responsive scale that adapts based on screen size (switching at the 640 px tablet breakpoint) and a static scale that stays the same for all screen sizes. Both scales are enforced through dedicated SASS helpers: `govuk-responsive-margin`, `govuk-responsive-padding`, and `govuk-spacing`. Providing these helpers means all margins and padding are derived from a single shared scale rather than chosen as ad-hoc pixel values — a structural constraint that makes deviations from the scale the explicit choice rather than the default.
**Sources:**
- GOV.UK Design System, "Spacing" — https://design-system.service.gov.uk/styles/spacing/
**Applies when:** any multi-component UI.
