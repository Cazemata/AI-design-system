# Typography

## Purpose
Defines the type scale and text styles used across the app. Each token bundles font, weight, size, line-height, and letter-spacing so components reference one token instead of four separate values.

## Type scale

| Token | Size (pt/sp) | Line height | Weight | Usage |
|---|---|---|---|---|
| type-display | 34 | 41 | Bold (700) | Hero/marketing screens only |
| type-heading-lg | 28 | 34 | Bold (700) | Screen titles |
| type-heading-md | 22 | 28 | Semibold (600) | Section headers |
| type-heading-sm | 18 | 24 | Semibold (600) | Card/list group headers |
| type-body-lg | 17 | 24 | Regular (400) | Primary reading text |
| type-body-md | 15 | 21 | Regular (400) | Default UI text, labels |
| type-body-sm | 13 | 18 | Regular (400) | Secondary/support text |
| type-caption | 12 | 16 | Regular (400) | Timestamps, metadata, legal text |
| type-label | 13 | 16 | Semibold (600) | Buttons, tabs, form labels |

Font family: [set project typeface here — system default is SF Pro (iOS) / Roboto (Android) unless a custom typeface is licensed].

## Minimum sizes
Do not go below **13pt/sp** for any text a user needs to read to complete a task. `type-caption` (12pt) is reserved for genuinely secondary metadata, never for actionable content.

## Platform-specific scaling
- **iOS**: supports Dynamic Type. Map each token to the nearest system text style (e.g. `type-body-md` → `.body`) so text scales with the user's OS-level accessibility setting.
- **Android**: supports font scaling via system settings. Use `sp` units (not `dp`) for all type tokens so they respond to the user's font size preference.
- Test every screen at the largest supported accessibility text size — layouts should reflow, not truncate or overlap, at 2x scale.

## Usage guidelines
- One `heading` token per screen for the primary title; avoid stacking multiple heading levels on a single screen.
- `type-label` is for short, fixed-width UI text (buttons, tabs) — not for paragraphs.
- Don't create one-off font sizes outside this scale. If nothing fits, propose a new token here first.

## Accessibility
- Maintain **4.5:1** contrast against background for body/label text (see [`color.md`](./color.md)).
- Never rely on weight or size alone to convey required/error states — pair with color and/or an icon.
- Support OS text scaling as described above; do not disable Dynamic Type / font scaling for any body or label text.

## Do / Don't
- **Do** use `type-body-md` as the default for most UI text.
- **Do** reference tokens by name in component files rather than raw point sizes.
- **Don't** hardcode a font size in a component file.

## Related
- [`color.md`](./color.md) — text color tokens
- [`spacing.md`](./spacing.md) — spacing around text blocks