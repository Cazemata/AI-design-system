# Pattern: Conversational Flow (GigaCheck Redesign)

## Overview
This pattern describes how the confirmed GigaCheck screen flow (see
`gigacheck-flow-schema.md`) is re-expressed as a conversational, agent-led sequence using
`agent-message`, `option-card`, `chat-composer`, and `progress-indicator`. The goal: a
technician moves through the same verification checklist, but experiences it as a guided
back-and-forth rather than a stack of static forms — while preserving every mandatory
field, validation rule, and branching behavior confirmed in the schema, except where a
deliberate deviation is called out explicitly (see Living Area / Wohnbereich below).

This is a **1:1 content mapping** for the majority of the flow — every question, option,
helper text, and validation rule carries over exactly unless flagged otherwise. What changes
is the presentation: one exchange at a time instead of a full-screen form per step.

**Section headers below use plain descriptive names, not the source file's lettered
structure (A, B, C, D, F).** Confirmed decision: letters don't add value in a conversational
flow, since `progress-indicator` and `agent-message` Statement turns already carry
section-transition context on their own. Original lettered section names are noted
parenthetically for provenance only, where relevant.

German section/field names and bilingual copy conventions used throughout this mapping are
catalogued in `terminology.md`; copy-handling and register rules (including the legal-copy
verbatim rule) are in `voice-and-tone.md`.

## Section-by-section mapping

### Introduction *(source flow: A. DEIN AUFTRAG)*
**Still unidentified** — the two nodes previously placed here (`1:2128`/`1:2091`) have been
reassigned: Figma verification confirmed they're actually an "Internet Status" screen
(`1:2128` empty/error state, `1:2091` the same screen filled in — not separate content),
which now lives under Home & Connectivity Check below. This section's real intro screens
haven't been found yet.

- Agent Statement turn: brief intro to the check ("Let's get started — I'll walk through a
  few checks with you.")

### Home & Connectivity Check *(source flow: B. DEIN ZUHAUSE)*
- **Coverage Area** (`1:2052`): two Question turns — "Handover point" and "Amplifier" — each
  paired with a multi-select `option-card` ("Checked and values checked" / "Exchanged").
- **Internet Status** (`1:2128` / `1:2091` — reassigned from the original intro placement;
  confirmed via Figma to be one screen in two states, not separate content): multi-select
  `option-card` turn for "Internet Status — mandatory" ("Internet is working" / "Internet is
  used"), followed by two `chat-composer` numeric turns: "Booked Bandwidth (Mbit/s) —
  mandatory" and "Maximum technical available bandwidth (Mbit/s) — mandatory."
- **Living Area / Wohnbereich** (`1:2844`→`1:2773`→`1:2920`): single-select `option-card` turn
  for "Booked Products - Mandatory" (TV Only / Internet Only / Internet and TV), followed by
  the "Router - Mandatory" / "Multimedia-Dose - Mandatory" Question turns, each paired with a
  multi-select `option-card` ("Checked and values checked" / "Exchanged"); "Multimedia-Dose"
  additionally offers a third option, "No Multimedia-Dose available." **Confirmed decision —
  conditional branching (deviates from the original):** the original prototype played all three Wohnbereich
  screens sequentially regardless of the radio answer; this redesign intentionally branches
  instead — TV-related turns are skipped when "Internet Only" is chosen, internet-related
  turns are skipped when "TV Only" is chosen. **This is a deliberate improvement, not a
  like-for-like carryover** — flag this explicitly if anyone later compares the
  conversational flow against the original prototype for parity, since the turn sequence
  will legitimately differ.
- **WLAN** (`1:2019`): "Wi-Fi works"/"Wi-Fi is used" Question turn, plus a numeric/text turn
  for signal strength via `chat-composer` text/numeric variant.
- **Telefon** (`1:3067`→`1:3102`→`1:3137`→`1:3172`): "Telephone is working"/"is used"/"Other
  provider" Question turn(s), sequential per the confirmed path.

### Optimization Options *(source flow: C. OPTIMIZATION OPTIONS)*
- TV/Internet usage check (`1:1964`, `1:1912`): Question turns with multi-select
  `option-card`, including the validation-follow-up path for the "Mandatory field hasn't
  been filled!" case.
- **OptimiseInternet** (`1:1854`) and **OptimiseTV** (`1:1789`): rendered as a sequence of
  Upsell offer card turns (one agent Statement introducing the offers, then the cards
  themselves), preserving each helper/definition line from the original screens.
  - **Open question — `.definitionToggle` behavior**: OptimiseInternet's "has received" /
    "has NOT received a FREE WiFi router" copy uses the original `.definitionToggle`
    component. The schema only confirms this as an account-driven conditional copy swap, not
    something the technician taps — see `definition-toggle.md`'s Conditional vs. Expandable
    variants for the full detail. Needs a decision before implementation; not resolved here.

### Summary *(source flow: D. SUMMARY)*
- **Summary** (`1:1524`): a single Summary recap `agent-message`, listing every answer
  captured so far in grouped, readable form — not a literal re-rendering of every field.
  Followed by a `chat-composer` Continue affordance and an explicit "Anything to change?"
  prompt.
- **Edit flow**: instead of the original Edit_overlay screens, an "Anything to change?" answer
  of "yes" re-opens the relevant section as a short conversational detour (re-asking just that
  section's Question turns), then returns to the recap. This avoids the original's separate
  overlay screens while preserving the same edit capability.

### Confirmation / Consent
> **Note — section-lettering gap:** the original Figma file has no lettered section between
> **D. SUMMARY** and **F. FEEDBACK**. This content (Confirmation / Consent, and Customer
> Signature below) likely corresponds to an unlabeled "E" section in the source file that was
> never named. Flagging this rather than assigning a label ourselves.

- Consent turns render as two Question turns (multi-select `option-card`, single item each,
  since each consent is independently optional) using the exact legal copy confirmed in the
  schema — see `voice-and-tone.md`'s Legal & consent copy rule for how this copy must be
  handled.
- Scheduling ("When would you like to be contacted?") is a single-select `option-card` turn
  for Morning/Afternoon.
- **Confirmed validation rule carries over exactly**: if the scheduling question is skipped or
  not registered, the flow surfaces the Validation follow-up `agent-message` variant (standing
  in for the `1:2697` error state) rather than silently blocking — matching the real behavior
  we confirmed by walking the prototype.

### Customer Signature
> **Note — section-lettering gap:** this section falls in the same unlabeled gap between
> **D. SUMMARY** and **F. FEEDBACK** flagged under Confirmation / Consent above — see that
> note for detail.

- Confirmed node: `1:3224` ("Landscape DE" in the Figma file), a landscape-oriented frame
  (809×360) — signing is expected with the device rotated, so the capture surface for this
  turn should expect/support landscape orientation.
- A dedicated turn using the `chat-composer` Capture trigger variant, opening the signature
  pad. Confirmed copy: title "Customer signature," body "I hereby confirm that the technical
  order has been fulfilled and that I have been informed about the service provided," buttons
  "Zurück" (glossed in `terminology.md`) / "Send report." The body copy renders as the
  preceding agent Statement turn, not as an incidental caption.
- **Confirmed**: the customer must sign before the report can be sent — "Send report" is the
  final action on this screen, so signature capture is a hard requirement for report
  generation, not optional.
- **Unconfirmed**: the exact UI mechanism enforcing that requirement — whether the terminal
  Submit control (`chat-composer` Submit variant, "Send report") is disabled outright until a
  signature is present, or instead remains tappable and fails validation on tap (mirroring the
  scheduling field's behavior). This needs confirmation before implementation.

### Feedback *(source flow: F. FEEDBACK)*
- **Send/Success** (`1:1460`): rendered as an inline system confirmation message in the
  conversation thread (the "report was successfully sent" copy, plus the "I've informed the
  customer" action) rather than a full-screen takeover — keeps the technician in the same
  conversational context rather than ejecting them to a separate screen. **Confirmed as
  final** — this inline treatment replaces the original's full-screen success paradigm.
- **Send/Error** (`1:1493`): **deferred** — being addressed in a separate pass, not specified
  in this mapping. Its trigger condition wasn't confirmed during the walkthrough; a tentative
  mapping to `chat-composer`'s Submit Error state (inline "Sending the report failed — want
  to try again?") is noted for reference only and should not be treated as confirmed until
  that separate pass resolves it.

## Open items carried from the flow schema
- Introduction section's real screens (previously referenced as A. DEIN AUFTRAG) are still
  unidentified.
- Send/Error trigger condition — deferred to a separate pass (see Feedback above).
- Customer Signature's disable-vs-validate-on-tap *mechanism* for "Send report" — unconfirmed
  (the requirement to sign before sending is itself confirmed; only the enforcement mechanism
  is open — see Customer Signature above).
- VF KDG branded-section scope — unresolved, per `gigacheck-flow-schema.md`.

## Related
`gigacheck-flow-schema`, `agent-message`, `option-card`, `chat-composer`,
`progress-indicator`, `terminology`, `voice-and-tone`
