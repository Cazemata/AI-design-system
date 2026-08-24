# Top Navigation

## Overview
The fixed header visible throughout the original GigaCheck screens: a status bar followed by
a colored header bar carrying the screen title and a close icon. Documented as-is from the
existing screens, adapted here to sit above the conversational thread instead of above a
static form — `progress-indicator` is pinned directly beneath it. Don't confuse with
`progress-indicator`: this component is identity/exit chrome (where am I, how do I leave);
`progress-indicator` is flow-position chrome (how far along am I).

## Anatomy
1. **Status bar** — OS-owned, safe-area inset; not drawn by this component.
2. **Header bar** — colored container beneath the status bar.
3. **Title** — the current screen/flow name.
4. **Close icon** — exits the flow.

## Variants
- **Standard (only confirmed treatment)** — the single visual treatment seen throughout the
  original screens; no alternate header styles have been confirmed, so none are documented
  here.

## States
| State | Visual change | Description |
|---|---|---|
| Default | Static header, no interaction | Persistent, always visible above the conversation thread |
| Close icon pressed | Ripple (Android) / opacity dim (iOS) on the icon only | Triggers exit from the flow — see Do/Don't on confirming before discarding progress |

## Sizing & spacing
- Header bar background: `color-surface-brand` (see [`color.md`](../00-foundations/color.md))
  — distinct from `color-critical` despite sharing the same underlying `red-500` primitive
  today; see that token's provenance note if the header's actual brand red is ever confirmed
  to differ from the error red.
- Header bar height: `header-height-default` (56dp, see
  [`spacing.md`](../00-foundations/spacing.md)).
- Close icon: `icon-size-lg` (24px, per `iconography.md`'s "standalone icons, tab bar, nav
  bar" usage), tappable area `touch-target-min-android` minimum.
- Horizontal padding around title/icon: `spacing-16`.
- Title text: `type-heading-sm`.
- Shadow beneath the header bar: `elevation-1` is the closest existing token (its usage
  column doesn't explicitly list app bars, but the shadow weight — y:1px, blur:2px, 8%
  opacity — is the right order of magnitude); used here as a reasonable extension of an
  existing token, not a new one.

## Platform behavior
Android is the default spec (see [`CLAUDE.md`](../CLAUDE.md)). iOS is documented only where
it meaningfully diverges.

- **Android (default)**: status bar + Material app bar, using `WindowInsets` for the system
  status bar per `grid-layout.md`.
- **iOS (if different)**: status bar + nav bar using safe-area layout guides; a close "X"
  rather than a back chevron, since this flow is entered as a task, not pushed onto a
  navigation stack.

## Accessibility
- Title is exposed as the screen's accessible heading/name.
- Close icon needs an explicit accessible label ("Close" or "Exit check," not "X icon").
- Minimum touch target for the close icon: `touch-target-min-android` (see
  [`spacing.md`](../00-foundations/spacing.md)).
- Status bar content (time, battery, etc.) is OS-owned and outside this component's
  accessibility surface.

## Do / Don't
- **Do** use the OS safe-area API for the status bar inset, never a fixed offset (see
  [`grid-layout.md`](../00-foundations/grid-layout.md)).
- **Do** confirm before discarding in-progress work if the close icon is tapped mid-flow —
  don't exit silently.
- **Don't** hardcode the header bar's height or background color — reference
  `header-height-default` and `color-surface-brand` instead.

## Related components
`progress-indicator` (pinned directly beneath this component)
