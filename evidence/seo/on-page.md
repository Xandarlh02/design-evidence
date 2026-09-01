# SEO evidence: on-page fundamentals

This file covers core on-page SEO practices: page titles, meta descriptions, heading structure, semantic HTML landmarks, and descriptive link text. EV-SEO-001 and EV-SEO-002 are backed by Google Search Central documentation and are labelled `convention`. EV-SEO-003 is backed by Google guidance and is labelled `convention`; the heading-hierarchy point overlaps WCAG 1.3.1 but is cited here via the SEO Starter Guide. EV-SEO-004 is backed by WCAG 1.3.1 SC (Info and Relationships) and is labelled `standard` because the SEO Starter Guide does not address HTML landmark elements specifically. EV-SEO-005 is backed by WCAG 2.4.4 SC (Link Purpose) as primary source with Google SEO guidance as co-source, and is labelled `standard`.

## EV-SEO-001: Write a unique, descriptive title for each page
**Strength:** convention
**Claim:** Give every indexable page a unique title element that accurately describes its content. The title becomes the primary link shown in search results; vague or repeated titles make pages indistinguishable to both users and Google.
**Evidence:** Google Search Central guidance on title links states that title text should be descriptive and concise, and warns against vague descriptors such as "Home" for a home page or repeated boilerplate text that makes pages impossible for users to tell apart. The same guidance notes that Google generates title links automatically and may override a title it finds inaccurate, outdated, or unclear — making an accurate, specific title the best input a publisher can supply.
**Sources:**
- Google Search Central, "Influencing your title links in search results" — https://developers.google.com/search/docs/appearance/title-link
**Applies when:** every indexable page.

## EV-SEO-002: Write a useful meta description
**Strength:** convention
**Claim:** Provide a concise, accurate meta description that summarises the page's content. Google may use it as the snippet shown beneath the title link in search results, and a clear description can improve click-through.
**Evidence:** Google Search Central guidance on snippets explains that Google sometimes uses the meta description tag when it would give users a more accurate description of the page than content taken directly from the page. The guidance recommends creating a distinct description for each page and avoiding keyword stuffing, and warns that snippets may still be generated automatically from page content regardless of the meta description provided. The length of any displayed snippet is truncated to fit the device width.
**Sources:**
- Google Search Central, "Control your snippets in search results" — https://developers.google.com/search/docs/appearance/snippet
**Applies when:** pages you want to influence the snippet for.
**Exception:** Google may generate its own snippet from page content even when a meta description is present.

## EV-SEO-003: Use one clear H1 and a logical heading outline
**Strength:** convention
**Claim:** Structure content with a single descriptive H1 and properly nested headings so both users and crawlers can understand the page. Having headings in semantic order aids screen readers; a clear outline also signals content structure to Google.
**Evidence:** Google's SEO Starter Guide advises breaking up long content into paragraphs and sections with headings to help users navigate pages. The guide notes that having headings in semantic order is beneficial for screen readers. It clarifies that Google Search does not penalise out-of-order headings, because the web generally does not produce fully valid HTML, but the intent is clear: logical, descriptive heading structure helps both users and search engines understand the page hierarchy.
**Sources:**
- Google Search Central, "SEO Starter Guide" — https://developers.google.com/search/docs/fundamentals/seo-starter-guide
**Applies when:** content pages with more than a single block of text.

## EV-SEO-004: Use semantic HTML landmarks
**Strength:** standard
**Claim:** Use real semantic elements (header, nav, main, footer, and heading tags) rather than generic divs so content structure is machine-readable for assistive technologies and search engines.
**Evidence:** WCAG 2.1 SC 1.3.1 (Info and Relationships, Level A) requires that information, structure, and relationships conveyed through presentation can be programmatically determined or are available in text. The understanding document explains that sighted users perceive structure through visual cues such as larger bold headings and bulleted list items, but that these visual patterns must be reinforced with semantic markup so screen readers and other assistive technologies can detect the same relationships. Using heading elements H1 through H6 is listed as a sufficient technique for meeting this criterion. Using landmark HTML elements to convey structure fulfils the same principle: a div styled to look like a navigation region is not programmatically equivalent to a nav element.
**Sources:**
- W3C, "Understanding SC 1.3.1: Info and Relationships (Level A)" — https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html
**Applies when:** any page with structural regions (navigation, main content, header, footer).

## EV-SEO-005: Write descriptive link text
**Strength:** standard
**Claim:** Link text should describe the destination or action; avoid generic phrases such as "click here" or bare URLs. Descriptive link text helps keyboard and screen reader users navigate efficiently and tells search engines what the linked page is about.
**Evidence:** WCAG 2.1 SC 2.4.4 (Link Purpose In Context, Level AA) requires that the purpose of each link can be determined from the link text alone, or from the link text together with its programmatically determined link context. The understanding document identifies three groups of users who benefit: those with motion impairments who can skip unwanted links, those with cognitive limitations who avoid disorientation from ambiguous links, and those with visual disabilities who determine link purpose without seeing surrounding content. The understanding document also notes that meaningful link text helps users who tab from link to link. As a co-source, Google's SEO Starter Guide explains that anchor text tells users and Google something about the page being linked to and that good anchor text lets people and search engines understand what a linked page contains before they visit it.
**Sources:**
- W3C, "Understanding SC 2.4.4: Link Purpose (In Context) (Level AA)" — https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html
- Google Search Central, "SEO Starter Guide" — https://developers.google.com/search/docs/fundamentals/seo-starter-guide
**Applies when:** all links.
