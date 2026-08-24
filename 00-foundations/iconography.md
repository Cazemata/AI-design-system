# Iconography

## Purpose
Defines the icon grid, sizing, and usage rules so icons stay visually consistent across the app.

## Icon grid
- Base grid: **24x24px**, drawn on a 20x20px live area with 2px padding on each side (matches Material and iOS conventions closely enough to share a single icon set).
- Stroke weight: **1.5px** at 24px size, scaling proportionally at other sizes.
- Style: outlined by default; filled variants only for active/selected states (e.g. a filled star vs outline star for favorite toggle).

## Sizing tokens
| Token | Value | Usage |
|---|---|---|
| icon-size-sm | 16px | Inline with `type-body-sm`/`type-caption` text, dense lists |
| icon-size-md | 20px | Inline with `type-body-md` text, default UI icons |
| icon-size-lg | 24px | Standalone icons, tab bar, nav bar |
| icon-size-xl | 32px | Empty states, feature highlights |

Icon size should always be chosen relative to the adjacent text token (see [`typography.md`](./typography.md)) rather than picked independently.

## Color
Icons use the same semantic color tokens as text — see [`color.md`](./color.md). Default to `color-text-primary` or `color-text-secondary`; use `color-action-primary` only for icons that are themselves interactive (e.g. an icon button).

## Usage guidelines
- **Pair icons with labels** wherever the meaning isn't universally understood (e.g. a trash icon for delete is fine alone; a custom/ambiguous icon needs a text label).
- Don't use icons as the sole means of conveying critical information — always have a text equivalent available (tooltip, label, or accessible name).
- Keep icon meaning consistent across the app — one icon should not represent two different actions in different screens.

## Touch targets
Interactive icons (icon buttons) must meet the same touch target minimums as any control — see [`spacing.md`](./spacing.md) (48dp/44pt minimum), even when the visual icon is smaller (e.g. a 20px icon inside a 48dp tappable area).

## Accessibility
- Every interactive icon needs an accessible label (VoiceOver/TalkBack) describing its action, not its appearance (e.g. "Delete", not "Trash can icon").
- Decorative icons (no interactive or unique-information role) should be marked as hidden from screen readers to avoid noise.

## Do / Don't
- **Do** size icons relative to the text they sit beside.
- **Do** give every icon button a proper accessible label.
- **Don't** introduce a new icon style (filled vs outline) without checking existing usage first.

## Related
- [`color.md`](./color.md) — icon color tokens
- [`typography.md`](./typography.md) — pairing icon size with text size
- [`spacing.md`](./spacing.md) — touch target minimums for icon buttons