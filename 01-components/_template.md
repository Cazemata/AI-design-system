# [Component Name]

## Overview
One or two sentences: what this component is and when to use it. If there's a common component it's easily confused with, name it here and clarify the distinction (e.g. "Use Button for primary actions; use Chip for filters or selections").

## Anatomy
List the labeled parts that make up the component, in visual order (e.g. container → leading icon → label → trailing icon). Add a simple diagram or numbered image reference here if available.

1. Container
2. [Part 2]
3. [Part 3]

## Variants
The distinct visual/functional versions of this component.

- **[Variant name]** — when to use it
- **[Variant name]** — when to use it

## States
Every interactive state this component supports, and what changes visually in each. The rows below are illustrative, not fixed — add, remove, or rename rows to match this component's actual interaction model (e.g. a text input has no "Pressed" state but does have "Filled" and "Read-only"; a static display component may have none of these).

| State | Visual change |
|---|---|
| Default | — |
| Pressed (if applicable) | — |
| Focused | — |
| Filled / populated (if applicable) | — |
| Read-only (if applicable) | — |
| Disabled | — |
| Loading (if applicable) | — |
| Error (if applicable) | — |

## Sizing & spacing
- Touch target: reference `touch-target-min-android` / `touch-target-min-ios` from [`spacing.md`](../00-foundations/spacing.md) (Android baseline is the default per `CLAUDE.md`).
- Internal padding: reference relevant `spacing-*` tokens.
- Minimum/maximum width or height, if constrained.

## Platform behavior
Android is the default spec (see `CLAUDE.md`). Only document iOS here where it meaningfully diverges — don't restate identical behavior twice.

- **Android (default)**: [behavior, Material convention referenced if applicable]
- **iOS (if different)**: [only fill in if it actually deviates]

## Accessibility
- Accessible name / label requirements
- Minimum touch target (see [`spacing.md`](../00-foundations/spacing.md))
- Contrast requirements (see [`color.md`](../00-foundations/color.md))
- Screen reader behavior for each state (e.g. how "disabled" or "loading" is announced)

## Do / Don't
- **Do** [concrete example]
- **Do** [concrete example]
- **Don't** [concrete example]
- **Don't** [concrete example]

## Related components
- [`[component].md`](./[component].md) — how it relates