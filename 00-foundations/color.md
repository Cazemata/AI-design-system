# Color

## Purpose
Defines the color palette and semantic tokens used across the app. Components should always reference semantic tokens (e.g. `color-action-primary`), never raw hex values or primitive tokens directly — this keeps theming (including dark mode) centralized here.

## Primitives
Raw color values. Not used directly in components — only as the source for semantic tokens below.

| Token | Light value | Dark value |
|---|---|---|
| blue-100 | #E6F0FF | #0A1F3D |
| blue-500 | #0052CC | #4C9AFF |
| blue-700 | #003D99 | #6FB0FF |
| gray-50 | #FAFBFC | #1B1F24 |
| gray-100 | #F4F5F7 | #22262C |
| gray-300 | #DFE1E6 | #3A3F47 |
| gray-500 | #6B778C | #8C97A8 |
| gray-700 | #253858 | #C1C7D0 |
| gray-900 | #091E42 | #F4F5F7 |
| red-500 | #DE350B | #FF6B4A |
| green-500 | #00875A | #4BCE97 |
| yellow-500 | #FFAB00 | #FFC53D |

## Semantic tokens

### Text
| Token | Maps to | Usage |
|---|---|---|
| color-text-primary | gray-900 | Default body/heading text |
| color-text-secondary | gray-500 | Supporting/secondary text |
| color-text-disabled | gray-300 | Disabled labels |
| color-text-inverse | gray-50 | Text on dark/filled surfaces |
| color-text-link | blue-500 | Links, tappable text |

### Background & surface
| Token | Maps to | Usage |
|---|---|---|
| color-background-default | gray-50 | App/screen background |
| color-surface-default | gray-100 | Cards, sheets, elevated surfaces |
| color-surface-sunken | gray-300 | Inset areas, dividing regions |

### Brand
| Token | Maps to | Usage |
|---|---|---|
| color-surface-brand | red-500 | Persistent brand-colored surfaces (e.g. `top-navigation`'s header bar) — **not** an error state, despite sharing a primitive with `color-critical` |

**Note on provenance:** the original screens use a persistent brand-red header, but no hex
value for it was ever captured from the source Figma file — this reuses the `red-500`
primitive as a placeholder since it's the only red currently defined, not because the header
and the error color are confirmed to be the same red. If the header's actual brand red turns
out to differ from `red-500` once confirmed, add a distinct primitive and repoint this token
— don't leave a component reusing `color-critical` for a non-error, always-on surface in the
meantime, which is what prompted adding this token.

### Action
| Token | Maps to | Usage |
|---|---|---|
| color-action-primary | blue-500 | Primary buttons, active states |
| color-action-primary-pressed | blue-700 | Primary button pressed state |
| color-action-disabled | gray-300 | Disabled buttons/controls |

### Feedback
| Token | Maps to | Usage |
|---|---|---|
| color-critical | red-500 | Errors, destructive actions |
| color-success | green-500 | Success states, confirmations |
| color-warning | yellow-500 | Warnings, caution states |

### Border
| Token | Maps to | Usage |
|---|---|---|
| color-border-default | gray-300 | Default dividers, input borders |
| color-border-focus | blue-500 | Focused input/control outline |
| color-border-critical | red-500 | Error/invalid state borders (e.g. input fields) |

## Dark mode
Every semantic token has a light and dark value (see primitives table). Components should never hardcode a mode — always resolve through the semantic token so the system switches automatically with the OS setting.

## Accessibility
- Text on background must meet **4.5:1** contrast minimum (WCAG AA) for body text, **3:1** for large text (18pt+/14pt+ bold).
- Do not convey meaning (error, success, etc.) through color alone — always pair with an icon or text label.
- Verify contrast for both light and dark values when adding a new token.

## Do / Don't
- **Do** reference semantic tokens in component files (`color-action-primary`).
- **Don't** reference primitives directly in component or pattern files.
- **Don't** introduce a new primitive without checking if an existing one already fits.

## Related
- [`typography.md`](./typography.md) — text tokens often pair with color tokens
- [`elevation-shadow.md`](./elevation-shadow.md) — surface tokens relate to elevation levels