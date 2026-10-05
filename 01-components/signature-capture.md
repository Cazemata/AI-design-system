# Signature Capture

## Overview
The signature pad widget used for the Customer signature turn — confirmed via the flow
schema (`gigacheck-flow-schema.md`, node `1:3224` "Landscape DE"). This is a **hard gate
before report submission**: per the confirmed source screen, the customer must sign before
the report can be sent, so the paired `chat-composer` Submit ("Send report") control must
not be enabled until this component reports either a completed signature or a checked
**signature waiver** (see the Waiver checkbox below — **confirmed via 2026-10 screenshot
pass**). This component is signature-only — there is no photo/camera capture step anywhere in
the confirmed source flow, and this file does not cover one.

## Anatomy
1. **Canvas** — the drawing surface where the signature stroke is captured.
2. **Baseline guide** — a subtle line indicating where to sign.
3. **Signature stroke** — the rendered ink once drawing begins.
4. **Clear affordance** — resets the canvas to empty.
5. **Back affordance** — returns to the previous turn without confirming (mirrors the
   confirmed screen's "Zurück" button).
6. **Done affordance** — commits the signature and returns control to the conversation
   thread; this is what flips the external `chat-composer` Submit control from disabled to
   enabled. (The confirmed source screen combines the signature pad and "Send report" on one
   frame; this redesign splits them — Done here just commits the signature, and the actual
   send happens via the separate terminal `chat-composer` Submit control back in the thread.)
7. **Waiver checkbox** — **confirmed via 2026-10 screenshot pass** (supersedes the workshop
   pass's description of this affordance): a plain checkbox labeled **"Customer waives
   signature,"** placed next to the canvas. Checking it is the entire interaction — there is
   **no** confirmation step before it commits. Delegate the control itself to
   `checkbox-radio` (Checkbox variant) rather than drawing a bespoke one.

## Variants
- **Landscape (confirmed)** — the only orientation confirmed in the source flow: node
  `1:3224` is an 809×360 landscape-oriented frame, since signing is expected with the device
  rotated. No portrait treatment has been confirmed; treat portrait as out of scope until
  specified.

## States
| State | Visual change | Description |
|---|---|---|
| Empty (default) | Canvas shows only the baseline guide, no stroke | Awaiting the first touch/stroke; Done is disabled in this state |
| Mid-signature | Stroke renders live as the finger/stylus moves | Actively being drawn |
| Completed | Full stroke visible, Clear and Done both available | A signature is present; this is the state that unlocks the external `chat-composer` Submit control |
| Waived | "Customer waives signature" checkbox is checked; the canvas is no longer required | **Confirmed via 2026-10 screenshot pass**, superseding the workshop pass's "Declined" description — there is no confirmation step, and the canvas is not cleared or dimmed on check. Reached by checking the waiver box, not by leaving Empty untouched; unlocks the external `chat-composer` Submit control as an alternative to Completed — not a failure state |

## Sizing & spacing
- Reference frame: 809×360 (landscape), per the confirmed source node — treat as a reference
  aspect ratio rather than a fixed pixel size across devices.
- Canvas margin from frame edges: `spacing-16`.
- Clear/Back/Done tappable areas: `touch-target-min-android` minimum each, with at least
  `spacing-8` between adjacent controls to avoid mis-taps.
- Button label text: `type-label`.

## Platform behavior
Android is the default spec (see [`CLAUDE.md`](../CLAUDE.md)). iOS is documented only where
it meaningfully diverges.

- **Android (default)**: the surface locks to landscape orientation for the duration of this
  turn, regardless of the device's rotation-lock setting, matching the confirmed source
  screen; returns to the app's normal orientation behavior once Done is tapped.
- **iOS (if different)**: no difference in orientation-lock intent, but implemented via
  iOS's own orientation-lock API rather than Android's.

## Accessibility
- **Known, unresolved gap**: freehand signature capture has no accessible equivalent for
  screen-reader or switch-access users — this is a real limitation of signature pads
  generally, not specific to this design system, and isn't solved here. Flagging rather than
  asserting a fix; an alternative confirmation path for users who cannot draw a signature
  needs a product decision before this ships.
- Clear, Back, and Done each need a clear accessible label ("Clear signature," "Back,"
  "Done") — not icon-only with no label.
- Minimum touch target for all three controls: `touch-target-min-android` (see
  [`spacing.md`](../00-foundations/spacing.md)).
- Screen reader behavior: announce the transition into the Completed state (e.g. "Signature
  captured") so non-visual users know Done is now meaningful to activate.
- The waiver checkbox exposes checkbox semantics and announces its checked/unchecked state
  per `checkbox-radio`, with the accessible name taken from its visible label ("Customer
  waives signature") and kept distinct from Clear/Back/Done.

## Do / Don't
- **Do** keep the external `chat-composer` Submit control disabled until this component
  reports Completed *or* Waived — this is a functional gate, not just a visual one.
- **Do** force landscape orientation for this turn specifically, matching the confirmed
  source screen.
- **Don't** let Done be tappable while the canvas is Empty.
- **Don't** add a confirmation step before the waiver commits — the confirmed design is a
  plain checkbox. (The workshop pass described a confirm-before-commit dialog; the 2026-10
  screenshot pass superseded that. The accidental-check risk is real but isn't mitigated this
  way in the current design — raise it as a design question rather than reintroducing a
  dialog here.)
- **Don't** add a camera/photo capture affordance here — that was never part of the confirmed
  source flow.

## Related components
`chat-composer` (paired Submit control and Capture trigger variant), `agent-message`
(carries the confirmed legal copy as the preceding Statement turn), `checkbox-radio` (the
waiver checkbox delegates to its Checkbox variant)
