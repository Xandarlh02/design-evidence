# Layout evidence: typography and readability

This file covers how line length, line spacing, and a disciplined type scale affect reading comfort and visual hierarchy. EV-LAYOUT-007 and EV-LAYOUT-008 are backed by WCAG 2.1 SC 1.4.8, a Level AAA success criterion, which provides normative numeric thresholds. EV-LAYOUT-009 draws on the practical guidance in Butterick's Practical Typography and is labelled `convention` because no controlled study evidence is cited in that source.

## EV-LAYOUT-007: Keep body line length in a readable range
**Strength:** standard
**Claim:** Limit paragraphs of running text to roughly 45–80 characters per line, including spaces. Lines shorter than about 45 characters force the eye to return too frequently; lines longer than 80 characters make it hard to track from the end of one line to the start of the next.
**Evidence:** WCAG 2.1 SC 1.4.8 (Level AAA) sets a normative ceiling: "Width is no more than 80 characters or glyphs (40 if CJK)." Butterick's Practical Typography, "Line length," gives a practical working range: "Aim for an average line length of 45–90 characters, including spaces" and states "You should be able to fit between two and three alphabets on a line." WCAG 1.4.8 is a Level AAA criterion, meaning it is not a minimum conformance requirement but represents best practice for readability; the 80-character ceiling is the normative upper bound adopted by this claim. Butterick's practical range of 45–90 extends slightly beyond that ceiling — his upper bound of 90 exceeds WCAG's 80. This claim adopts 80 as its upper bound because it is the normative accessibility threshold; lines between 80 and 90 characters may be typographically acceptable by Butterick's measure but do not satisfy SC 1.4.8.
**Sources:**
- W3C, "Understanding SC 1.4.8: Visual Presentation (Level AAA)" — https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation.html
- Matthew Butterick, "Line length," Practical Typography — https://practicaltypography.com/line-length.html
**Applies when:** paragraphs of running body text in articles, forms, onboarding copy, or any multi-sentence content.
**Exception:** single-line inputs, short captions, table cells, and navigation labels are not subject to this constraint.

## EV-LAYOUT-008: Use adequate line spacing for body text
**Strength:** standard
**Claim:** Set line height for running body text to at least 1.5 times the font size. Tighter leading causes lines to bleed together, forcing readers to re-read lines and slowing comprehension.
**Evidence:** WCAG 2.1 SC 1.4.8 (Level AAA) states: "Line spacing (leading) is at least space-and-a-half within paragraphs." The understanding document clarifies this means "top of one line is 150% further from the top of the line below it" — equivalent to a line-height of 1.5 in CSS terms. SC 1.4.8 also requires that paragraph spacing is at least 1.5 times larger than the line spacing; this claim focuses on line-height (leading) specifically, and paragraph spacing is a separate concern addressed at the layout level. Butterick's Practical Typography, "Summary of key rules," rule 3, states line spacing should be "120–145% of the point size," providing a tighter lower bound for print. For UI body text, the WCAG threshold of 1.5 (150%) is the more conservative and accessibility-backed value; it is the appropriate floor for running copy intended for general audiences.
**Sources:**
- W3C, "Understanding SC 1.4.8: Visual Presentation (Level AAA)" — https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation.html
- Matthew Butterick, "Summary of key rules," Practical Typography — https://practicaltypography.com/summary-of-key-rules.html
**Applies when:** body copy, onboarding text, help text, article content — any passage longer than one or two sentences.

## EV-LAYOUT-009: Limit the type scale
**Strength:** convention
**Claim:** Use a small, deliberate set of font sizes and weights to build hierarchy. Introducing additional sizes or weights beyond what the hierarchy demands makes the design read as noise rather than structure, and removes the contrast needed to signal importance.
**Evidence:** Butterick's Practical Typography, "Bold or italic," states: "But if everything is emphasized, then nothing is emphasized." The same source, "Summary of key rules," rule 8, states: "Use bold or italic as little as possible, and not together." These rules reflect a principle of restraint: typographic variation only communicates hierarchy when it is genuinely sparse. Applying it to sizes as well as weights follows the same logic — a design with many competing size levels has no clear dominant level, which collapses the hierarchy rather than reinforcing it. The Butterick summary also specifies point sizes of 10–12pt (print) and 15–25px (web) for body text, implying body text is held to a single band, not varied arbitrarily. This is consensus practitioner guidance, not a finding from a controlled study.
**Sources:**
- Matthew Butterick, "Bold or italic," Practical Typography — https://practicaltypography.com/bold-or-italic.html
- Matthew Butterick, "Summary of key rules," Practical Typography — https://practicaltypography.com/summary-of-key-rules.html
**Applies when:** any UI with a text hierarchy — headings, subheadings, body, captions, labels.
