# Accessibility evidence: semantics and ARIA

This file covers the use of semantic HTML and ARIA in building accessible interfaces. The claims address the primacy of native HTML elements, the requirement for programmatic label associations, image alternatives, heading structure, and the use of live regions to communicate dynamic content changes to assistive technology users.

## EV-A11Y-012: Prefer native HTML elements over ARIA roles (the first rule of ARIA)
**Strength:** standard
**Claim:** If a native HTML element or attribute already provides the required semantics and behaviour, use it rather than repurposing a generic element with ARIA roles, states, or properties.
**Evidence:** The W3C "Using ARIA" document opens with Rule 1: "If you can use a native HTML element or attribute with the semantics and behavior you require already built in, instead of re-purposing an element and adding an ARIA role, state or property to make it accessible, then do so." Three exceptions permit ARIA when the feature is not yet implemented by browsers, when visual design constraints rule out the native element, or when the required semantic does not exist in HTML.
**Sources:**
- W3C, "Using ARIA", Rule 1 — https://www.w3.org/TR/using-aria/#rule1
**Applies when:** any component that could be built with either a native HTML element or a custom element enhanced with ARIA.

## EV-A11Y-013: Every input needs a programmatically associated label
**Strength:** standard
**Claim:** Each form input must have an accessible name that assistive technology can determine programmatically, established through a `<label>` element, `aria-label`, `aria-labelledby`, or an equivalent technique.
**Evidence:** WCAG 2.2 SC 1.3.1 Information and Relationships (Level A) requires that structure and relationships conveyed through presentation be programmatically determinable; SC 4.1.2 Name, Role, Value (Level A) additionally requires that the name of every user interface component can be determined by assistive technologies. Together they mandate that form inputs carry a discoverable label — a visible `<label>` associated by `for`/`id`, a fieldset and legend for grouped controls, or an ARIA attribute where no label element can be used.
**Sources:**
- W3C, "Understanding SC 1.3.1: Info and Relationships", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships.html
- W3C, "Understanding SC 4.1.2: Name, Role, Value", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html
**Applies when:** all form controls including text inputs, checkboxes, radio buttons, select menus, and custom widgets that accept user input.
**Exception:** Inputs whose purpose is entirely clear from surrounding context and whose role is defined in the UI — rare in practice and difficult to demonstrate reliably; prefer explicit labelling.

## EV-A11Y-014: Informative images need meaningful alt text; decorative images need empty alt
**Strength:** standard
**Claim:** Images that convey information must have a text alternative describing that information; images that are purely decorative must have an empty `alt` attribute so assistive technology ignores them.
**Evidence:** WCAG 2.2 SC 1.1.1 Non-text Content (Level A) requires that all non-text content presented to the user has a text alternative that serves the equivalent purpose. For informative images this means alt text that conveys the same information the image conveys; for decorative images — those adding only visual styling without contributing meaning — the correct implementation is an empty `alt=""` with no title attribute, which signals assistive technology to skip the element entirely.
**Sources:**
- W3C, "Understanding SC 1.1.1: Non-text Content", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html
- W3C WAI, "Images Tutorial" — https://www.w3.org/WAI/tutorials/images/
**Applies when:** all `<img>` elements, SVG graphics, and CSS background images used to convey content or decoration in web interfaces.
**Exception:** CAPTCHA images and images used in tests where a text alternative would invalidate the purpose; these require an alternative form of access rather than descriptive alt text.

## EV-A11Y-015: Use a logical heading hierarchy; screen reader users navigate by headings
**Strength:** research-backed
**Claim:** Structure page content with a logical heading hierarchy because the majority of screen reader users rely on heading navigation as their primary strategy for finding information on a page.
**Evidence:** WebAIM's Screen Reader User Survey 10 found that 71.6% of respondents use headings as their primary method when trying to find information on a lengthy web page — the most common approach by a wide margin over alternatives such as using Find (13.6%) or reading sequentially (6.4%). A disordered or skipped heading structure therefore prevents the most common navigation path available to screen reader users.
**Sources:**
- WebAIM, "Screen Reader User Survey 10", 2024 — https://webaim.org/projects/screenreadersurvey10/
**Applies when:** any page or view with multiple sections of content where headings are used to organise the information hierarchy.
**Exception:** Single-topic pages or application views with no meaningful content sections may not require a multi-level heading structure, but a page-level `<h1>` is still required.

## EV-A11Y-016: Announce dynamic content updates with ARIA live regions
**Strength:** standard
**Claim:** When content changes on a page without a full navigation — status messages, search results, error notifications, chat messages — mark the update container with `aria-live` so assistive technologies announce the change without requiring the user to move focus.
**Evidence:** WAI-ARIA 1.2 defines live regions as perceivable areas of a page that are typically updated as a result of an external event when user focus may be elsewhere. Authors mark a container with `aria-live="polite"` for updates that should be announced at the next opportunity without interrupting the current speech, or `aria-live="assertive"` (equivalent to `role="alert"`) for urgent messages that must interrupt immediately. The live region container must be present in the DOM before content is injected so that assistive technology registers the region at load time.
**Sources:**
- W3C, "Accessible Rich Internet Applications (WAI-ARIA) 1.2", aria-live property — https://www.w3.org/TR/wai-aria-1.2/#aria-live
- W3C WAI, "ARIA19: Using ARIA role=alert or Live Regions to Identify Errors" — https://www.w3.org/WAI/WCAG21/Techniques/aria/ARIA19
**Applies when:** single-page applications and any interface where content, status, or errors are injected into the DOM after initial page load without triggering a full navigation.
**Exception:** Focus-managed flows such as modal dialogs where focus is moved programmatically to the updated content do not require a live region; the focus movement itself announces the change.
