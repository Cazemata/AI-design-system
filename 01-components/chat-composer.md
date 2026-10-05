# Chat Composer

## Overview
The persistent input area anchored to the bottom of the conversational flow. Handles three
distinct jobs that were previously three separate things in GigaCheck (a numeric text field,
a mandatory-consent checkbox pair, and a fixed "Next" button): free-text/numeric entry,
confirming a multi-select `option-card` turn, and advancing past a Statement-only agent
message. The composer's content changes based on what the current agent turn expects —
it is not always a text field.

## Anatomy
1. **Input row** — appears only when the current turn expects free text or a number (e.g.
   "Booked Bandwidth (Mbit/s)"). Standard text field, numeric keyboard variant when
   appropriate.
2. **Confirm button** — appears when the current turn is a multi-select `option-card` group;
   replaces the original "Next" button for that specific case. Disabled until the minimum
   required selections are made.
3. **Continue affordance** — a lightweight "Continue" chip or tap-anywhere-to-continue pattern
   for Statement-only agent turns that need no input (section transitions).
4. **Signature-capture control** (optional, contextual) — signature icon, shown only on the
   turn that expects a signature (the Customer signature step), opening `signature-capture`
   rather than typing.
5. **Send/submit control** — final-turn variant, replacing the "Send report" button; only
   ever appears on the terminal turn, after signature capture is complete or a decline has
   been recorded.

## Variants
- **Text/numeric entry** — single-line by default; validates inline (mirrors the original
  "Mandatory field hasn't been filled!" states) but surfaces the correction as an
  `agent-message` Validation follow-up rather than red field-level text alone.
- **Confirm selection** — paired with multi-select `option-card`; label reads "Confirm" or
  similar, not a generic "Next," so it's clear what action is being taken.
- **Continue** — minimal, low-emphasis; used sparingly since most turns should expect genuine
  input given this is a verification checklist, not a passive briefing.
- **Capture trigger** — opens `signature-capture` as a modal/full-screen surface and returns
  the result inline as a confirmation card in the conversation thread, rather than navigating
  to a separate screen and back.
- **Submit (terminal)** — the "Send report" equivalent; only enabled once `signature-capture`
  reports a completed signature **or an explicitly recorded decline to sign** (confirmed via
  2026-10 stakeholder workshop, not a new Figma pass — see `signature-capture.md`'s Declined
  state). This directly encodes the flow rule confirmed on the Customer Signature screen: the
  report cannot be generated without one of those two outcomes recorded first, so this
  control should be disabled — not just validated on tap — until that condition is met.

## States
| State | Visual change | Description |
|---|---|---|
| Default | Composer shows the control matching the current turn (input row / confirm button / continue chip) | Ready for input matching the current turn's expected type |
| Disabled | Confirm/Submit rendered in `color-action-disabled` background, `color-text-disabled` label | Disabled until minimum requirement met (mirrors "mandatory" field logic throughout the original flow) |
| Loading | Submit control shows a brief loading indicator in place of its label | Shows while the report sends — replaces the standalone Send/Success and Send/Error screens with an inline result message instead of a full-screen transition, where feasible |
| Error | Inline `color-critical` system note appears above the composer | Submit failed — surfaces as an agent-message-style system note ("Sending the report failed — want to try again?") rather than a dead-end screen, since the technician needs a retry path without losing their place |

## Sizing & spacing
- Fixed to bottom of viewport, safe-area aware (per `grid-layout.md` safe-area rule — no
  fixed offsets, always via OS APIs).
- Height: `touch-target-min-android` minimum, expands for multi-line text entry up to a
  reasonable cap (~3 lines) before scrolling internally.
- Horizontal padding: `margin-screen-default` (16px).

## Platform behavior
Android is the default spec (see [`CLAUDE.md`](../CLAUDE.md)). iOS is documented only where it
meaningfully diverges.

- **Android (default)**: Standard Material text field and button treatment.
- **iOS (if different)**: No deviation currently scoped.

## Accessibility
- The composer's expected-input-type must be announced when a new agent turn begins (e.g.
  "Enter a number" vs. "Confirm your selection above"), since the control's function changes
  turn to turn and that's not obvious from a static screen reader pass alone.
- Disabled Submit/Confirm states must announce *why* they're disabled, not just that they are.

## Do / Don't
- **Do** make the terminal Submit control's disabled reason explicit and tied to the actual
  gate (signature required) rather than a generic "complete all fields" message.
- **Do** keep the composer's visible control minimal and singular per turn — never show a
  text field and a confirm button and a capture trigger simultaneously.
- **Don't** silently swap what the composer does without a clear cue from the preceding
  `agent-message` about what's being asked for.

## Related components
`agent-message`, `option-card`, `progress-indicator`, `signature-capture` (opened by the
Capture trigger variant; its Completed or Declined state gates this component's terminal
Submit control)
