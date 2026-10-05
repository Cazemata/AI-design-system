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

Some items below are marked as confirmed by one of two non-Figma passes, flagged inline where
they occur: the **2026-10 stakeholder workshop** (hand-written German sticky notes — confirmed
product *decisions*, not pixel-level screens), and the **2026-10 screenshot pass** (updated
screenshots of the current static-form design — screen-level content, but captured from
screenshots rather than read from Figma, so new screens carry no node IDs).

## Section-by-section mapping

**Flow order (confirmed 2026-10):** Introduction → Coverage Area → Living Area → Your products
→ Summary → Consent (BEW) → Customer signature → Send/Success. Sections below appear in that
order. Screens removed from the flow are recorded under **Removed from the flow** near the end
of this file rather than in the active mapping.

### Introduction *(source flow: A. DEIN AUFTRAG)*
**Now confirmed** — **confirmed via 2026-10 screenshot pass**. This section was an open item
from the original extraction onward; the updated screenshots show its first screen (see
`gigacheck-flow-schema.md`, section A). The nodes once placed here (`1:2128`/`1:2091`) were
reassigned to the Internet Status screen, which has since been removed from the flow — see
**Removed from the flow** below.

- Agent Statement turn: brief intro to the check ("Let's get started — I'll walk through a
  few checks with you.")
- **"Could you resolve the issue?"** — single-select `option-card` Question turn (Yes / No).
  - `Yes` → the conversation continues into the Home & Connectivity checks below.
  - `No` → two follow-up turns, in order:
    1. A multi-select `option-card` Question turn for **Reasons** (mandatory): "Needs further
       work (NE3 / structural)" / "No access / customer not reachable" / "Third-party NE4
       facility."
    2. A `chat-composer` free-text turn for **"Other."** The static screen's `0/300` counter
       becomes the composer's own character limit — don't carry the counter across as visible
       chrome borrowed from the form.
  - **Translation note:** the static screen *reveals* Reasons and Other inline beneath a `No`
    answer, so both are present-but-empty on screen. Conversationally they're separate turns
    that only appear once `No` is chosen — nothing is shown then hidden, and nothing sits
    empty waiting to be noticed.
  - **Unconfirmed:** what happens after the `No` path captures its reasons — whether the flow
    ends there or continues. The earlier workshop sketch showed an "Always On" offer and a
    follow-up-steps message at this point; neither appears in the screenshots, so neither is
    mapped here.

### Home & Connectivity Check *(source flow: B. DEIN ZUHAUSE)*
- **Coverage Area** (`1:2052`): two Question turns — "Test point" and "Amplifier" — each
  paired with a multi-select `option-card` ("Tested and working" / "Not tested").
  **Confirmed via 2026-10 screenshot pass** — "Handover point" was renamed to "Test point,"
  and this option pair replaces the earlier "Checked and values checked" / "Exchanged."
- **Living Area / Wohnbereich** (`1:2844`→`1:2773`→`1:2920`): single-select `option-card` turn
  for "Booked Products - Mandatory" (TV Only / Internet Only / Internet and TV), followed by
  three Question turns, each paired with a multi-select `option-card` — all option wording
  **confirmed via 2026-10 screenshot pass** from the active, non-grayed state:
  - "Router - Mandatory" — "Tested and working" / "Exchanged" / "Customer uses third-party
    device" (third option new in this pass)
  - "Multimedia-Dose - Mandatory" — "Tested and working" / "Exchanged" / "No Multimedia-Dose
    available" (the third option's wording is **unconfirmed against the new design** — the
    screenshot cuts it off, so it carries over from the original extraction)
  - "Connection Cable" — "Tested and working" / "Exchanged". **New turn in this pass**, asked
    after Multimedia-Dose, and **not** marked mandatory.
  - **Branching — the gating is now corroborated by the static design; only the mechanism is
    our translation.** The 2026-10 screenshot pass shows the static screen graying out Router
    and Multimedia-Dose and dropping their "Mandatory" label when `TV Only` is selected, with
    Connection Cable left enabled. So **conditional branching is no longer a deviation we
    introduced** — the current design gates these fields too. What remains a deliberate
    translation is the *mechanism*: a turn-based conversation has no equivalent of a
    visible-but-disabled field, so those turns are **skipped entirely** rather than asked and
    shown grayed. This corroborates the skipping language that was already here from the
    workshop pass rather than replacing it with a new pattern.
  - **Still flagged on branching:** (a) the screenshots show only the `TV Only` state, so the
    other half of the rule — TV-related turns skipped when "Internet Only" is chosen —
    remains **uncorroborated**; (b) the original prototype click-path recorded in
    `gigacheck-flow-schema.md` played all three Wohnbereich frames in sequence with no
    gating at all, so **prototype and current static design now disagree** on whether this
    radio gates anything. Treat the prototype as history on this point.
  - **Flag — probable mockup inconsistency, not normalized:** in the grayed `TV Only` state,
    the disabled Router and Multimedia-Dose options still read the old "Checked and values
    checked" wording while the rest of the screen uses the new wording. Confirm rather than
    quietly normalizing it in either direction.
- **Your products** — **confirmed via 2026-10 screenshot pass** (no node ID captured). Asked
  **directly after Living Area**, per the confirmed flow. **This section deliberately mixes a
  Question turn with a Statement turn, because the static screen mixes two different kinds of
  content:**
  - **Question turn — the product / functional checks are real input.** A multi-select
    `option-card` turn covering Internet, Phone, WLAN, and TV. The static screen's two-column
    "Product" / "Functional" grid is *layout*, not two separate questions — don't carry the
    grid across as a table.
  - **Statement turn — the speed-test values are not input at all.** The three measured
    bandwidth values (measured bandwidth, bandwidth measured on the multimedia outlet,
    bandwidth on the modem) are read automatically from a speed test. The technician has
    nothing to supply, so there is nothing to ask. They render as one informational
    `agent-message` Statement turn — a readout, e.g. "Here's what the speed test found: …" —
    **not** as `chat-composer` numeric fields, and **not** as a Question turn.
  - **Why the mix (worth being explicit about):** everywhere else in this mapping, a static
    field becomes a Question turn because the technician supplies the value. Auto-measured
    values break that assumption. A Question turn would imply the technician is being asked
    for something they can't change; a `chat-composer` field would imply the value is
    editable. A Statement readout is the correct conversational form for system-supplied data,
    and it's the reason this one section isn't all one turn type.
  - **Unconfirmed — the Functional dependency:** one screenshot shows WLAN unchecked with its
    "Functional" box disabled, suggesting Functional only enables once the product itself is
    checked. **Inferred, not confirmed.** If it is confirmed, the conversational equivalent is
    that the functional question is only *asked* for products the technician marked as
    present — again a skipped turn, not a disabled option.
  - **Unconfirmed — label copy:** the two screenshots word the three bandwidth labels slightly
    differently; `gigacheck-flow-schema.md` records the longer wording. Confirm before the
    readout copy is written.

### Summary *(source flow: D. SUMMARY)*
- **Summary** (`1:1524`): a single Summary recap `agent-message`, listing every answer
  captured so far in grouped, readable form — not a literal re-rendering of every field.
  Followed by a `chat-composer` Continue affordance and an explicit "Anything to change?"
  prompt.
- **Edit flow**: instead of the original Edit_overlay screens, an "Anything to change?" answer
  of "yes" re-opens the relevant section as a short conversational detour (re-asking just that
  section's Question turns), then returns to the recap. This avoids the original's separate
  overlay screens while preserving the same edit capability.
- **What the recap now covers (updated to the confirmed flow, 2026-10).** The recap echoes
  only what the flow actually collects:
  1. The **"Could you resolve the issue?"** answer — and, on the `No` path, the selected
     Reasons plus any "Other" free text.
  2. **Coverage Area** — Test point and Amplifier ("Tested and working" / "Not tested").
  3. **Living Area** — Booked Products, Router, Multimedia-Dose, and **Connection Cable**
     ("Tested and working" / "Exchanged"), honoring the `TV Only` branching: turns that were
     skipped have nothing to echo, so the recap shouldn't show empty rows for them.
  4. **Your products** — the Product / Functional checks, plus the speed-test readout. The
     readout values are echoed as *reported*, not as answers the technician gave.
- **Field-level wording still pending.** The actual Summary screen was German-language and too
  small to read in the screenshots, so the list above reflects what the flow collects rather
  than what the screen is confirmed to display. Exact labels and grouping remain unconfirmed.

### Confirmation / Consent
> **Note — section-lettering gap:** the original Figma file has no lettered section between
> **D. SUMMARY** and **F. FEEDBACK**. This content (Confirmation / Consent, and Customer
> Signature below) likely corresponds to an unlabeled "E" section in the source file that was
> never named. Flagging this rather than assigning a label ourselves.

- Consent turns render as two Question turns (multi-select `option-card`, single item each,
  since each consent is independently optional) using the exact legal copy confirmed in the
  schema — see `voice-and-tone.md`'s Legal & consent copy rule for how this copy must be
  handled. These are the **BEW (Beratungseinwilligung / consultation consent)** checkboxes.
- **Scheduling question removed** — **confirmed via 2026-10 stakeholder workshop, not a new
  Figma pass** ("Vormittags / Nachmittags raus"). The "When would you like to be contacted?"
  Morning/Afternoon question, its two options, and its Validation follow-up (previously
  standing in for the `1:2697` error state) are no longer part of this flow. The only
  remaining requirement is the two BEW consent checkboxes above.
- **Not adopted — BEW stays separate (confirmed 2026-10).** The workshop note had floated
  consolidating BEW onto the same screen as Customer Signature ("evtl. mit Unterschrift auf
  eine Seite"). The confirmed flow keeps Consent (BEW) as its own step between Summary and
  Customer signature, so the consolidation was **not adopted**. This replaces the earlier
  "proposed, not yet settled" note.

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
- **Waiver path — confirmed via 2026-10 screenshot pass** (supersedes the workshop pass's
  description): the customer can decline to sign via a **plain checkbox labeled "Customer
  waives signature,"** placed next to the canvas, with **no confirmation step**. The body copy
  above is also re-confirmed as current by this pass. Conversationally the waiver stays part
  of the signature turn rather than becoming a turn of its own — it's an alternative way to
  complete the same turn, not a separate question. See `signature-capture.md`'s **Waived**
  state for component-level detail; the control itself delegates to `checkbox-radio`.
- **Not adopted** (see Confirmation / Consent above): the floated consolidation of the BEW
  consent checkboxes onto this screen was not adopted — BEW stays its own preceding step.
- **Confirmed**: the customer must either sign or have the waiver checked before the report
  can be sent — "Send report" is the final action on this screen, so one of those two
  outcomes is a hard requirement for report generation, not optional.
- **Unconfirmed**: the exact UI mechanism enforcing that requirement — whether the terminal
  Submit control (`chat-composer` Submit variant, "Send report") is disabled outright until a
  signature or waiver is present, or instead remains tappable and fails validation on tap.
  This needs confirmation before implementation.
- **Don't introduce:** an alternative body sentence appeared in one screenshot and was
  confirmed **not** current. It's deliberately not recorded here or in the schema.

### Feedback *(source flow: F. FEEDBACK)*
- **Send/Success** (`1:1460`): rendered as an inline system confirmation message in the
  conversation thread (the "report was successfully sent" copy, plus the "I've informed the
  customer" action) rather than a full-screen takeover — keeps the technician in the same
  conversational context rather than ejecting them to a separate screen. **Confirmed as
  final** — this inline treatment replaces the original's full-screen success paradigm.
- **Dual delivery on send** — **confirmed directly with the product owner, not sourced from
  `gigacheck-flow-schema.md`** (the schema only documents the MeinVodafone-Portal outcome;
  this requirement falls outside its Figma extraction, so it isn't recorded there — see that
  file's own header): "Send report" triggers two things together on every successful send,
  not as alternatives — (1) the report becomes available on the MeinVodafone-Portal (the
  schema's original confirmed behavior), and (2) a PDF of the report is generated and emailed
  directly to the customer. The inline Send/Success message should reflect both outcomes,
  since the schema's original copy only mentions the portal.
- **Send/Error** (`1:1493`): **deferred** — being addressed in a separate pass, not specified
  in this mapping. Its trigger condition wasn't confirmed during the walkthrough; a tentative
  mapping to `chat-composer`'s Submit Error state (inline "Sending the report failed — want
  to try again?") is noted for reference only and should not be treated as confirmed until
  that separate pass resolves it.
  - **Open question**: whether Send/Error needs to distinguish which delivery channel failed
    (portal vs. PDF/email) now that send has two outcomes, or a single generic failure state
    is sufficient — not resolved, flagging only.

## Removed from the flow (confirmed 2026-10)

These sections were in the active mapping until the flow was confirmed. One note each, kept so
the history is traceable; see `gigacheck-flow-schema.md` for the retained screen-level records.

**Design principle (confirmed 2026-10):** the technician flow stays free of sales-related
prompts, so the technician doesn't upset the client with sales-related topics. Check any
future addition to this mapping against that principle before adding it.

- **Internet Status** (`1:2128` / `1:2091`) — removed. Its subject matter moved to **Your
  products**: "Internet" is now a Product / Functional row, and bandwidth is a speed-test
  readout rather than two `chat-composer` numeric turns. Both workshop open questions attached
  to this section are **resolved by removal**: the "show the booked bandwidth more prominently"
  note and the "is Maximum technical available bandwidth a field anyone needs" note no longer
  apply, since the field itself is gone and bandwidth is now measured, not entered.
- **WLAN** (`1:2019`) — removed. WLAN survives only as a Product / Functional row in **Your
  products**. The signal-strength numeric turn was **dropped on purpose (confirmed 2026-10)**
  and needs no replacement — not an unfilled gap.
- **Telefon** (`1:3067`–`1:3172`) — removed. Phone survives only as a Product / Functional row
  in **Your products**. The "Other provider" option was **dropped on purpose (confirmed
  2026-10)** — removed so the technician doesn't raise sales-related topics with the client —
  and needs no replacement.
- **Optimization Options** (TV/Internet usage check `1:1964`/`1:1912`, OptimiseInternet
  `1:1854`, OptimiseTV `1:1789`) — the whole section is removed, with no content relocated.
  Two earlier notes are resolved by that removal:
  - The workshop pass's **"trim upsells to informational-only"** scope reduction is **moot** —
    there is no upsell content left to trim. Removed rather than kept as a live instruction.
  - The **"TV Nutzung - nur wenn kein TV gebucht"** conflict flag (a workshop sketch note that
    contradicted the Wohnbereich branching) is **resolved by removal** — the TV usage check it
    referred to no longer exists, so there's no conflict left to reconcile.
  - The `.definitionToggle` behavior question also loses its subject here; see the fallout note
    in `definition-toggle.md`.

## Open items carried from the flow schema
- Introduction section — **mostly resolved** by the 2026-10 screenshot pass ("Could you
  resolve the issue?"). Residual: the "Always On" offer and follow-up message from the
  workshop sketch aren't in the screenshots, and the `No` path's continuation is unknown.
- Send/Error trigger condition — deferred to a separate pass (see Feedback above).
- Customer Signature's disable-vs-validate-on-tap *mechanism* for "Send report" — unconfirmed
  (the requirement to sign *or have the waiver checked* before sending is itself confirmed;
  only the enforcement mechanism is open — see Customer Signature above).
- VF KDG branded-section scope — unresolved, per `gigacheck-flow-schema.md`.
- **Resolved (confirmed 2026-10):** the six previously-unconfirmed screens are removed from
  the flow, and "Your products" does supersede the Optimization Options section — see Removed
  from the flow above. The "don't build both versions" warning no longer applies.
- Summary recap — now scoped to what the flow actually collects (see Summary above), but
  field-level wording is still pending a readable Summary screen.
- Screen-title naming: the new screenshots title the Coverage Area screen "Coverage Area,"
  while `gigacheck-flow-schema.md`'s section header and `terminology.md` say "Service Area."
  Left for a separate terminology cleanup, not fixed here.

## Related
`gigacheck-flow-schema`, `agent-message`, `option-card`, `chat-composer`,
`progress-indicator`, `terminology`, `voice-and-tone`
