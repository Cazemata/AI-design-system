# Elevation & Shadow

## Purpose
Defines how surfaces stack visually (cards over background, modals over cards, etc.) so depth and hierarchy stay consistent.

## Elevation levels
| Token | Level | Shadow | Usage |
|---|---|---|---|
| elevation-0 | 0 | none | Base screen background |
| elevation-1 | 1 | y:1px, blur:2px, 8% opacity | Resting cards, list items |
| elevation-2 | 2 | y:2px, blur:4px, 10% opacity | Raised cards (e.g. on press/drag), dropdown menus |
| elevation-3 | 3 | y:4px, blur:8px, 12% opacity | Sheets, popovers |
| elevation-4 | 4 | y:8px, blur:16px, 16% opacity | Modals, dialogs |
| elevation-5 | 5 | y:12px, blur:24px, 20% opacity | Toasts/snackbars (float above everything, including modals) |

Shadow color should always be a neutral dark (derived from `gray-900` at low opacity — see [`color.md`](./color.md)), never a brand color, so elevation reads consistently regardless of surface color.

## Dark mode
In dark mode, shadows are less visually effective against dark backgrounds. Prefer signaling elevation through subtle background color shifts (lighter surface = higher elevation) in addition to or instead of shadow, using the `color-surface-*` tokens.

## Usage guidelines
- Only one elevation level should visually "win" at a time — don't stack multiple elevated surfaces without a clear z-order.
- Elevation should reflect actual interaction hierarchy: a modal is always higher than the sheet or card that triggered it.
- Pressed/dragged states typically move an element up one elevation level temporarily (e.g. `elevation-1` → `elevation-2` while dragging a card), then return on release.

## Platform behavior
- **iOS**: elevation is usually communicated more through blur/translucency (e.g. sheets with a blurred background) than heavy shadow — keep shadow subtle.
- **Android**: Material conventions use elevation more explicitly with visible shadow — slightly stronger shadow values are acceptable here if branching per-platform.

## Accessibility
- Never use elevation/shadow as the only indicator of interactivity — pair with clear affordances (borders, icons, or labels).
- Ensure elevated surfaces still meet text contrast requirements against their (possibly shifted) background color in dark mode.

## Do / Don't
- **Do** increase elevation by exactly one level for pressed/active states, not arbitrary amounts.
- **Do** use background color shifts as a dark-mode-friendly elevation signal.
- **Don't** apply shadow using anything other than the tokens above.

## Related
- [`color.md`](./color.md) — surface color tokens used alongside elevation in dark mode
- [`motion.md`](./motion.md) — elevation changes are often animated (e.g. card press)