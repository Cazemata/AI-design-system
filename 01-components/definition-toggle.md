# Definition Toggle

## Overview
A small inline component for supplementary copy, based on the `.definitionToggle` pattern
found in the original OptimiseInternet screens. **Note on source ambiguity**: the confirmed
schema (`gigacheck-flow-schema.md`) describes `.definitionToggle`'s one confirmed real-world
use — swapping between "Customer has received" / "has NOT received a FREE WiFi router" — as
a *conditional, account-driven* copy state, not something the user taps. `option-card.md`'s
Upsell offer card variant, written before that schema detail was confirmed, instead describes
`.definitionToggle` as something *user-toggled* ("optionally expandable inline"). Rather than
silently pick one, this component documents both as separate variants — **only the
Conditional variant is actually confirmed in the source flow**; the Expandable variant
matches `option-card.md`'s existing description but hasn't itself been verified against a
real screen. Confirm which is intended for OptimiseInternet before implementation.

## Anatomy
1. **Label/copy** — the currently visible text.
2. **Toggle indicator** (Expandable variant only) — a chevron or icon showing more content is
   available.
3. **Revealed content** — additional copy (Expandable) or the alternate branch of the
   conditional copy (Conditional).

## Variants
- **Conditional (confirmed)** — displays one of two pre-set copy strings based on
  account/context state, not user interaction (e.g. "Customer has received" / "has NOT
  received a FREE WiFi router"). No toggle indicator; the technician doesn't interact with it.
- **Expandable (unconfirmed — matches `option-card.md`'s existing description)** — the
  technician taps a toggle indicator to reveal additional supplementary copy inline, then taps
  again to collapse it.

## States
| State | Visual change | Description |
|---|---|---|
| Conditional A / Conditional B (Conditional variant only) | Displays one of two pre-set strings, no toggle indicator shown | Which string displays is driven by account/context state, not user interaction |
| Collapsed (Expandable variant only) | Single-line copy, indicator points toward "more" | Default state before the technician taps to expand |
| Expanded (Expandable variant only) | Additional copy revealed inline, indicator flips direction | Technician has tapped to reveal the fuller definition |

## Sizing & spacing
- Toggle indicator (Expandable only): visually `icon-size-sm` (16px, per `iconography.md`'s
  "inline with `type-body-sm`/`type-caption` text" usage), tappable area
  `touch-target-min-android` minimum via invisible hit-area padding.
- Label-to-indicator gap: `spacing-4`.
- Gap between collapsed line and revealed content: `spacing-8`.
- Copy text: `type-body-sm`, in `color-text-secondary` (matches the helper-text treatment
  used elsewhere for supplementary, non-primary copy, e.g. `agent-message`'s helper text).

## Platform behavior
Android is the default spec (see [`CLAUDE.md`](../CLAUDE.md)). iOS is documented only where
it meaningfully diverges.

- **Android (default)** (Expandable variant): the indicator rotates in place on tap; revealed
  content animates in using `motion-duration-fast` / `motion-ease-decelerate` (content
  entering).
- **iOS (if different)**: same visual reveal, no ripple on the tap itself — feedback is the
  indicator rotation and content reveal only.
- The Conditional variant has no interaction, so no platform divergence applies to it.

## Accessibility
- Expandable variant: the toggle must expose its expanded/collapsed state to assistive tech
  (not just a visual chevron flip), and needs an accessible name describing the action (e.g.
  "Show more about Super-WLAN," not just "chevron" or "toggle").
- Conditional variant: whichever string is currently shown must be fully exposed to screen
  readers as static text — there's no toggle state to expose since there's no interaction.
- Minimum touch target for the Expandable toggle: `touch-target-min-android` (see
  [`spacing.md`](../00-foundations/spacing.md)).

## Do / Don't
- **Do** confirm which variant (Conditional or Expandable) is actually intended for each use
  before building — don't assume Expandable just because it reads more flexibly.
- **Do** reserve this component for genuinely optional or supplementary copy.
- **Don't** use the Expandable variant to hide copy the technician needs to complete a
  mandatory field — that copy belongs in visible helper text instead (see `agent-message`).
- **Don't** nest a Definition Toggle inside another one.

## Related components
`option-card` (Upsell offer card variant renders this inline)
