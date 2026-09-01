# Layout evidence: scanning patterns and text alignment

This file covers how users scan text-heavy pages and how text alignment affects readability. EV-LAYOUT-010 and EV-LAYOUT-011 are backed by Nielsen Norman Group eyetracking and usability research and are labelled `research-backed`. EV-LAYOUT-012 is backed by WCAG 2.1 SC 1.4.8, a Level AAA success criterion, which provides normative alignment requirements, and by Butterick's Practical Typography; it is labelled `standard`.

## EV-LAYOUT-010: Design for F-pattern scanning
**Strength:** research-backed
**Claim:** Users scan text-heavy pages in an F-shaped or layer-cake pattern. They read the first lines most thoroughly, then scan down the left edge and read only the first few words of each subsequent line. Place the most important content at the top and left of the page, and lead headings and paragraphs with their most meaningful words.
**Evidence:** Nielsen Norman Group eyetracking research, aggregated from multiple participant sessions, found that "First lines of text on a page receive more gazes than subsequent lines of text on the same page." and "First few words on the left of each line of text receive more fixations than subsequent words on the same line." The same research documents a layer-cake variant: "Layer-cake pattern occurs when the eyes scan headings and subheadings and skip the normal text below." The article notes that "The F-pattern is the default pattern when there are no strong cues to attract the eyes towards meaningful information," meaning that a strong visual hierarchy can redirect gaze away from the default F-path.
**Sources:**
- Kara Pernice, "F-Shaped Pattern of Reading on the Web: Misunderstood, But Still Relevant (Even on Mobile)," Nielsen Norman Group, 2017 — https://www.nngroup.com/articles/f-shaped-pattern-reading-web-content/
**Applies when:** content pages, search results, articles, and any layout with blocks of running text and limited visual hierarchy.
**Exception:** pages with a deliberate and strong visual hierarchy that draws the eye to key elements can break the default F-pattern; this claim applies most directly when layout structure is weak or uniform.

## EV-LAYOUT-011: Front-load the important words
**Strength:** research-backed
**Claim:** Start headings, links, list items, and paragraphs with the information-carrying words. Users rarely read word by word; they scan and pick up the first few words per element. An idea buried past the opening of a paragraph will be skipped.
**Evidence:** Jakob Nielsen's usability study comparing five website versions found that "People rarely read Web pages word by word; instead, they scan the page, picking out individual words and sentences." The same study found that effective copy uses "one idea per paragraph (users will skip over any additional ideas if they are not caught by the first few words in the paragraph)" and "meaningful sub-headings (not 'clever' ones)." These findings reflect measured differences in reading and comprehension across tested site variants, not opinion.
**Sources:**
- Jakob Nielsen, "How Users Read on the Web," Nielsen Norman Group, 1997 — https://www.nngroup.com/articles/how-users-read-on-the-web/
**Applies when:** headings, links, list items, and body copy — any text element where the user may scan rather than read in full.

## EV-LAYOUT-012: Left-align running text; avoid justified text
**Strength:** standard
**Claim:** Left-align body text for left-to-right reading and avoid full justification. Justified text adds uneven white space between words, which creates visual interruptions and impedes reading, particularly for users with cognitive disabilities.
**Evidence:** WCAG 2.1 SC 1.4.8 (Level AAA) requires: "Text is not justified (aligned to both the left and the right margins)." The understanding document states: "People with certain cognitive disabilities have problems reading text that is both left and right justified." SC 1.4.8 is a Level AAA criterion representing best practice for readability, not a minimum conformance requirement. Butterick's Practical Typography, "Justified text," explains the mechanism: "Justification works by adding white space between the words in each line so all the lines are the same length," and recommends that for web pages, "I'll always left-align the text, because justification can look clunky and coarse."
**Sources:**
- W3C, "Understanding SC 1.4.8: Visual Presentation (Level AAA)" — https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation.html
- Matthew Butterick, "Justified text," Practical Typography — https://practicaltypography.com/justified-text.html
**Applies when:** running body text — paragraphs, article copy, onboarding text, help text.
**Exception:** short centred display text such as a single headline or pull quote is acceptable; this claim applies to multi-line running copy.
