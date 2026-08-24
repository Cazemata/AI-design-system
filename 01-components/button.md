# Button

## Overview
The primary control for triggering an action (submit, confirm, navigate, delete). Use Button for tappable actions with a text label; use a dedicated Icon Button (once documented) for icon-only controls, and Chip (once documented) for filters or multi-select toggles.

## Anatomy
1. Container
2. Label
3. Leading icon (optional)
4. Trailing icon (optional)

## Variants
- **Primary** — filled with `color-action-primary`; the single highest-emphasis action in a given screen or section.
- **Secondary** — outlined with `color-border-default`, transparent background, label in `color-action-primary`; for an alternative action alongside a Primary button.
- **Text** — no container or border, label only in `color-action-primary`; for low-emphasis actions (e.g. "Cancel" in a dialog).
- **Destructive** — filled with `color-critical`; for irreversible or destructive actions (delete, remove account). Pair with a confirmation step.

## States
| State | Visual change |
|---|---|
| Default | Variant's resting fill/border/label color |
| Pressed | Background shifts to `color-action-primary-pressed` (Primary); see Platform behavior for ripple/elevation vs. dim treatment |
| Focused | `spacing-4`-equivalent outline in `color-border-focus` around the container |
| Disabled | Background/border in `color-action-disabled`, label in `color-text-disabled`; no elevation |
| Loading | Label replaced by a spinner at `icon-size-md`; container size unchanged; non-interactive |

## Sizing & spacing
- Minimum height: `touch-target-min-android` (48dp), the default per `CLAUDE.md`. Only branch to `touch-target-min-ios` (44pt) if a build explicitly targets native iOS sizing.
- Horizontal padding: `spacing-16` on each side of the label.
- Icon-to-label gap: `spacing-8`.
- Label: `type-label`.
- Minimum width: none fixed — width fits label plus padding, no smaller than the touch target height.

## Platform behavior
Android is the default spec (see [`CLAUDE.md`](../CLAUDE.md)). iOS is documented only where it meaningfully diverges.

- **Android (default)**: Pressed state shows a Material ripple radiating from the touch point; elevation rises from `elevation-1` to `elevation-2` for the duration of the press, then returns to `elevation-1` on release, using `motion-duration-fast` and `motion-ease-standard` for the elevation transition (see [`elevation-shadow.md`](../00-foundations/elevation-shadow.md), [`motion.md`](../00-foundations/motion.md)).
- **iOS (if different)**: No ripple and no elevation change on press — Buttons on iOS don't use Material-style elevation. Pressed state is communicated with a brief opacity/tint dim of the container instead.

## Accessibility
- Accessible name: the visible label is always exposed to the accessibility tree; an icon-only Button must still carry an explicit accessible name describing the action, not the icon.
- Minimum touch target: `touch-target-min-android` (see [`spacing.md`](../00-foundations/spacing.md)) — pad the tappable area with invisible hit-area padding if the visual button is smaller.
- Contrast: label-to-background must meet the 4.5:1 minimum in [`color.md`](../00-foundations/color.md), checked for both light and dark values of the variant's tokens.
- Screen reader behavior: Disabled buttons are announced as disabled per platform convention and excluded from the default activation gesture. Loading buttons announce a busy/loading state and reject repeated activation until loading completes.

## Do / Don't
- **Do** use exactly one Primary button per screen or section.
- **Do** pair Destructive buttons with a confirmation step before the action completes.
- **Don't** place two Primary buttons in the same view — demote one to Secondary or Text.
- **Don't** shrink the tappable area below `touch-target-min-android` to fit a dense layout; add invisible padding instead.

## Related components
No other component files exist yet — Button is the first documented. Once added, cross-link here: Icon Button (icon-only equivalent of this component) and Chip (selection/filter control, not to be confused with Button).
