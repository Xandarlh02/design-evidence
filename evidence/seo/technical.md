# SEO evidence: technical fundamentals

This file covers technical SEO practices that affect how Google crawls, indexes, and ranks pages: mobile-first indexing, Core Web Vitals, image alt text and optimisation, structured data, and canonicalisation. EV-SEO-006 and EV-SEO-007 are backed by Google Search Central and web.dev guidance and are labelled `convention`. EV-SEO-008 is backed by WCAG 1.1.1 (Level A) as primary source and Google image guidance as co-source; the alt text requirement is labelled `standard` because it derives from a normative accessibility standard, while the image optimisation guidance is a Google convention. EV-SEO-009 and EV-SEO-010 are backed by Google Search Central guidance and are labelled `convention`.

## EV-SEO-006: Make pages mobile-friendly
**Strength:** convention
**Claim:** Serve responsive, mobile-usable pages. Google predominantly uses the mobile version of a page's content — crawled with its smartphone agent — for indexing and ranking, so a page that renders poorly or incompletely on mobile risks ranking on the basis of a degraded or missing experience.
**Evidence:** Google Search Central documentation on mobile-first indexing states that Google uses the mobile version of a site's content for indexing and ranking, and that only the content shown on the mobile site is used for indexing. The guidance recommends responsive web design as the easiest pattern to implement and maintain, and requires that the mobile and desktop versions contain equivalent primary content — removing content from the mobile version can cause traffic loss because that content is not indexed.
**Sources:**
- Google Search Central, "Mobile-first indexing best practices" — https://developers.google.com/search/docs/crawling-indexing/mobile/mobile-sites-mobile-first-indexing
**Applies when:** every indexable page.

## EV-SEO-007: Meet Core Web Vitals thresholds
**Strength:** convention
**Claim:** Optimise loading performance (LCP), interactivity (INP), and visual stability (CLS) to meet the "good" thresholds: LCP within 2.5 seconds, INP at or below 200 milliseconds, and CLS at or below 0.1. These thresholds are measured at the 75th percentile of page loads across mobile and desktop. Page experience, of which Core Web Vitals is the primary measurable component, is a consideration in Google's ranking systems.
**Evidence:** The web.dev Web Vitals article defines the "good" bands for each metric: LCP should occur within 2.5 seconds of when the page first starts loading; INP should be 200 milliseconds or less; and CLS should be 0.1 or less. The article specifies that thresholds should be met at the 75th percentile of page loads, segmented across mobile and desktop devices, and that field measurement data — actual user experiences rather than lab tests — is used to assess them. Google's page experience documentation states that Core Web Vitals are used by its ranking systems, and that a strong page experience can contribute to success in Search, particularly when multiple pages offer similarly relevant content.
**Sources:**
- web.dev, "Web Vitals" — https://web.dev/articles/vitals
- Google Search Central, "Understanding page experience in Google Search results" — https://developers.google.com/search/docs/appearance/page-experience
**Applies when:** production pages served to real users.

## EV-SEO-008: Provide descriptive alt text and optimised images
**Strength:** standard
**Claim:** Give informative images descriptive alt text that conveys equivalent information to a user who cannot see the image. Additionally, serve appropriately sized and compressed image files using modern formats and responsive image techniques, as images are often the largest contributor to page size.
**Evidence:** WCAG 2.1 SC 1.1.1 (Non-text Content, Level A) requires that all non-text content presented to the user has a text alternative that serves the equivalent purpose. For purely decorative images — those used only for visual formatting or not presented to users — the standard requires that they be implemented in a way that allows assistive technology to ignore them, such as with a null alt attribute (alt=""). As co-source, Google Images best practices documentation identifies alt text as the most important attribute for providing metadata about an image, and recommends writing useful, information-rich descriptions that use keywords appropriately and in context. The same Google guidance notes that images are often the largest contributor to overall page size, and recommends applying image optimisation and responsive image techniques — including the use of srcset and the picture element — to balance quality and load performance.
**Sources:**
- W3C, "Understanding SC 1.1.1: Non-text Content (Level A)" — https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html
- Google Search Central, "Google Images best practices" — https://developers.google.com/search/docs/appearance/google-images
**Applies when:** pages with images.
**Exception:** Purely decorative images that convey no information should use an empty alt attribute (alt="") so assistive technology skips them.

## EV-SEO-009: Add structured data where the content type supports it
**Strength:** convention
**Claim:** Mark up eligible content — such as products, articles, FAQs, and breadcrumbs — with valid schema.org structured data to enable rich results in Google Search. Rich results are visually enhanced listings that can meaningfully improve click-through rates.
**Evidence:** Google's introduction to structured data describes it as a standardised format for providing information about a page and classifying page content, enabling Google to understand the content and display it in richer search result features. The documentation presents several named case studies of sites that implemented structured data — including measured improvements in click-through rates and engagement — but results vary by site and content type, so structured data can improve click-through rates without guaranteeing a consistent lift. The guidance also states explicitly that structured data should not be added for information that is not visible to the user on the page, even if the information is accurate.
**Sources:**
- Google Search Central, "Intro to structured data markup" — https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data
**Applies when:** pages whose content maps to a supported schema.org type (products, articles, FAQs, breadcrumbs, events, and similar).
**Exception:** Do not add structured data markup for content that is not visible on the page.

## EV-SEO-010: Set a canonical URL for duplicate or near-duplicate pages
**Strength:** convention
**Claim:** Designate a canonical URL when the same content is reachable at multiple URLs, to consolidate ranking signals — including links — under a single preferred URL and avoid splitting authority across duplicates.
**Evidence:** Google Search Central documentation on consolidating duplicate URLs explains that specifying a canonical URL allows Google to consolidate the signals it has for individual URLs, such as links to them, into a single preferred URL. The documentation ranks canonicalization methods by signal strength: permanent redirects are the strongest signal, followed by the rel="canonical" link annotation in the page's HTML head (also a strong signal), with sitemap inclusion providing only a weak signal. Google will automatically identify what it considers the optimal canonical version if no preference is specified; explicit canonicalization is not required but gives publishers direct control over which URL is consolidated in Search results.
**Sources:**
- Google Search Central, "Consolidate duplicate URLs" — https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls
**Applies when:** sites with the same content accessible at multiple URLs, including parameterised URLs, protocol variants (HTTP/HTTPS), and trailing-slash variants.
**Exception:** Canonicalization signals are optional. Google will select a canonical automatically if none are specified, but without explicit signals the publisher cedes control over which URL Google treats as preferred.
