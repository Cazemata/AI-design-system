# Agent Message

## Overview
The agent's turn in the conversational flow. Carries a question, a statement, a validation
response, or a summary recap. This replaces the static "Question" label + form-field block
pattern used throughout the original GigaCheck screens — instead of a form field with a bold
label above it, the technician sees the same content phrased as something being *asked* or
*told* to them, one exchange at a time.

Agent messages are never editable directly — they're paired with a response control
(`option-card`, `chat-composer`, or a signature/photo capture widget) that carries the
technician's actual input.

## Anatomy
1. **Avatar/icon** (optional, 24×24) — small system/agent mark, left-aligned. Omitted on
   consecutive agent messages in the same turn group (see Grouping below).
2. **Bubble** — rounded container, left-aligned, max-width ~85% of viewport.
3. **Body text** — the question or statement itself.
4. **Helper/context text** (optional) — smaller, muted text beneath the body, used for the
   explanatory copy that used to sit as field helper text (e.g. "Internet connection can be
   increased to 1,000 Mbit/s").
5. **Timestamp** (optional, shown on long-press or hover, not by default) — avoid cluttering
   a technician-facing tool with chat-app chrome it doesn't need.

## Variants
- **Question** — asks for input; always paired with a response control on the next turn.
- **Statement** — informational only (e.g. "Let's check the coverage area next"), no response
  control required, used for section transitions (replaces the lettered section dividers:
  A. DEIN AUFTRAG, B. DEIN ZUHAUSE, etc.)
- **Validation follow-up** — appears when the technician's previous answer fails a required
  check (replaces "Mandatory field hasn't been filled!" / "Select at least one field!").
  Uses `color-critical` for the bubble background/border instead of the default bubble's
  `color-surface-default`, and always restates what's needed in plain language rather than a
  generic error string.
- **Summary recap** — a longer-form agent message listing everything captured so far,
  replacing the static Summary screen. Groups sub-items visually (see Related patterns) but
  remains a single conversational turn with an explicit "Anything to change?" follow-up
  rather than a grid of inline edit icons.

## States
| State | Visual change | Description |
|---|---|---|
| Default | Bubble renders at full opacity with complete text | Static, fully rendered message |
| Streaming | Text reveals progressively (token-by-token or per-sentence) using `motion-duration-default` / `motion-ease-decelerate` | Used when generated live rather than pre-scripted; never shows a spinner |
| Error (validation) | `color-critical` background tint on the bubble, icon replaces avatar | Feedback/error variant; always restates what's needed in plain language |

## Sizing & spacing
- Bubble padding: `spacing-16` horizontal, `spacing-12` vertical.
- Gap between avatar and bubble: `spacing-8`.
- Gap between consecutive messages in the same turn: `spacing-8`; gap between different
  speakers' turns: `spacing-16`.
- Corner radius: `radius-md` (see [`spacing.md`](../00-foundations/spacing.md)), matching
  `option-card`'s container radius for visual consistency.
- Body text: `type-body-md`. Helper text: `type-body-sm` or `type-caption`, in
  `color-text-secondary`.

## Platform behavior
Android is the default spec (see [`CLAUDE.md`](../CLAUDE.md)). iOS is documented only where it
meaningfully diverges.

- **Android (default)**: Bubble and streaming-text pattern as described above.
- **iOS (if different)**: No deviation — both platforms use the same bubble/streaming pattern.

## Accessibility
- Agent messages are announced as they appear; streaming text should not fire a screen-reader
  announcement per token — announce once the message is complete, using the platform's native
  live-region equivalent (TalkBack's `AccessibilityLiveRegion` on Android, a debounced VoiceOver
  announcement on iOS), not a web ARIA attribute.
- Validation follow-up messages must be programmatically associated with the field/control
  they refer to (not just visually adjacent), so assistive tech users get the correction in
  context.
- Never rely on bubble color alone to convey the "error" variant — pair with the icon and the
  restated instruction text.

## Do / Don't
- **Do** keep one question (or one tightly-related group, like Morning/Afternoon) per agent
  turn — this is the direct replacement for "one Question block per form section."
- **Do** let the Statement variant carry section-transition context, so the technician always
  knows what part of the check they're in without a persistent stepper header.
- **Don't** stack multiple unrelated questions in a single bubble — that reintroduces the
  dense form-field problem this component exists to solve.
- **Don't** use the Validation follow-up variant for anything except a failed required-field
  check — general errors (network failure, send failure) belong in a different pattern.

## Related components
`option-card`, `chat-composer`, `progress-indicator`
