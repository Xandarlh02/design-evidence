# Usability heuristics evidence: Nielsen's 10

This file covers Jakob Nielsen's ten usability heuristics as a whole-screen review lens. These heuristics are expert-distilled principles, not claims derived from a single controlled study, so they are labelled `convention`. They function as a holistic checklist: apply them when reviewing any interactive screen for broad usability problems.

## EV-HEUR-001: Visibility of system status
**Strength:** convention
**Claim:** Always keep users informed about what the system is doing by providing timely, appropriate feedback about the outcome of each action.
**Evidence:** Nielsen Norman Group describes this heuristic as the obligation for a design to keep users continuously informed about what is happening. When users understand the current system state, they can interpret the outcome of their previous actions and plan their next steps with confidence. Predictable feedback builds trust in both the product and the brand.
**Sources:**
- Jakob Nielsen, "10 Usability Heuristics for User Interface Design," Nielsen Norman Group, 1994 (updated) — https://www.nngroup.com/articles/ten-usability-heuristics/
**Applies when:** any interactive UI where an action triggers a process, state change, or navigation.

## EV-HEUR-002: Match between the system and the real world
**Strength:** convention
**Claim:** Use language, concepts, and conventions that match users' real-world mental models; avoid internal jargon and present information in a natural, logical order.
**Evidence:** Nielsen Norman Group states that a design should speak the user's language, using words, phrases, and concepts familiar to the target audience rather than system-oriented terminology. Terms that are clear to designers and developers may be confusing to users. When controls and labels correspond to real-world conventions and lead to expected outcomes, the interface feels intuitive and is easier to learn.
**Sources:**
- Jakob Nielsen, "10 Usability Heuristics for User Interface Design," Nielsen Norman Group, 1994 (updated) — https://www.nngroup.com/articles/ten-usability-heuristics/
**Applies when:** any interactive UI, especially where labels, icons, or interaction patterns may draw on domain-specific or technical vocabulary unfamiliar to the target audience.

## EV-HEUR-003: User control and freedom
**Strength:** convention
**Claim:** Provide a clearly marked way to undo or exit any action or process so that users can recover from mistakes without penalty.
**Evidence:** Nielsen Norman Group notes that users frequently trigger actions by mistake and need a clearly marked exit that lets them leave an unwanted state without going through a lengthy process. When backing out is easy, users feel in control and confident rather than stuck or frustrated. This freedom to reverse actions reduces the cost of errors.
**Sources:**
- Jakob Nielsen, "10 Usability Heuristics for User Interface Design," Nielsen Norman Group, 1994 (updated) — https://www.nngroup.com/articles/ten-usability-heuristics/
**Applies when:** any interactive UI with multi-step flows, destructive actions, or state-changing operations.

## EV-HEUR-004: Consistency and standards
**Strength:** convention
**Claim:** Follow platform and industry conventions so that users do not have to re-learn what words, icons, or actions mean when moving through a product.
**Evidence:** Nielsen Norman Group points out that users spend the majority of their time with other digital products, and those experiences set their expectations. When a design breaks from established conventions, users must expend extra cognitive effort to learn a new pattern. Inconsistency across an interface — or between the interface and platform norms — raises cognitive load unnecessarily.
**Sources:**
- Jakob Nielsen, "10 Usability Heuristics for User Interface Design," Nielsen Norman Group, 1994 (updated) — https://www.nngroup.com/articles/ten-usability-heuristics/
**Applies when:** any interactive UI, particularly when introducing custom patterns, iconography, or terminology that deviates from platform or category norms.

## EV-HEUR-005: Error prevention
**Strength:** convention
**Claim:** Design to prevent errors before they occur by eliminating error-prone conditions or requiring confirmation before a consequential action is committed.
**Evidence:** Nielsen Norman Group describes two categories of error: slips, which are unconscious mistakes caused by inattention, and mistakes, which arise from a mismatch between the user's mental model and how the design actually works. The heuristic holds that good error messages matter, but the best designs remove or guard against error-prone conditions in the first place, either by eliminating the conditions entirely or by surfacing a confirmation step before a consequential action is committed.
**Sources:**
- Jakob Nielsen, "10 Usability Heuristics for User Interface Design," Nielsen Norman Group, 1994 (updated) — https://www.nngroup.com/articles/ten-usability-heuristics/
**Applies when:** any interactive UI, especially forms, destructive actions, irreversible operations, and flows with costly mistakes.

## EV-HEUR-006: Recognition rather than recall
**Strength:** convention
**Claim:** Make options, actions, and required information visible or easily retrievable so that users do not have to remember details from one part of the interface to another.
**Evidence:** Nielsen Norman Group states that human short-term memory is limited, and interfaces should minimise the memory load placed on users by keeping relevant elements, actions, and options visible. Users should not need to recall information from one context to use it in another; anything required to complete a task should be present or easily surfaced. Designs that favour recognition over recall reduce the cognitive effort required.
**Sources:**
- Jakob Nielsen, "10 Usability Heuristics for User Interface Design," Nielsen Norman Group, 1994 (updated) — https://www.nngroup.com/articles/ten-usability-heuristics/
**Applies when:** any interactive UI, particularly navigation menus, multi-step workflows, and any interface that requires users to carry information across screens or states.

## EV-HEUR-007: Flexibility and efficiency of use
**Strength:** convention
**Claim:** Support both novice and expert users by offering shortcuts and the ability to tailor frequent actions, without exposing that complexity to users who do not need it.
**Evidence:** Nielsen Norman Group explains that shortcuts, which may be invisible to novice users, allow experienced users to perform frequent actions much faster. Flexible processes can be carried out in more than one way so that each person can use the method that works best for them. A design that accommodates both ends of the expertise spectrum serves a broader user population without overwhelming beginners.
**Sources:**
- Jakob Nielsen, "10 Usability Heuristics for User Interface Design," Nielsen Norman Group, 1994 (updated) — https://www.nngroup.com/articles/ten-usability-heuristics/
**Applies when:** any interactive UI used by a range of users, particularly productivity tools, dashboards, and applications where returning users perform repetitive tasks.

## EV-HEUR-008: Aesthetic and minimalist design
**Strength:** convention
**Claim:** Remove or de-emphasise any information, decoration, or interface element that does not support the user's primary task, because every non-essential element competes for attention with the essential ones.
**Evidence:** Nielsen Norman Group states that every extra unit of information in an interface competes with the relevant information and reduces its relative visibility. This heuristic is not a mandate for flat or sparse visual design; it is about keeping content and visual elements focused on what users actually need to accomplish. Decorative or irrelevant elements dilute the signal of what matters.
**Sources:**
- Jakob Nielsen, "10 Usability Heuristics for User Interface Design," Nielsen Norman Group, 1994 (updated) — https://www.nngroup.com/articles/ten-usability-heuristics/
**Applies when:** any interactive UI; applies most acutely to high-density screens, dashboards, and landing pages where attention is scarce.

## EV-HEUR-009: Help users recognize, diagnose, and recover from errors
**Strength:** convention
**Claim:** Write error messages in plain language, precisely identify the problem, and suggest a constructive path to resolution; present them with visual treatment that ensures they are noticed.
**Evidence:** Nielsen Norman Group states that error messages should use plain language rather than codes, pinpoint the specific problem, and offer a concrete suggestion for how to fix it. Beyond the message text, the visual presentation of errors matters: error states need to be displayed in a way that users will notice and recognise as requiring their attention.
**Sources:**
- Jakob Nielsen, "10 Usability Heuristics for User Interface Design," Nielsen Norman Group, 1994 (updated) — https://www.nngroup.com/articles/ten-usability-heuristics/
**Applies when:** any interactive UI that can produce error states, particularly forms, authentication flows, and system-triggered failure conditions.

## EV-HEUR-010: Help and documentation
**Strength:** convention
**Claim:** When users need additional support to complete a task, provide documentation that is easy to search, focused on the user's goal, concise, and structured as concrete steps.
**Evidence:** Nielsen Norman Group notes that the ideal design requires no additional explanation, but acknowledges that documentation is sometimes necessary. When it is provided, help content should be searchable and task-focused rather than system-centric, kept concise, and presented as concrete steps the user can follow rather than as general reference material.
**Sources:**
- Jakob Nielsen, "10 Usability Heuristics for User Interface Design," Nielsen Norman Group, 1994 (updated) — https://www.nngroup.com/articles/ten-usability-heuristics/
**Applies when:** complex or specialised interfaces where users may need guidance, onboarding flows, and any screen that handles infrequent or high-stakes tasks.
