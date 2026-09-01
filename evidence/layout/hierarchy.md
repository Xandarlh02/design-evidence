# Layout evidence: visual hierarchy

This file covers how to structure visual weight across a screen so users can scan and act efficiently. The claims address hierarchy through size, colour, and contrast; the role of a single dominant focal point; and the principle that visual prominence should reflect task priority. All claims are drawn from NN/g published guidelines; none have been measured in controlled studies, so the honest strength label is `convention`.

## EV-LAYOUT-001: Establish a clear visual hierarchy
**Strength:** convention
**Claim:** Use size, weight, colour, and contrast so the most important element is perceived first and the eye moves through the screen in priority order. Limit size variation to roughly three levels (large, medium, small) to preserve a legible hierarchy without visual noise.
**Evidence:** NN/g's "Visual Hierarchy in UX: Definition" states that visual hierarchy "refers to the organization of design elements so that the eye is guided to consume each in order of intended importance" and that the page's visual hierarchy "controls the delivery of information from the system to the end user." The article identifies scale as "key in creating visual hierarchy" — larger elements "stand out more and attract users' attention" — and notes that contrast in value and saturation, not raw colour, determines what draws the eye. It recommends limiting designs to three size variations to maintain a readable hierarchy.
**Sources:**
- Nielsen Norman Group, "Visual Hierarchy in UX: Definition" — https://www.nngroup.com/articles/visual-hierarchy-ux-definition/
**Applies when:** any screen with more than a few elements.

## EV-LAYOUT-002: Give each view one dominant focal point
**Strength:** convention
**Claim:** Make a single element clearly dominant per view. When multiple elements compete at equal visual weight, the hierarchy collapses and users struggle to know where to focus first.
**Evidence:** NN/g's "Visual Hierarchy in UX: Definition" describes the failure mode directly: when elements are "all relatively equal in size and color and lack breathing room," users struggle to focus. The article states that "if everything is contrasted, then nothing stands out," explaining why undifferentiated, competing elements undermine effective scanning. Giving one element a clear size, contrast, or spacing advantage over all others establishes the dominant focal point that guides entry into the page.
**Sources:**
- Nielsen Norman Group, "Visual Hierarchy in UX: Definition" — https://www.nngroup.com/articles/visual-hierarchy-ux-definition/
**Applies when:** landing pages, hero sections, primary task screens.

## EV-LAYOUT-003: Match visual prominence to task priority
**Strength:** convention
**Claim:** The most visually prominent element on a screen should be the highest-priority action or piece of information, not a decorative element. Misaligned prominence — where a low-priority item draws the most attention — causes users to overlook the primary task path.
**Evidence:** NN/g's "Visual Hierarchy in UX: Definition" establishes that visual hierarchy "controls the delivery of information from the system to the end user" and that bright, saturated colours should emphasise important items while less-saturated colours serve secondary content. The same article warns that if visual contrast is applied indiscriminately, "nothing stands out," meaning prominence choices must track importance. Applying strong visual weight to decorative elements therefore competes directly with the hierarchy needed to guide users to primary actions.
**Sources:**
- Nielsen Norman Group, "Visual Hierarchy in UX: Definition" — https://www.nngroup.com/articles/visual-hierarchy-ux-definition/
**Applies when:** any task-oriented UI.
