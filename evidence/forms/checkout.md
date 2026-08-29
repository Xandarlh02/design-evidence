# Forms evidence: checkout flow design

This file covers design decisions that affect checkout completion rates and abandonment. The claims address guest checkout, cost transparency, form field count, and form layout. Each claim is drawn from Baymard Institute large-scale benchmark data and usability testing across major e-commerce sites.

## EV-FORM-010: Offer guest checkout; forced account creation causes abandonment
**Strength:** research-backed
**Claim:** Always provide a guest checkout path. Requiring users to create an account before purchasing is a significant cause of checkout abandonment.
**Evidence:** Baymard Institute's cart abandonment survey found that 18% of users abandoned a checkout specifically because the site required account creation. This figure comes from a survey of users who had intended to complete a purchase, isolating design-caused abandonment from browsing intent.
**Sources:**
- Baymard Institute, "Cart Abandonment Rate Statistics", 2024 — https://baymard.com/lists/cart-abandonment-rate
**Applies when:** any e-commerce or transactional checkout flow.

## EV-FORM-011: Show all costs as early as possible; surprise costs are the leading abandonment reason
**Strength:** research-backed
**Claim:** Display shipping costs, taxes, and fees before the final checkout step. Unexpected extra costs are the single largest identifiable driver of checkout abandonment.
**Evidence:** Baymard Institute's abandonment survey found that 40% of users abandoned because extra costs (shipping, tax, fees) were too high, and a further 12% left because they could not see or calculate the total order cost up-front. Together, cost surprise accounts for a larger share of intentional abandonment than any other single factor on the list.
**Sources:**
- Baymard Institute, "Cart Abandonment Rate Statistics", 2024 — https://baymard.com/lists/cart-abandonment-rate
**Applies when:** any checkout that involves variable shipping, tax, or additional fees.

## EV-FORM-012: Minimize the number of form fields in checkout
**Strength:** research-backed
**Claim:** Reduce visible checkout form fields to the minimum needed. The average site presents roughly 40% more fields than necessary, and checkout complexity drives measurable abandonment.
**Evidence:** Baymard Institute's 2024 benchmark measured an average of 11.3 form fields across major e-commerce checkout flows, and found that most sites require only 8 fields to collect the necessary information. Separately, 17% of users reported abandoning a checkout because the process was too long or complicated. Baymard identifies five specific field-reduction opportunities — combining name fields, hiding Address Line 2 by default, hiding coupon codes, collapsing billing address fields, and deferring account creation — that the majority of sites fail to implement.
**Sources:**
- Baymard Institute, "Checkout Flow Average Form Fields", 2024 — https://baymard.com/blog/checkout-flow-average-form-fields
**Applies when:** any multi-field checkout form.

## EV-FORM-013: Use a single-column layout for forms
**Strength:** research-backed
**Claim:** Lay out checkout and other multi-field forms in a single column. Multi-column layouts cause users to skip required fields, misinterpret field relationships, and make more errors.
**Evidence:** Baymard Institute's usability testing across multiple rounds of checkout studies found that single-column layouts resulted in fewer skipped fields, fewer misinterpreted fields, and fewer errors compared to multi-column layouts. Users in testing struggled to determine which fields to complete across columns, and their attention was drawn in competing directions. Baymard notes that placing two or three logically related short fields on one row (such as city, state, and postcode) does not cause the same problems, distinguishing that pattern from a full two-column form layout. Despite this evidence, 16% of sites in their benchmark still use extensive multi-column forms.
**Sources:**
- Baymard Institute, "Avoid Multi-Column Forms", 2024 — https://baymard.com/blog/avoid-multi-column-forms
**Applies when:** any form with multiple fields, particularly checkout and registration forms.
**Exception:** Grouping two or three closely related short fields on a single row (e.g. expiry date and CVV, or city and postcode) is acceptable when the relationship is obvious to the user.
