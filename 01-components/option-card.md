# Option Card

## Overview
The technician's response to an agent question, when the answer is a choice from a known
set. Direct replacement for the checkbox lists and radio groups used throughout GigaCheck
(e.g. "Checked and values checked" / "Exchanged", "TV Only / Internet Only / Internet and
TV", "Morning / Afternoon"). Rendered as a horizontal or vertical stack of tappable cards
directly beneath the triggering agent message, standing in for the chat-composer on turns
where free text isn't the expected input.

## Anatomy
1. **Card container** — rounded rectangle, full available width (vertical stack) or
   fixed/flexible width (horizontal chip row for short 2–3 option sets like Morning/Afternoon).
2. **Leading icon** (optional) — used when the original screen paired a checkbox with an
   icon-bearing helper (e.g. the OptimiseInternet upsell items — **no source in the current
   flow**, that screen is removed).
3. **Label** — the option text itself (e.g. "Internet is working").
4. **Helper text** (optional) — smaller text beneath the label, for upsell/offer copy that
   had its own explanatory line in the original screens — **no source in the current flow**,
   since the upsell/offer screens are removed.
5. **Selection indicator** — delegated to `checkbox-radio`: checkmark (multi-select) or
   filled dot (single-select), trailing or leading depending on platform convention, rather
   than introducing new iconography here.

## Variants
- **Single-select** — replaces radio-button questions (e.g. "Booked Products": TV Only /
  Internet Only / Internet and TV). Selecting one option auto-advances the conversation;
  no separate "Next" tap needed since there's nothing else to confirm on that turn.
- **Multi-select** — replaces checkbox-group questions (e.g. "Checked and values checked" /
  "Exchanged", which can both apply). Requires an explicit confirm action (see
  `chat-composer`'s inline "Confirm selection" affordance) since multiple taps are expected
  before the turn is complete.
- **Upsell offer card** — a richer variant combining leading icon, label, and helper/definition
  text, used for OptimiseInternet/OptimiseTV screens. Optionally expandable inline (replacing
  the `.definitionToggle` component) rather than needing a separate detail screen.
  - **Flag — no source in the current flow (confirmed 2026-10).** The OptimiseInternet and
    OptimiseTV screens this variant was built for have been **removed from the GigaCheck
    flow**, and no upsell content remains in it (see `conversational-flow.md`'s "Removed from
    the flow"). The variant is **retained, not deleted** — flagging that it currently has no
    confirmed consumer, which is a decision for the component-set owner, not something
    resolved here.

## States
| State | Visual change | Description |
|---|---|---|
| Default | Unselected container, no fill | Awaiting input |
| Selected | Selection indicator filled; single-select shows only the chosen card as filled, others dim slightly | Reduces visual noise around the chosen option |
| Disabled | `color-action-disabled` fill/border, `color-text-disabled` label | Used when an option is contextually unavailable (the "upsell already active on the account" example has **no source in the current flow**) — shown, not hidden, with a short reason |
| Error | No border change on the cards themselves — instead of a `color-border-critical` border on the cards, the error surfaces via an inline agent Validation follow-up message | Multi-select group shows this state collectively when confirmed with zero selections on a mandatory question — replaces the red-bordered box + "Select at least one field!" pattern |

## Sizing & spacing
- Card min touch target: `touch-target-min-android` (48dp), consistent with base system rule.
- Card padding: `spacing-16`.
- Gap between stacked cards: `spacing-8`.
- Gap between horizontal chip-style cards: `spacing-8`, wrapping to a new row rather than
  horizontal scroll if the set exceeds available width.

## Platform behavior
Android is the default spec (see [`CLAUDE.md`](../CLAUDE.md)). iOS is documented only where it
meaningfully diverges.

- **Android (default)**: Material ripple on tap.
- **iOS (if different)**: No deviation currently scoped; revisit if/when this pattern ships
  cross-platform.

## Accessibility
- Each card is a single focusable element (not a nested checkbox-inside-a-button); label and
  helper text are both included in the accessible name.
- Single-select groups use radio-group semantics; multi-select groups use checkbox-group
  semantics — don't reuse one role for both.
- Minimum touch target and color-contrast rules inherited from `spacing.md` and `color.md`
  apply without exception, since this is a mandatory-input control in a field-work context
  (technician may be using this outdoors, one-handed, on a ladder).

## Do / Don't
- **Do** auto-advance on single-select — don't make the technician tap twice for a choice
  that only ever has one valid answer.
- **Do** keep multi-select explicit-confirm, so partial taps don't silently submit.
- **Don't** collapse more than ~4-5 options into a card stack without reconsidering whether
  the question itself should be broken into two conversational turns instead.

## Related components
`agent-message`, `chat-composer`, `checkbox-radio` (this component's selection indicator is
delegated to it), `definition-toggle` (rendered inline by the Upsell offer card variant —
**no source in the current flow**; link retained)
