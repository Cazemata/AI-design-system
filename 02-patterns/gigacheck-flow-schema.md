# GigaCheck Flow Schema

Extracted from Figma file "AI Design System Test" (fileKey: `63HryYbfkIyzath7V25H6q`), page "Page 1", section "GIGA CHECK FORM".

**Context:** A field-technician tool (Vodafone West / VF KDG branded) used during a home service visit for service and product checks: confirming whether the technician could resolve the issue, checking the coverage area and the living area, checking that the customer's products are functional, capturing customer consent and signature, and sending the completion report.

This is a linear multi-step checklist wizard with an editable summary and a confirmation/consent step before submission.

**Non-Figma update notes (2026-10):** entries below may be marked as confirmed by one of two
later passes, neither of which is a new Figma extraction. Both are flagged inline wherever
they occur:
- **2026-10 stakeholder workshop** (hand-written German sticky notes) — confirmed
  *decisions*, not confirmed *pixel-level screens*.
- **2026-10 screenshot pass** — updated screenshots of the current static-form design. These
  *are* screen-level content, but captured from screenshots rather than read from Figma, so
  newly added screens carry no node IDs.

---

## A. DEIN AUFTRAG (Your Order) — intro

**"Could you resolve the issue?"** — **confirmed via 2026-10 screenshot pass** (no Figma node
ID captured). The first screen of the flow. This resolves what was long an unidentified
section: `1:2128`/`1:2091` had been placed here on canvas x-position alone, and are actually
the **"Internet"** status screens under B below.
- Single-select question: **"Could you resolve the issue?"** — `Yes` / `No`
  - `Yes` continues into the check.
  - `No` reveals the two fields below.
- Revealed on `No` — **"Reasons"** (mandatory), multi-select:
  - "Needs further work (NE3 / structural)"
  - "No access / customer not reachable"
  - "Third-party NE4 facility"
- Revealed on `No` — **"Other"**, free-text field with a `0/300` character counter.
- **Not confirmed by this pass:** the earlier workshop sketch for this screen also showed an
  **"Always On" offer** and a **follow-up-steps message** after the reasons. Neither appears
  in the screenshots, and the screenshots don't show what happens after the `No`-path reasons
  are captured (whether the flow ends there or continues). Still open.

## B. DEIN ZUHAUSE (Your Home)

> **Note:** this section now holds a mix of active and superseded entries. For the current
> order of screens, use the **Confirmed current flow** click-path near the end of this file;
> superseded entries are kept here as historical records and are labeled individually.

**~~`GigaCheck` / "Internet"~~ — REMOVED FROM THE CURRENT FLOW (confirmed 2026-10)** —
`1:2128` (empty/error state), `1:2091` (filled/valid state — same screen, not separate
content)
- Title: "Internet"
- Question: **"Internet Status — mandatory"** — checkboxes "Internet is working" / "Internet
  is used"
- Question: **"Booked Bandwidth (Mbit/s) — mandatory"** — numeric input
- Question: **"Maximum technical available bandwidth (Mbit/s) — mandatory"** — numeric input
- `1:2128` shows the empty state with "Mandatory field hasn't been filled!" on all three
  fields; `1:2091` shows the same screen filled in (Internet is working ✓, bandwidth
  "123456"). Both are the same screen at different fill states, not two distinct steps.
- **Superseded — removed from the current flow, confirmed 2026-10.** Replaces the earlier
  "status unconfirmed" marker. Its subject matter (internet working/used, bandwidth) is now
  covered by **"Your products"** below, where bandwidth is read automatically from a speed
  test rather than typed in. Entry retained as a historical record of the original design.

**`GigaCheck/Versorgungsbereich` (Service Area)** — `1:2052`
- Two checkbox questions — **"Test point"** and **"Amplifier"** — each offering:
  - "Tested and working"
  - "Not tested"
- **Confirmed via 2026-10 screenshot pass:** "Handover point" was renamed to **"Test point,"**
  and both questions' options changed from "Checked and values checked" / "Exchanged" to
  **"Tested and working" / "Not tested."** The earlier labels were confirmed via
  `get_design_context` during the original extraction and are superseded here.
- **Flag — screen title naming, not resolved in this pass:** the new screenshots title this
  screen **"Coverage Area,"** while this section header and `terminology.md` both call it
  "Service Area" (and the click-path below uses "Coverage Area"). "Coverage Area" is the
  likely winner, but normalizing it belongs in a separate terminology cleanup.

**`GigaCheck/Wohnbereich` (Living Area)** — `1:2844`, `1:2773`, `1:2920` (variants)
- Radio question: **"Booked Products - Mandatory"**
  - Options: `TV Only` / `Internet Only` / `Internet and TV`
- Followed by three checkbox questions. Option wording below is the **active (non-grayed)
  state, confirmed via 2026-10 screenshot pass**:
  - **"Router - Mandatory"** — "Tested and working" / "Exchanged" / **"Customer uses
    third-party device"** (third option new in this pass)
  - **"Multimedia-Dose - Mandatory"** — "Tested and working" / "Exchanged" / "No
    Multimedia-Dose available" — **third option's wording unconfirmed against the new
    design**: the screenshot cuts it off, so it is carried over from the original extraction
    rather than re-read.
  - **"Connection Cable"** — "Tested and working" / "Exchanged". **New in this pass**; sits
    after Multimedia-Dose and is **not** marked mandatory in the screenshots.
- *Note on option pairs:* Living Area's three questions pair "Tested and working" with
  **"Exchanged,"** while Service Area's two pair it with **"Not tested"** (above). Both are
  confirmed as-is — don't normalize one to the other.
- **Branching, now visible in the static design (confirmed via 2026-10 screenshot pass):**
  selecting `TV Only` grays out **Router** and **Multimedia-Dose** and removes their
  "Mandatory" label; **Connection Cable** stays enabled. This supersedes the earlier
  "*likely determines which later screens are shown*" inference — but note the two are
  different claims: the observed behavior gates *fields on this screen*, whereas the earlier
  inference was about gating *later* TV/Internet/Phone screens, which remains unconfirmed.
  Only the `TV Only` state appears in the screenshots; the `Internet Only` and
  `Internet and TV` states were not captured.
- **Flag — probable mockup inconsistency, not normalized:** in that grayed-out `TV Only`
  state, the disabled Router and Multimedia-Dose options still read the old "Checked and
  values checked" wording, while Connection Cable reads the new "Tested and working." The old
  wording appears *only* in the grayed state. Likely a mockup oversight rather than two real
  option sets — confirm before building, and don't silently normalize it either way.
- **Naming note:** "Living Area," "Booked Products," and "Multimedia-Dose" are the current
  names. An alternative set — "Residential area," "Sought products," "Multimedia outlet" —
  appeared in one source and was **confirmed not current**. Don't introduce it anywhere.

**"Your products"** — **confirmed via 2026-10 screenshot pass** (no Figma node ID captured).
Sits **directly after Living Area** in the confirmed flow.
- A two-column list with headers **"Product"** and **"Functional,"** with a checkbox in each
  column, for four rows: **Internet**, **Phone**, **WLAN**, **TV**.
  - In one screenshot, WLAN is unchecked and its "Functional" box is disabled. That
    *suggests* "Functional" only becomes enabled once the product itself is checked —
    **inferred, not confirmed.** Verify before building.
- Three read-only values, labeled as read automatically from a speed test:
  - **measured bandwidth** — 150 Mbit/s in the example
  - **bandwidth measured on the multimedia outlet** — 1000 Mbit/s in the example
  - **bandwidth on the modem** — 800 Mbit/s in the example, "automatically read via speed test"
  - **Label variance flagged:** the two screenshots word these three labels slightly
    differently; the longer wording is recorded above. Confirm the final labels.

**~~`GigaCheck/WLAN`~~ — REMOVED FROM THE CURRENT FLOW (confirmed 2026-10)** — `1:2019`
- Checkbox question: **"Wi-Fi works"** / **"Wi-Fi is used"**
- Second question with a helper text field (numeric/signal input, exact label unresolved)
- **Superseded — removed from the current flow, confirmed 2026-10.** Replaces the earlier
  "status unconfirmed" marker. WLAN now appears only as a row in **"Your products"** above
  (Product / Functional), not as its own screen. **The signal-strength field was dropped
  intentionally (confirmed 2026-10)**, part of the same decision that removed "Other
  provider" and all sales/upsell content: the technician flow is kept free of sales-related
  topics so the technician doesn't upset the client. No equivalent is needed in "Your
  products." Entry retained as a historical record.

**~~`GigaCheck/Telefon` (Phone)~~ — REMOVED FROM THE CURRENT FLOW (confirmed 2026-10)** —
`1:3067`, `1:3102`, `1:3137`, `1:3172` (4 variants — likely different states/errors)
- Checkbox question: **"Telephone is working"** / **"Telephone is used"** / **"Other provider"**
- **Superseded — removed from the current flow, confirmed 2026-10.** Replaces the earlier
  "status unconfirmed" marker. Phone now appears only as a row in **"Your products"** above
  (Product / Functional), not as its own screen. **The "Other provider" option was dropped
  intentionally (confirmed 2026-10)** — removed so the technician doesn't raise sales-related
  topics with the client, and it needs no equivalent in "Your products." Entry retained as a
  historical record.

## ~~C. OPTIMIZATION OPTIONS (upsell)~~ — SECTION REMOVED FROM THE CURRENT FLOW (confirmed 2026-10)

> All three entries in this section are superseded. The section is retained in full as a
> historical record of the original design; none of it is part of the confirmed current flow.
**`GigaCheck` (Internet check)** — `1:1964`, `1:1912`
- Checkbox question: **"Standard digital is used and TV works"** / **"4K box is used and TV works"** / **"Not in use"**
  - Includes a validation state: *"Mandatory field hasn't been filled!"*
- Second checkbox question: **"Other TV provider"** / **"SAT usage"** / **"Streaming Services"**
- **Superseded — removed from the current flow, confirmed 2026-10.** Replaces the earlier
  "status unconfirmed" marker. TV usage is no longer checked as its own question; TV appears
  only as a row in **"Your products."** Entry retained as a historical record.

**`GigaCheck/OptimiseInternet`** — `1:3608`, `1:3679`, `1:1854` (variants — DE and EN copy present)
- Checkbox list of upsell offers:
  - **"Giga-Kund:in" / "Giga customer"** — helper: *"Internet connection can be increased to 1,000 Mbit/s"*
  - **"Super-WLAN" / "Super-Wi-Fi"** — helper: *"Intelligent reception technology for the router – super smart, super reliable"*
  - **"SuperWLAN-Verstärker" / "Super Wi-Fi Extender"** — helper: *"For strong Wi-Fi throughout the home"*
  - **"Expert Service"** — helper: *"Optimization of Wi-Fi and setup of smartphone, tablet, etc. by technician"*
  - A `.definitionToggle` component toggles copy between "Customer has received / has NOT received a FREE WiFi router" — a conditional micro-copy state, not a separate question.
- **Superseded — removed from the current flow, confirmed 2026-10.** Replaces the earlier
  "status unconfirmed" marker. No upsell/offer content remains in the confirmed flow. Entry
  retained as a historical record — note this was the only confirmed source for the
  `.definitionToggle` component (see `definition-toggle.md`).

**`GigaCheck/OptimiseTV`** — `1:1789`
- Checkbox list of TV product upsells:
  - `GigaTV Cable including HD Premium`
  - `GigaTV Cable`
  - `GigaTV Net`
  - `Audio by Bang & Olufsen`
  - `Extension to several rooms`
  - (list continues beyond metadata depth captured)
- **Superseded — removed from the current flow, confirmed 2026-10.** This resolves the earlier
  "not addressed either way" flag: OptimiseTV is now explicitly confirmed as removed, like the
  rest of this section. Entry retained as a historical record.

## D. SUMMARY
**`GigaCheck/Summary`** — `1:1524`
- Read-only summary card showing entered values (e.g. name "John", phone number, date) followed by **editable sections** echoing every checkbox answer collected earlier (e.g. "Checked and values checked" / "Exchanged" again).
- Each summary section has an edit affordance leading to:
- **Confirmed to persist, contents unreadable (2026-10 screenshot pass):** a Summary screen
  appears in one screenshot (German-language, too small to read), so the step still exists.
  Its updated contents could not be captured. **The mapping above is now provably stale** —
  it echoes field names and option labels this pass renamed ("Test point," "Tested and
  working," Connection Cable, Router's third option) and doesn't account for "Your products."
  Refresh the summary field list against the new names before relying on it.

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

## Confirmed current flow (authoritative, confirmed 2026-10)

This is the current screen sequence. Where an entry above is labeled superseded, it is **not**
in this path.

```
"Could you resolve the issue?"  (section A — Yes continues; No captures Reasons + Other)
 → Coverage Area            (1:2052 — Test point, Amplifier)
 → Living Area              (1:2844 / 1:2773 / 1:2920 — Booked Products, Router,
                             Multimedia-Dose, Connection Cable)
 → Your products            (Product / Functional rows + speed-test readout; no node ID)
 → Summary                  (1:1524)
 → Consent — BEW            (1:2424 / 1:2466 / 1:2634 / 1:2571 — consent checkboxes only,
                             scheduling removed in the workshop pass)
 → Customer signature       (1:3224 "Landscape DE" — sign, or check "Customer waives
                             signature")
 → Send/Success             (1:1460) ✅ terminal screen
```

**Removed from this flow (confirmed 2026-10, entries retained above as historical records):**
the "Internet" status screen (`1:2128`/`1:2091`), WLAN (`1:2019`), Telefon (`1:3067`–`1:3172`),
the TV/Internet usage check (`1:1964`/`1:1912`), OptimiseInternet (`1:3608`/`1:3679`/`1:1854`),
and OptimiseTV (`1:1789`).

**Design principle (confirmed 2026-10):** the technician flow stays free of sales-related
prompts, so the technician doesn't upset the client with sales-related topics. Check any
future addition to this flow against that principle before adding it.

**Still open on this path:** what follows the `No` branch of "Could you resolve the issue?"
(the workshop sketch's "Always On" offer and follow-up message remain unconfirmed, and the
screenshots don't show whether the flow ends or continues there), and Send/Error (`1:1493`),
which stays deferred.

---

## ~~CONFIRMED real click-path~~ — ORIGINAL PROTOTYPE, SUPERSEDED

> Walked live in the prototype, not inferred from canvas. **Superseded by the Confirmed
> current flow above (2026-10)** — retained as a historical record of how the prototype
> behaved. Don't read it as current: it includes screens since removed, and it records the
> Booked Products radio as *not* gating anything, which the current static design contradicts.

```
1:2052 (Versorgungsbereich — Coverage Area: Handover point, Amplifier
    — "Handover point" is the label as walked; renamed to "Test point" per the
    2026-10 screenshot pass, see section B above)
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

**Signature screen updates — confirmed via 2026-10 screenshot pass:**
- The signature-waiver path is a **plain checkbox labeled "Customer waives signature,"**
  placed next to the canvas, with **no confirmation step** before it commits. This supersedes
  the workshop pass's confirm-before-commit description (see `signature-capture.md`).
- The body copy — *"I hereby confirm that the technical order has been fulfilled and that I
  have been informed about the service provided"* — is **re-confirmed as still current.**
- **Don't introduce:** a different body sentence appeared in one screenshot and was confirmed
  **not** current. It is deliberately not recorded here so it can't be picked up later.

**Key corrections to the inferred version above:**
- The **"Booked Products" radio (TV Only / Internet Only / Internet+TV) does not branch the flow** in this prototype — all three Wohnbereich frames play in sequence regardless of selection. If real branching is intended for production, it isn't wired into this prototype and would need to be specified separately.
  - **Superseded in part — the prototype and the current static design now disagree.** The
    2026-10 screenshot pass shows `TV Only` graying out Router and Multimedia-Dose on the
    Living Area screen (see section B above), so the current design *does* gate on this
    radio. The prototype click-path recorded here does not. Treat the prototype as a
    historical record on this point, not current behavior.
- **Confirmation originally required both consent checkboxes checked AND a contact-time
  preference (Morning or Afternoon) selected** to proceed, missing the time preference
  routing to a dedicated validation-error screen (`1:2697`) — true of the Figma prototype as
  walked, but the scheduling requirement has since been **removed per the 2026-10 workshop**
  (see Confirmation / Consent above); only the two consent checkboxes remain required.
- The 6 "Confirmation" variants we originally treated as ambiguous states are now understood: some are default/empty, one is the live validation-error state, and which one appears depends on what's already filled in from the previous screen — not a fixed default.
- We did not confirm the `1:1493` (Send/Error) trigger condition — only the success path was walked live.

## Remaining open items
1. **A. DEIN AUFTRAG — mostly resolved (2026-10 screenshot pass).** The section's first screen
   is now confirmed: **"Could you resolve the issue?"** (Yes/No, with a `No`-path Reasons
   multi-select and an "Other" free-text field) — see section A above. **Residual open:** the
   workshop sketch's "Always On" offer and follow-up-steps message don't appear in the
   screenshots, and what happens after the `No`-path reasons are captured is still unknown.
2. **Send/Error (`1:1493`) trigger** — not walked; likely a network/API-failure state rather than a user-input branch, worth confirming with the file owner.
3. **VF KDG branded section** — still unconfirmed whether in scope for the conversational redesign, or purely a visual re-skin of the same flow.
4. **Signature gate mechanism** — whether "Send report" on `1:3224` is disabled outright pre-signature or fails validation on tap hasn't been confirmed in Figma.
5. **Resolved (2026-10 screenshot pass)** — the workshop sketch that *might* have been the
   A. DEIN AUFTRAG intro is now confirmed as the "Could you resolve the issue?" screen; see
   item 1 above for what's confirmed and what residual remains.
6. **Resolved (confirmed 2026-10)** — the six screens whose status was previously unconfirmed
   (Internet status, WLAN, Telefon, TV/Internet usage check, OptimiseInternet, OptimiseTV) are
   **removed from the current flow**. Entries retained as historical records, labeled
   superseded inline. This also resolves OptimiseTV's earlier "not addressed either way" flag.
7. **"Your products" — position resolved, dependency still open.** Its position is confirmed:
   directly after Living Area (see Confirmed current flow). **Still open:** whether the
   "Functional" column only enables once the matching "Product" box is checked — inferred from
   one screenshot, not confirmed.
10. **Multimedia-Dose third option wording** — "No Multimedia-Dose available" is carried over
    from the original extraction because the screenshot cuts it off. Still unconfirmed against
    the new design.
8. **Speed-test label wording** — the three read-only bandwidth labels are worded slightly
   differently across the two screenshots; the longer wording is recorded. Confirm final copy.
9. **Living Area grayed-state option wording** — in the `TV Only` grayed state, Router and
   Multimedia-Dose show the old "Checked and values checked" wording while the rest of the
   screen uses the new wording. Probable mockup inconsistency; confirm rather than normalize.