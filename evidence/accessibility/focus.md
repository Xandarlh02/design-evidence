# Accessibility evidence: keyboard focus

This file covers WCAG 2.2 requirements for keyboard operability and focus management. The claims address focus visibility, focus order, the prohibition on keyboard traps, and the requirement that all functionality be reachable by keyboard alone. Each claim cites the relevant W3C Understanding document; all are normative Level A or AA requirements under WCAG 2.2.

## EV-A11Y-005: Keyboard focus must be visibly indicated
**Strength:** standard
**Claim:** Any keyboard-operable interface must have a mode in which the focus indicator is visible, showing keyboard users which element will receive their next input.
**Evidence:** WCAG 2.2 SC 2.4.7 Focus Visible (Level AA) requires that the pixels changed to indicate a focused state are perceptible at all times during keyboard navigation. The criterion applies to all keyboard-operable elements; removing the browser's default outline without providing an equivalent replacement indicator violates this requirement.
**Sources:**
- W3C, "Understanding SC 2.4.7: Focus Visible", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/focus-visible.html
**Applies when:** all interactive elements reachable by keyboard, including links, buttons, form controls, and custom components.

## EV-A11Y-006: Focus order must follow the meaning and reading order of the page
**Strength:** standard
**Claim:** Focusable components must receive focus in an order that preserves the meaning and operability of the page.
**Evidence:** WCAG 2.2 SC 2.4.3 Focus Order (Level A) requires that sequential keyboard navigation moves through interactive elements in an order consistent with the content's logical relationships. The criterion does not mandate that focus order mirror the visual layout exactly; it requires only that the sequence preserve meaning and allow the user to control the interface effectively. Multiple valid orderings are acceptable provided both conditions are met.
**Sources:**
- W3C, "Understanding SC 2.4.3: Focus Order", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/focus-order.html
**Applies when:** any page or view with more than one focusable element, and especially when DOM order diverges from visual order through CSS positioning or dynamic insertion.

## EV-A11Y-007: Keyboard users must never get trapped in a component
**Strength:** standard
**Claim:** If keyboard focus can be moved into a component, it must also be possible to move focus away from that component using only the keyboard. If a non-standard key combination is required to exit, users must be told what it is.
**Evidence:** WCAG 2.2 SC 2.1.2 No Keyboard Trap (Level A) states that focus must be escapable from any component a keyboard user can enter. Exiting via Tab, arrow keys, or standard methods such as Escape requires no additional disclosure. If a non-standard keystroke is needed, the interface must advise users of that method before they become trapped.
**Sources:**
- W3C, "Understanding SC 2.1.2: No Keyboard Trap", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/no-keyboard-trap.html
**Applies when:** modal dialogs, date pickers, custom select menus, carousels, and any component that captures or constrains keyboard focus.

## EV-A11Y-008: All functionality must be operable by keyboard alone
**Strength:** standard
**Claim:** Every action available via pointer must also be available through a keyboard interface, without requiring specific timing for individual keystrokes.
**Evidence:** WCAG 2.2 SC 2.1.1 Keyboard (Level A) requires that all content functionality be operable through a keyboard interface. The sole exception covers functions whose underlying operation is inherently path-dependent — such as freehand drawing — rather than endpoint-dependent. Tasks such as resizing, dragging to a specific location, and selecting text do not qualify for the exception because they require only endpoint information, not a continuous movement path.
**Sources:**
- W3C, "Understanding SC 2.1.1: Keyboard", WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/keyboard.html
**Applies when:** all interactive functionality, including drag-and-drop, hover menus, gesture-triggered actions, and any control activated by mouse or touch.
**Exception:** Functions that inherently depend on the path of the user's movement and not just the start and end points — for example, freehand drawing or handwriting input.
