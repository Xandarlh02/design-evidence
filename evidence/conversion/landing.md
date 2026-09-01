# Conversion evidence: landing pages

This file covers design decisions that affect whether visitors on landing and marketing pages stay, engage, and convert. The claims address value proposition placement, message continuity from ad to page, single primary calls to action, scannable copy, social proof, visual guidance toward the primary action, and form friction. EV-CONV-001 and EV-CONV-004 are labelled `research-backed` because the cited NN/g articles present measured usability or eyetracking data. The remaining claims — EV-CONV-002, EV-CONV-003, EV-CONV-005, EV-CONV-006, and EV-CONV-007 — are labelled `convention`, reflecting that the cited sources establish design guidance or benchmark an adjacent context (checkout forms) rather than quantified conversion experiments on landing-page forms specifically.

## EV-CONV-001: Lead with a benefit-focused value proposition above the fold
**Strength:** research-backed
**Claim:** State what the page offers and why it matters within the first viewport. Users assess whether to continue scrolling — or leave — based primarily on what is visible without scrolling, so the primary value proposition must be immediately accessible.
**Evidence:** NN/g's "The Fold Manifesto: Why the Page Fold Still Matters" presents eyetracking and advertising data showing that content above the fold is viewed substantially more than content below it. An eyetracking study cited in the article found that content 100 pixels above the fold received 102% more attention than content 100 pixels below. A Google advertising analysis found 73% viewability for ads above the fold versus 44% below. Aggregated across multiple studies, the article concludes that there is an 84% average difference in how users treat information above versus below the fold. The article states that what appears at the top of the page helps users decide whether to continue scrolling, navigate elsewhere, try another site, or abandon the task altogether, making the first viewport critical for communicating purpose and value.
**Sources:**
- Nielsen Norman Group, "The Fold Manifesto: Why the Page Fold Still Matters" — https://www.nngroup.com/articles/page-fold-manifesto/
**Applies when:** landing pages and marketing pages where the primary goal is retaining visitor attention.

## EV-CONV-002: Match the headline to the source message
**Strength:** convention
**Claim:** The landing page headline should continue the promise of the advertisement, link, or search result that brought the user. A gap between what the link promised and what the page delivers weakens information scent, causes users to doubt they have arrived at the right place, and increases the likelihood they will leave.
**Evidence:** NN/g's "Information Scent: How Users Decide Where to Go Next" defines information scent as the user's estimate of how much value a destination will deliver, based on link labels, accompanying text, imagery, and context. The article describes the behavioral consequence of broken scent: users abandon pages that lack sufficient context or that fail to deliver on the link's implied promise, skipping further interaction when relevance is unclear. The article also warns that misleading link labels erode trust, making users less likely to click on genuinely relevant content in future. While the article frames the concept in navigation terms, the same mechanism applies when an advertisement or organic search result creates an expectation that the landing page does not fulfill.
**Sources:**
- Nielsen Norman Group, "Information Scent: How Users Decide Where to Go Next" — https://www.nngroup.com/articles/information-scent/
**Applies when:** campaign landing pages reached via paid ads, email links, or organic search results where the source message sets a specific expectation.

## EV-CONV-003: Feature a single primary call to action
**Strength:** convention
**Claim:** Give the page one clearly dominant primary action and ensure it is visually more prominent than any secondary links or options. Competing actions at similar visual weight divide attention, making it harder for users to know what to do next, which adds cognitive load and can reduce completion.
**Evidence:** NN/g's "Minimize Cognitive Load to Maximize Usability" establishes that human working memory is limited and that every decision a design asks users to make consumes cognitive resources. The article recommends looking for anything that requires a decision and finding ways to reduce that burden, because when cognitive demands exceed capacity users may take longer, miss important details, or abandon. NN/g's "Visual Hierarchy in UX: Definition" supports the structural principle: it states that when design elements compete at equal visual weight — similar size, colour, and spacing — users struggle to identify where to focus first, and recommends giving one element a clear size, contrast, or spacing advantage over all others. Together, these sources underpin the convention that a landing page with one clearly dominant action is easier to act on than one with several competing options at similar prominence.
**Sources:**
- Nielsen Norman Group, "Minimize Cognitive Load to Maximize Usability" — https://www.nngroup.com/articles/minimize-cognitive-load/
- Nielsen Norman Group, "Visual Hierarchy in UX: Definition" — https://www.nngroup.com/articles/visual-hierarchy-ux-definition/
**Applies when:** goal-driven landing pages with a single conversion objective.
**Exception:** Pages serving genuinely distinct audiences (for example, a homepage that must route both consumers and businesses) may need two clearly ranked paths, provided the hierarchy between them is visually explicit.

## EV-CONV-004: Make copy scannable
**Strength:** research-backed
**Claim:** Use short paragraphs, meaningful subheadings, and front-loaded key words. Users scan rather than read web pages linearly, so placing the most important information early in each block and structuring content for rapid scanning substantially improves usability.
**Evidence:** NN/g's "How Users Read on the Web" found that 79% of test users always scanned any new page they encountered; only 16% read word by word. A controlled experiment compared five variants of the same web content and found measurable usability differences: a concise version produced 58% better usability scores, a scannable layout produced 47% better scores, and a version combining both techniques with objective language produced 124% better scores than the baseline. The article recommends one idea per paragraph (as users skip over additional ideas if the first words do not catch their attention), meaningful rather than clever subheadings, and starting sentences and headings with the words carrying the most information.
**Sources:**
- Nielsen Norman Group, "How Users Read on the Web" — https://www.nngroup.com/articles/how-users-read-on-the-web/
**Applies when:** any marketing or landing page copy.

## EV-CONV-005: Provide credible social proof near decision points
**Strength:** convention
**Claim:** Include specific, credible evidence of adoption or endorsement — such as named testimonials, third-party review references, real usage numbers, or recognisable logos — positioned near the primary call to action or sign-up form. Social proof reduces decision-making uncertainty by showing that others have already made the same choice.
**Evidence:** NN/g's "Social Proof in the User Experience" explains that people reference the behaviour of others to guide their own decisions, and that adding an indication that other people like a product or piece of content can remove decision-making uncertainty. The article also documents a failure mode: displaying a low count (such as 1,000 shares on an article) can backfire by suggesting the content lacks value, so social proof is most effective when numbers are substantial or qualitative signals are specific and credible. NN/g's "Trustworthy Design" reports that participants consistently preferred reviews and endorsements from external sources over company-hosted testimonials, and that an isolated website lacking external connections appears less established and less trustworthy. These sources collectively support the convention that specific, credible social signals near a conversion point reduce the perceived risk of acting.
**Sources:**
- Nielsen Norman Group, "Social Proof in the User Experience" — https://www.nngroup.com/articles/social-proof-ux/
- Nielsen Norman Group, "Trustworthy Design" — https://www.nngroup.com/articles/trustworthy-design/
**Applies when:** landing pages asking visitors to sign up, purchase, or commit to an action where trust is a factor.
**Exception:** Low or unverifiable social proof signals can reduce rather than increase confidence; include social proof only when the numbers and sources are genuinely credible and independently verifiable.

## EV-CONV-006: Guide the eye toward the primary call to action
**Strength:** convention
**Claim:** Use visual hierarchy, whitespace, and spatial relationships so the layout leads the user's eye from the headline through supporting content to the primary action. The primary CTA should be the most visually prominent interactive element on the page.
**Evidence:** NN/g's "Visual Hierarchy in UX: Definition" states that visual hierarchy controls the delivery of information from the system to the user, and that it lets users know where to focus their attention. The article establishes that larger elements attract attention first; bright, saturated colours emphasise important items while less-saturated colours serve secondary content; and whitespace between groups separates sections and guides the eye. It warns that when elements compete at equal weight — similar size, colour, and spacing — users struggle to identify where to focus. Applying these principles means the primary CTA should be the largest, most saturated, or most visually distinct interactive element on the page, with whitespace creating breathing room that draws attention to it. This claim ties directly to EV-LAYOUT-001, which covers establishing a clear visual hierarchy, and EV-LAYOUT-003, which covers matching visual prominence to task priority.
**Sources:**
- Nielsen Norman Group, "Visual Hierarchy in UX: Definition" — https://www.nngroup.com/articles/visual-hierarchy-ux-definition/
**Applies when:** landing pages with a primary conversion action.

## EV-CONV-007: Reduce form friction on conversion pages
**Strength:** convention
**Claim:** Ask for the fewest fields necessary on any form embedded in a landing page. Each additional field increases the effort required to complete the form and lowers the likelihood of completion.
**Evidence:** Baymard Institute's large-scale benchmark and usability testing of e-commerce checkout flows provides the empirical basis for the underlying principle. Baymard found that the average site presents around 11.3 form fields when most need only 8 — roughly 40% more than necessary — and that 17% of users reported abandoning a checkout because the process was too long or complicated. The principle established by this data is that each unnecessary field is a friction point and a potential abandonment trigger. That principle is the same mechanism operating in lead-capture, email sign-up, free-trial, and other landing-page forms: unnecessary fields raise effort, and raised effort lowers completion. Applying a checkout-derived benchmark to landing-page forms is an extension by convention — the mechanism is identical, but no landing-page-specific study has been cited here. Strength is therefore `convention`, not `research-backed`. See also EV-FORM-012, which covers minimising form fields in checkout in more detail.
**Sources:**
- Baymard Institute, "Checkout Optimization: 5 Ways to Minimize Form Fields in Checkout" (data: 2024) — https://baymard.com/blog/checkout-flow-average-form-fields
**Applies when:** landing pages that include a form for lead capture, email sign-up, free trial, or similar conversion action.
