# Spacing

## Purpose
Defines the spacing scale and touch target minimums used across the app. Consistent spacing tokens keep layouts rhythmically aligned and make components easy to compose predictably.

## Spacing scale
Base unit: **8px** (with a 4px half-step for tight/inline cases).

| Token | Value | Usage |
|---|---|---|
| spacing-4 | 4px | Icon-to-label gaps, tight inline spacing |
| spacing-8 | 8px | Default gap between related elements |
| spacing-12 | 12px | Compact padding (chips, small cards) |
| spacing-16 | 16px | Default screen margin, standard card padding |
| spacing-24 | 24px | Gap between distinct sections |
| spacing-32 | 32px | Large section breaks |
| spacing-48 | 48px | Top-level screen padding, empty state spacing |

## Touch targets
| Token | Value | Usage |
|---|---|---|
| touch-target-min-ios | 44pt | Minimum tappable area, iOS (Apple HIG) |
| touch-target-min-android | 48dp | Minimum tappable area, Android (Material) |

Always design to the larger of the two platform minimums (48dp/48pt-equivalent) when building a single cross-platform spec, unless the component file explicitly branches iOS vs Android sizing.

## Corner radius
**Note on provenance:** no radius measurement had ever been captured from the source Figma
file when this scale was added — the values below are a considered first-pass scale (same
base-4 logic as the spacing scale above), not Figma-verified. Confirm against the real file
and adjust if they're off; this was added specifically to stop individual component files
(`agent-message.md`, `checkbox-radio.md`) from each improvising their own fallback.

| Token | Value | Usage |
|---|---|---|
| radius-sm | 4px | Small controls (checkbox, chips) |
| radius-md | 8px | Default cards and containers (`option-card`, `agent-message` bubble) |
| radius-lg | 12px | Larger surfaces (sheets, modals) |
| radius-full | 9999px | Fully rounded (radio control, pills, avatars) |

## Component sizing
| Token | Value | Usage |
|---|---|---|
| control-size-md | 20px | Checkbox and radio control dimensions — deliberately separate from `icon-size-md` (same value today, but independently adjustable; a control shouldn't resize just because icon sizing changes) |
| header-height-default | 56dp | App bar / persistent header height. Set to match Android Material's standard app bar height (this project's default platform per `CLAUDE.md`) rather than a captured Figma measurement — no header height had been recorded from the source file either. |

## Layout margins
| Token | Value | Usage |
|---|---|---|
| margin-screen-default | 16px | Default left/right screen margin |
| margin-screen-compact | 12px | Dense layouts (e.g. settings lists) |

## Usage guidelines
- Space between unrelated elements should always be greater than space between related elements (e.g. a label and its input use `spacing-4`–`spacing-8`; two separate form fields use `spacing-16`+).
- Don't use raw pixel/dp values in component files — reference the token.
- If a component needs a spacing value not on this scale, that's a signal to either round to the nearest token or propose a new one here — not to introduce a one-off value locally.

## Accessibility
- All interactive elements must meet the touch target minimums above, even if their visible size is smaller (use invisible hit-area padding if needed).
- Maintain at least `spacing-8` between adjacent tappable elements to avoid mis-taps.

## Do / Don't
- **Do** reference `spacing-*` tokens for all padding/margin/gap values.
- **Do** pad tappable elements to meet touch target minimums even if the visual design is smaller.
- **Don't** place two tappable elements closer than `spacing-8` apart.

## Related
- [`grid-layout.md`](./grid-layout.md) — screen-level layout and safe areas
- [`typography.md`](./typography.md) — spacing around text blocks