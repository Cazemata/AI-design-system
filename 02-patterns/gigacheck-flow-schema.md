# GigaCheck Flow Schema

Extracted from Figma file "AI Design System Test" (fileKey: `63HryYbfkIyzath7V25H6q`), page "Page 1", section "GIGA CHECK FORM".

**Context:** A field-technician tool (Vodafone West / VF KDG branded) used during a home service visit to verify that internet, Wi-Fi, phone, and TV services are working, offer optimization upsells, capture customer consent, and send a completion report.

This is a linear multi-step checklist wizard with an editable summary and a confirmation/consent step before submission.

**Workshop update note (2026-10):** some entries below are marked as confirmed via a
stakeholder workshop (hand-written German sticky notes), not a new Figma extraction pass.
Flagged inline at each occurrence — these are confirmed *decisions*, not confirmed
*pixel-level screens*, which is a different kind of confirmation than the rest of this file.

---

## A. DEIN AUFTRAG (Your Order) — intro
No screens confirmed in this section yet. `1:2128`/`1:2091` were originally placed here based
on canvas x-position only — confirmed via `get_design_context` to actually be **"Internet"**
status screens (see corrected placement under B below), not order/job intro content. This
section's actual screens remain unidentified.

## B. DEIN ZUHAUSE (Your Home)

**`GigaCheck` / "Internet"** — `1:2128` (empty/error state), `1:2091` (filled/valid state —
same screen, not separate content)
- Title: "Internet"
- Question: **"Internet Status — mandatory"** — checkboxes "Internet is working" / "Internet
  is used"
- Question: **"Booked Bandwidth (Mbit/s) — mandatory"** — numeric input
- Question: **"Maximum technical available bandwidth (Mbit/s) — mandatory"** — numeric input
- `1:2128` shows the empty state with "Mandatory field hasn't been filled!" on all three
  fields; `1:2091` shows the same screen filled in (Internet is working ✓, bandwidth
  "123456"). Both are the same screen at different fill states, not two distinct steps.

**`GigaCheck/Versorgungsbereich` (Service Area)** — `1:2052`
- Two checkbox questions — **"Handover point"** and **"Amplifier"** (confirmed via
  `get_design_context`) — each offering:
  - "Checked and values checked"
  - "Exchanged"

**`GigaCheck/Wohnbereich` (Living Area)** — `1:2844`, `1:2773`, `1:2920` (variants)
- Radio question: **"Booked Products - Mandatory"**
  - Options: `TV Only` / `Internet Only` / `Internet and TV`
- Followed by two checkbox questions — **"Router - Mandatory"** and **"Multimedia-Dose -
  Mandatory"** (confirmed via live screenshot of this screen in the prototype) — each
  offering "Checked and values checked" / "Exchanged"; **"Multimedia-Dose"** additionally
  offers a third option, **"No Multimedia-Dose available."**
- *Branching signal:* this radio selection likely determines which of the later service-check screens (TV, Internet, Phone) are shown.

**`GigaCheck/WLAN`** — `1:2019`
- Checkbox question: **"Wi-Fi works"** / **"Wi-Fi is used"**
- Second question with a helper text field (numeric/signal input, exact label unresolved)

**`GigaCheck/Telefon` (Phone)** — `1:3067`, `1:3102`, `1:3137`, `1:3172` (4 variants — likely different states/errors)
- Checkbox question: **"Telephone is working"** / **"Telephone is used"** / **"Other provider"**

## C. OPTIMIZATION OPTIONS (upsell)
**`GigaCheck` (Internet check)** — `1:1964`, `1:1912`
- Checkbox question: **"Standard digital is used and TV works"** / **"4K box is used and TV works"** / **"Not in use"**
  - Includes a validation state: *"Mandatory field hasn't been filled!"*
- Second checkbox question: **"Other TV provider"** / **"SAT usage"** / **"Streaming Services"**

**`GigaCheck/OptimiseInternet`** — `1:3608`, `1:3679`, `1:1854` (variants — DE and EN copy present)
- Checkbox list of upsell offers:
  - **"Giga-Kund:in" / "Giga customer"** — helper: *"Internet connection can be increased to 1,000 Mbit/s"*
  - **"Super-WLAN" / "Super-Wi-Fi"** — helper: *"Intelligent reception technology for the router – super smart, super reliable"*
  - **"SuperWLAN-Verstärker" / "Super Wi-Fi Extender"** — helper: *"For strong Wi-Fi throughout the home"*
  - **"Expert Service"** — helper: *"Optimization of Wi-Fi and setup of smartphone, tablet, etc. by technician"*
  - A `.definitionToggle` component toggles copy between "Customer has received / has NOT received a FREE WiFi router" — a conditional micro-copy state, not a separate question.

**`GigaCheck/OptimiseTV`** — `1:1789`
- Checkbox list of TV product upsells:
  - `GigaTV Cable including HD Premium`
  - `GigaTV Cable`
  - `GigaTV Net`
  - `Audio by Bang & Olufsen`
  - `Extension to several rooms`
  - (list continues beyond metadata depth captured)

## D. SUMMARY
**`GigaCheck/Summary`** — `1:1524`
- Read-only summary card showing entered values (e.g. name "John", phone number, date) followed by **editable sections** echoing every checkbox answer collected earlier (e.g. "Checked and values checked" / "Exchanged" again).
- Each summary section has an edit affordance leading to:

**`GigaCheck/Summary/Edit_overlay`** — `1:2213`, `1:2989`, `1:2183` (3 variants — one per editable section)
- Re-presents the original question(s) for that section as an overlay/modal so the technician can correct an answer without leaving the summary.
- Includes the same validation state pattern: *"Mandatory field hasn't been filled!"*

## Confirmation / Consent (unlabeled section, between D and F)
**`GigaCheck/Confirmation`** — `1:2424`, `1:2466`, `1:2508`, `1:2697`, `1:2634`, `1:2571` (6 variants, as found in the original Figma extraction — see workshop note below)
- Consent checkboxes (legally-worded, customer-facing) — **BEW (Beratungseinwilligung / consultation consent)**:
  - *"Yes, I agree that Vodafone West GmbH may contact me for tariff advice by telephone..."*
  - *"Yes, I agree that Vodafone West GmbH may send me an e-mail... asking me to give my consent to advertising..."*
- **Workshop update (2026-10, not a new Figma pass):** the scheduling question some of the 6
  variants added — "Morning (08:00 - 12:00)" / "Afternoon (12:00 - 17:00)," with validation
  state "Select at least one field!" (node `1:2508` for the scheduling variant, `1:2697` for
  its validation-error variant) — has been **removed** per stakeholder decision ("Vormittags
  / Nachmittags raus"). No longer part of the confirmed requirement; the node IDs are kept
  here only as a historical record of what the original Figma screens showed.
- With scheduling removed, the only remaining requirement is the two BEW consent checkboxes
  above. The 6 original variants were combinations of consent-only vs. consent+scheduling,
  and empty/error/filled states — only the consent-only, non-scheduling variants are still
  relevant.

## F. FEEDBACK (submission result)
**`GigaCheck/Send/Success`** — `1:1460`
- Pop-up: *"The report was successfully sent. Please inform the customer that the report is available on the MeinVodafone-Portal."*
- Button: **"I've informed the customer"**

**`GigaCheck/Send/Error`** — `1:1493`
- Message: *"Sending the report failed"*

---

## Reference-only sections (not part of the linear flow)
- **INPUT INTERACTION** — `GigaCheck/ active field shows above keypad` (×5 variants): a UI-behavior reference showing how the active field/keypad interaction looks, not a flow step.
- **VALIDATIONS & ERRORS** — `GigaCheck/ example`: isolated reference frame for validation/error states.
- **VODAFONE WEST GmbH / VF KDG** — a client-branded variant set, likely a duplicate of the whole flow re-skinned for a different brand/partner. Worth checking whether this needs its own schema pass or is purely visual re-skinning.

---

## CONFIRMED real click-path (walked live in the prototype, not inferred from canvas)

```
1:2052 (Versorgungsbereich — Coverage Area: Handover point, Amplifier)
 → 1:2844 → 1:2773 → 1:2920 (Wohnbereich ×3 — play sequentially, NOT branched by the
    "Booked Products" radio selection; the radio does not appear to gate which screens
    are shown next in this prototype)
 → 1:2128 → 1:2091 ("Internet" status screen — empty state, then filled state; corrected
    from earlier "A. DEIN AUFTRAG" mislabel, this belongs in B. DEIN ZUHAUSE)
 → 1:2019 (WLAN)
 → 1:3067 → 1:3102 → 1:3137 → 1:3172 (Telefon ×4, sequential)
 → 1:1964 → 1:1912 (TV/Internet service check)
 → 1:1854 (OptimiseInternet upsell)
 → 1:1789 (OptimiseTV upsell)
 → 1:1524 (Summary)
 → 1:2466 or 1:2424 (Confirmation — the specific variant reached depends on which
    consent checkboxes are already ticked when leaving Summary)
 → *(originally: 1:2508 scheduling screen → 1:2697 validation-error variant — both removed
    per 2026-10 workshop decision; see Confirmation / Consent section above)*
 → **1:3224 "Landscape DE"** — Customer signature, confirmed via `get_design_context`.
    Landscape-oriented frame (809×360 — device rotated for signing). Copy: "Customer
    signature" / "I hereby confirm that the technical order has been fulfilled and that I
    have been informed about the service provided" + empty signature pad + "Zurück"
    (Back) / "Send report" buttons. **The customer must sign here before the report can be
    sent — "Send report" is the final action on this screen, meaning signature capture is a
    hard gate before report generation, not optional.**
 → 1:1460 (GigaCheck/Send/Success) ✅ confirmed terminal screen
```

**Note:** whether "Send report" is disabled outright until a signature is present, or is
tappable but fails validation, hasn't been confirmed — worth checking directly in Figma or
with the file owner.

**Key corrections to the inferred version above:**
- The **"Booked Products" radio (TV Only / Internet Only / Internet+TV) does not branch the flow** in this prototype — all three Wohnbereich frames play in sequence regardless of selection. If real branching is intended for production, it isn't wired into this prototype and would need to be specified separately.
- **Confirmation originally required both consent checkboxes checked AND a contact-time
  preference (Morning or Afternoon) selected** to proceed, missing the time preference
  routing to a dedicated validation-error screen (`1:2697`) — true of the Figma prototype as
  walked, but the scheduling requirement has since been **removed per the 2026-10 workshop**
  (see Confirmation / Consent above); only the two consent checkboxes remain required.
- The 6 "Confirmation" variants we originally treated as ambiguous states are now understood: some are default/empty, one is the live validation-error state, and which one appears depends on what's already filled in from the previous screen — not a fixed default.
- We did not confirm the `1:1493` (Send/Error) trigger condition — only the success path was walked live.

## Remaining open items
1. **A. DEIN AUFTRAG** — this section's actual screens are still unidentified. (`1:2128`/`1:2091` were previously misattributed here; they're confirmed to be the "Internet" status screen under B. DEIN ZUHAUSE instead — see above. The real order/job-intro screens for this section haven't been located yet.)
2. **Send/Error (`1:1493`) trigger** — not walked; likely a network/API-failure state rather than a user-input branch, worth confirming with the file owner.
3. **VF KDG branded section** — still unconfirmed whether in scope for the conversational redesign, or purely a visual re-skin of the same flow.
4. **Signature gate mechanism** — whether "Send report" on `1:3224` is disabled outright pre-signature or fails validation on tap hasn't been confirmed in Figma.
5. **Possible A. DEIN AUFTRAG match — unverified hypothesis (2026-10 workshop sketch, not a
   confirmed Figma screen):** a hand-drawn workshop sketch shows a question resembling
   "Kannst Du das Anliegen lösen?" (Can you resolve the issue?) with Yes → continue to the
   check, No → reasons (technical work needed / no access / foreign NE4 system / custom
   input) → an "Always On" offer and a message about follow-up steps. This *might* be the
   still-unidentified A. DEIN AUFTRAG intro section (see item 1 above) — but it's inferred
   from a rough sketch, not confirmed Figma screens. Treat as a hypothesis to verify, not a
   confirmed addition to the flow.