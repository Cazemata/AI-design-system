# Checkbox / Radio

## Overview
The base selection control: a single component with two variants — Checkbox (multi-select)
and Radio (single-select) — matching the simple square/circle style used throughout the
original GigaCheck screens. This is the control `option-card` builds on and delegates its
selection indicator to; use Checkbox/Radio directly only in dense, non-conversational
contexts (e.g. a settings list), and use `option-card` for anything presented as a response
to an agent turn. Don't confuse with Button: a checkbox/radio holds a persisted selection
state, a button triggers a one-off action.

## Anatomy
1. **Control** — square (Checkbox) or circle (Radio) outline.
2. **Selected indicator** — checkmark (Checkbox) or filled dot (Radio), rendered inside the
   control when selected.
3. **Label** — the option text.
4. **Helper text** (optional) — smaller supporting text beneath the label.

## Variants
- **Checkbox (multi-select)** — square control; any number of options in a group can be
  selected independently.
- **Radio (single-select)** — circular control; selecting one option in a group deselects
  any other.

## States
| State | Visual change | Description |
|---|---|---|
| Default | Unfilled control, `color-border-default` outline | Unselected, awaiting input |
| Selected | Control fills with `color-action-primary`; checkmark/dot renders in `color-text-inverse` | Checked (Checkbox) or chosen (Radio) |
| Disabled | Control outline/fill in `color-action-disabled`, label in `color-text-disabled` | Not interactive; option is contextually unavailable |
| Error | Control outline in `color-border-critical` | Shown when this control is used standalone (outside `option-card`, which surfaces its own group-level error via an agent Validation follow-up message instead of a local border) |

## Sizing & spacing
- Control size: `control-size-md` (20px, see [`spacing.md`](../00-foundations/spacing.md)) —
  a dedicated token, independent of icon sizing.
- Tappable area: the control plus label together must meet `touch-target-min-android` (48dp)
  even though the visible control is smaller — use invisible hit-area padding (see
  [`spacing.md`](../00-foundations/spacing.md)).
- Control-to-label gap: `spacing-8`.
- Corner radius (Checkbox only): `radius-sm` (see [`spacing.md`](../00-foundations/spacing.md)).
- Label: `type-body-md`. Helper text: `type-body-sm`.

## Platform behavior
Android is the default spec (see [`CLAUDE.md`](../CLAUDE.md)). iOS is documented only where
it meaningfully diverges.

- **Android (default)**: Material checkbox/radio, with a ripple on tap using
  `motion-duration-fast`.
- **iOS (if different)**: no ripple; selection is communicated by the fill/checkmark
  animating in directly, since iOS has no native ripple convention.

## Accessibility
- Checkbox exposes checkbox semantics (checked/unchecked/mixed if partial-select is ever
  needed); Radio exposes radio-group semantics with only one member selected at a time —
  don't reuse one role for the other.
- Minimum touch target: `touch-target-min-android` (see [`spacing.md`](../00-foundations/spacing.md)).
- Contrast: control outline and fill against background must meet the requirements in
  [`color.md`](../00-foundations/color.md).
- Screen reader behavior: state changes (selected/deselected) announce immediately; Disabled
  controls are announced as disabled and excluded from the focus order.

## Do / Don't
- **Do** use Radio only when exactly one answer is valid; use Checkbox whenever more than one
  can apply.
- **Do** let `option-card` delegate to this component for its selection indicator rather than
  drawing its own checkmark/dot.
- **Don't** show the Error state's local border when this control is used inside
  `option-card` — that error surfaces via the agent Validation follow-up message instead (see
  `option-card`'s States table).

## Related components
`option-card`
