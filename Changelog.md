# Changelog

All notable additions and changes to this design system are logged here, most recent first.

## [Unreleased]

### Added
- Initial project scaffolding: folder structure for foundations, components, patterns, and content
- `CLAUDE.md` authoring rules and project instructions
- `README.md` index

## 2026-07-30

### Added
- `button.md` component (variants, states, sizing, accessibility, Android-default platform behavior with iOS deviations noted)
- `input.md` component (single-line, multiline, password, search variants; states, sizing, accessibility, Android-default platform behavior with iOS deviations noted)
- `agent-message.md`, `option-card.md`, `chat-composer.md`, `progress-indicator.md` components and `conversational-flow.md` pattern — conversational UI components and the flow-mapping pattern for the GigaCheck redesign

### Changed
- `color.md` — added `color-border-critical` token (Border section); there was no border color for error/invalid states, only `color-critical` for text/icons, which `input.md`'s Error state needed
- `_template.md` — States table rows are now marked as illustrative rather than fixed, and "Filled / populated" and "Read-only" rows were added; the original row set (Pressed, Focused, Disabled, Loading, Error) was Button-shaped and had no natural place for states that don't involve pressing, which `input.md` needed
- `agent-message.md`, `option-card.md`, `chat-composer.md`, `progress-indicator.md`, `conversational-flow.md` — audit fix pass: restored `type-`/`color-` token prefixes (e.g. `body-md` → `type-body-md`), corrected `motion-default` to `motion-duration-default` paired with the appropriate `motion-ease-*` token, replaced loose color prose ("a red border," "Feedback/error background tint," etc.) with exact `color.md` token names, flagged the nonexistent corner-radius token in `agent-message.md` as an unresolved gap instead of citing a token that doesn't exist, replaced `elevation`-token padding claim in `progress-indicator.md` with the correct `spacing-8` token, made `progress-indicator.md`'s Related list bidirectional with `chat-composer`, switched headings to Title Case, added a "Visual change" column to all four States tables, restored the full Android/iOS framing sentence in Platform behavior sections, replaced `aria-live="polite"` with platform-native live-region references per CLAUDE.md's mobile-specific rule, and added an explicit note in `conversational-flow.md` flagging the missing lettered "E" section between D. SUMMARY and F. FEEDBACK
- `conversational-flow.md` — second decision-review pass: removed lettered section-header framing (A/B/C/D/F) in favor of plain descriptive headers, with original letters kept parenthetically for provenance; moved the reassigned Internet Status screen (`1:2128`/`1:2091`, confirmed via Figma to be one screen in two states) out of the still-unidentified Introduction section and into Home & Connectivity Check with its three confirmed fields; marked the Wohnbereich single-select as an intentionally branching, confirmed deviation from the original's sequential playback (flagged as such for future parity comparisons); confirmed the inline Send/Success treatment as final (removed the prior open-hypothesis language); marked Send/Error handling as deferred to a separate pass; and walked back the Customer Signature "Send report" disable behavior from a confirmed hard gate to an explicitly unconfirmed item (disable-outright vs. fail-on-tap), per updated guidance

### Added (2026-07-30, cont'd — schema file)
- `gigacheck-flow-schema.md` added to `02-patterns/` — the authoritative Figma-derived source document that `conversational-flow.md` was always meant to reference but that hadn't actually been created in this project until now

### Changed (2026-07-30, cont'd — schema reconciliation)
- Relocated `conversational-flow.md` from `01-components/` to `02-patterns/`, matching its own "Pattern:" framing and resolving a mismatch flagged across three separate review passes
- Re-verified `conversational-flow.md`'s Internet Status and Customer Signature content against the actual `gigacheck-flow-schema.md` (rather than a paraphrase) and corrected two node-reference omissions: the Wohnbereich citation now reads `1:2844`→`1:2773`→`1:2920` (was missing the middle variant), and Telefon now reads `1:3067`→`1:3102`→`1:3137`→`1:3172` (was missing two of four variants)
- Corrected the Customer Signature wording: the schema confirms the customer *must* sign before the report can be sent (a settled requirement), while only the enforcement *mechanism* (disable-outright vs. fail-on-tap) is unconfirmed — the previous edit had collapsed both into a single "unconfirmed" claim, understating what's actually settled

### Fixed (2026-07-30, cont'd — cross-file gap closure)
- `conversational-flow.md` — "Booked Products" now reads "Booked Products - Mandatory," matching the schema's exact wording
- `gigacheck-flow-schema.md` — backfilled confirmed field names into the Versorgungsbereich (Service Area) and Wohnbereich (Living Area) entries, which previously described only the generic "Checked and values checked" / "Exchanged" checkbox pattern without naming the actual fields; the real names ("Handover point" / "Amplifier" for Service Area, "Router" / "Multimedia-Dose" for Wohnbereich, the latter both mandatory with "Multimedia-Dose" carrying a third "No Multimedia-Dose available" option) had only appeared in the file's own "CONFIRMED real click-path" section, so the file disagreed with itself
- `conversational-flow.md`'s Living Area bullet updated to match: added the "Mandatory" labels and the "No Multimedia-Dose available" third option; Coverage Area was already correct and needed no change

### Added (2026-07-30, cont'd — four new components)
- `checkbox-radio.md` — the base Checkbox (multi-select) / Radio (single-select) control that `option-card.md` already assumed existed; flags that no dedicated control-size or corner-radius token exists yet in `00-foundations/`, using `icon-size-md` as the nearest existing stand-in for size
- `signature-capture.md` — the signature pad widget referenced by `chat-composer.md` and `conversational-flow.md`, built from the confirmed node `1:3224` ("Landscape DE," 809×360); documents the hard-gate rule explicitly (paired `chat-composer` Submit control must stay disabled until this component reports a Completed signature) and flags the lack of an accessible alternative to freehand signing as an unresolved, unsolved gap rather than a false fix; signature-only, no photo/camera capture
- `top-navigation.md` — the fixed status-bar-plus-header component `progress-indicator.md` already referenced as an anchor point; flags two real foundations gaps found while drafting — no brand/header background color token distinct from the error-semantic `color-critical`, and no dedicated app-bar/header-height token
- `definition-toggle.md` — the inline expandable-copy component backing `option-card.md`'s Upsell offer card variant; documents an unresolved discrepancy between the confirmed schema (describes `.definitionToggle` as an account-driven conditional copy swap, not user-toggled) and `option-card.md`'s existing description (a user-tap expand/collapse) as two separate variants rather than silently picking one

### Changed (2026-07-30, cont'd — cross-linking for the four new components)
- `option-card.md` — Anatomy's Selection indicator now references `checkbox-radio` by name instead of the previous vague "existing Checkbox/Radio tokens from the base design system" (no such component existed until now); Related components list now includes `checkbox-radio` and `definition-toggle`
- `chat-composer.md` — Related components list now includes `signature-capture`
- `progress-indicator.md` — the bare "Top navigation" mention in Sizing & spacing is now a real cross-link to `top-navigation`; Related components list now includes `top-navigation`

### Added (2026-07-30, cont'd — foundations gap-filling)
- `spacing.md` — added a Corner radius scale (`radius-sm`/`radius-md`/`radius-lg`/`radius-full`) and a Component sizing section (`control-size-md`, `header-height-default`); this is the second time the missing radius scale had blocked a component (`agent-message.md`, then `checkbox-radio.md`), so it's now fixed at the foundation level instead of per-component. **Provenance note**: no radius, control-size, or header-height measurement had ever been captured from the source Figma file for any of these — verified by searching the whole project, including `gigacheck-flow-schema.md` — and this session has no Figma/`get_design_context` tool access, so these are considered first-pass defaults (same base-4 logic as the existing spacing scale; `header-height-default` matches Android Material's standard 56dp app bar per the platform-priority default in `CLAUDE.md`), not Figma-verified values. Flagged for confirmation against the real file.
- `color.md` — added a Brand section with `color-surface-brand`, mapped to the existing `red-500` primitive as a placeholder (no hex was ever captured for the header's actual brand red either) — distinct from `color-critical` so a persistent brand header no longer has to reuse an error-semantic token

### Changed (2026-07-30, cont'd — reference the new foundation tokens)
- `agent-message.md` — corner radius now references `radius-md` instead of the previous unresolved-gap note
- `checkbox-radio.md` — control size now references `control-size-md`, corner radius now references `radius-sm`, both replacing previous unresolved-gap notes
- `top-navigation.md` — header background and height now reference `color-surface-brand` and `header-height-default` instead of previous unresolved-gap notes; Do/Don't updated to match

### Fixed (2026-07-30, cont'd — remove leftover photo-capture language)
- `chat-composer.md` — Anatomy's "camera/signature icon" / "photo or signature" and Variants' "camera or signature pad" reworded to signature-only, referencing `signature-capture` by name; photo capture was never part of the confirmed flow

### Changed (2026-07-30, cont'd — surface the .definitionToggle open question in the pattern doc)
- `conversational-flow.md` — added a note under OptimiseInternet flagging the `.definitionToggle` Conditional-vs-Expandable ambiguity and pointing to `definition-toggle.md`, so the open question is visible from the pattern doc, not just buried in the component file. Not resolved — still needs a decision.

### Added (2026-07-30, cont'd — 03-content population)
- `voice-and-tone.md` — Purpose, a "Registers by audience" breakdown of the six distinct registers already implicit in the confirmed schema copy plus the redesign's own new conversational-agent register, the relocated legal & consent "verbatim, not paraphrased" rule, Do/Don't, Related
- `terminology.md` — Purpose, the DE/EN bilingual copy convention (stated as a principle, not a restatement of the OptimiseInternet pairs), a German section/screen name glossary table, and a VF KDG entry that explicitly declines to guess what "KDG" stands for since it was never confirmed

### Changed (2026-07-30, cont'd — relocate embedded content guidance out of conversational-flow.md)
- `conversational-flow.md` — Confirmation/Consent's inline "copy is not to be paraphrased" rule replaced with a cross-link to `voice-and-tone.md`'s Legal & consent copy section; Customer Signature's inline "Zurück (Back)" gloss replaced with a cross-link to `terminology.md` (only "Zurück" is glossed — "Send report" was already English and didn't need one); added a short pointer paragraph after the Overview directing readers to `terminology.md` and `voice-and-tone.md`; Related section now includes both. `microcopy-guidelines.md`, `error-handling.md`, and `loading-states.md` were left empty — nothing in scope for the first, and no cross-component sequencing logic found for the other two that wasn't already covered by an individual component's States table (agent-message's Validation follow-up/Streaming, chat-composer's Loading/Error, option-card's Error)

**Second-source-of-truth note**: `terminology.md`'s glossary table deliberately does *not* duplicate the German/English pairings already inline in `gigacheck-flow-schema.md`'s own section headers — it's built as an index with a provenance note naming the schema as the single source of truth per entry, styled after `spacing.md`'s corner-radius provenance note, specifically to avoid recreating the Wohnbereich-style drift this repo has already hit once.

### Changed (2026-07-30, cont'd — dual delivery on report send)
- `conversational-flow.md` — Feedback section: added a "Dual delivery on send" bullet between Send/Success and Send/Error documenting that "Send report" triggers both the MeinVodafone-Portal outcome and a PDF-by-email to the customer, confirmed directly with the product owner — **not sourced from `gigacheck-flow-schema.md`**, which only documents the portal outcome; the schema's own header states it's a Figma extraction, and this requirement isn't from Figma, so `gigacheck-flow-schema.md` was intentionally left unedited. Also added an open question under Send/Error about whether it needs to distinguish which delivery channel failed, not resolved.

## 2026-10-05

Two distinct non-Figma passes landed on this date. They are logged separately below because they carry different kinds of confirmation and, in two places, the later one supersedes the earlier.

---

### Pass 1 — stakeholder workshop notes

**Source note:** sourced from a stakeholder workshop (hand-written German sticky-note photos), not a new Figma extraction. `gigacheck-flow-schema.md` and `conversational-flow.md` mark every workshop-derived item inline as a confirmed *decision*, distinct from the file's otherwise confirmed *pixel-level screens*.

### Changed
- `gigacheck-flow-schema.md` — added a top-level workshop-provenance note; removed the Morning/Afternoon scheduling question (nodes `1:2508`/`1:2697`) from the Confirmation/Consent section and the confirmed click-path, per the workshop instruction "Vormittags / Nachmittags raus" — kept as a historical record of what Figma originally showed, marked removed rather than deleted outright; labeled the existing consent checkboxes as **BEW (Beratungseinwilligung)** for the first time; added item 5 to Remaining open items — an unverified hypothesis (from a rough workshop sketch, not a confirmed screen) that a "Kannst Du das Anliegen lösen?" triage question might be the still-unidentified A. DEIN AUFTRAG intro section
- `gigacheck-flow-schema.md` — fixed two dangling references to the now-removed scheduling field ("mirroring the scheduling field's behavior" / "like the scheduling field did") in the signature-gate note and Key corrections, caught while verifying the schema and `conversational-flow.md` still agree with each other
- `conversational-flow.md` — removed the scheduling question and its Validation follow-up from Confirmation/Consent, same workshop source; added a "Proposed — not yet settled" note (both there and under Customer Signature) about possibly consolidating BEW onto the Customer Signature screen, hedged per the workshop's own "evtl." wording; added a Decline path to Customer Signature ("Kunde verweigert Unterschrift") and updated the hard-gate language so "Send report" unlocks on signature *or* recorded decline, not signature alone; trimmed Optimization Options to informational-only framing per the workshop's sales-vs-information scope line, flagging that the exact copy still needs review; flagged two open UX questions on the Internet Status screen (bandwidth prominence, whether "Maximum technical available bandwidth" is needed) and a potential conflict between a workshop note ("TV Nutzung - nur wenn kein TV gebucht") and the existing Wohnbereich branching, without guessing a resolution
- `conversational-flow.md` — fixed the same dangling scheduling-field comparison in Customer Signature's "Unconfirmed" bullet, found during the same consistency check

### Added
- `signature-capture.md` — added a Decline affordance (Anatomy) and a Declined state (States table), both marked as workshop-confirmed, not Figma-confirmed; updated Overview, Accessibility, and Do/Don't so Completed and Declined are equally valid ways to satisfy the signature gate
- `chat-composer.md` — updated the Submit (terminal) variant, Anatomy's Send/submit control, and the Related components note so the terminal gate reflects "signature or decline," matching `signature-capture.md`

---

### Pass 2 — 2026-10 screenshot pass

**Source note:** sourced from updated screenshots of the current **static-form** design system (the same style as the original Figma extraction), not conversational mockups and not a new Figma read. These are screen-level content, so they're stronger than the workshop pass's decisions — but captured from images, so newly added screens carry **no node IDs**. Content was documented in `gigacheck-flow-schema.md` as static screen/field descriptions, then separately re-expressed in `conversational-flow.md` as agent-led turns rather than copied across as UI labels. Every item is marked "confirmed via 2026-10 screenshot pass" inline.

**Supersedes the workshop pass in two places:** the signature decline mechanism (now a plain "Customer waives signature" checkbox with no confirmation step), and the Wohnbereich branching, which the static design now shows directly rather than it being our own deviation.

#### Added
- `gigacheck-flow-schema.md` — new **"Could you resolve the issue?"** intro screen (Yes/No, with a `No`-path mandatory "Reasons" multi-select and an "Other" free-text field with a `0/300` counter), closing the long-open A. DEIN AUFTRAG item; new **"Your products"** screen (two-column Product/Functional list for Internet/Phone/WLAN/TV, plus three read-only speed-test bandwidth values); new **"Connection Cable"** field in Living Area
- `conversational-flow.md` — Introduction section now maps the intro screen as a single-select Question turn plus `No`-path Reasons and "Other" turns, with a translation note on why inline *reveals* become turns that only appear after `No`; new **"Your products"** section documenting why it deliberately mixes a Question turn (product/functional checks are real input) with an `agent-message` Statement readout (speed-test values are measured, not entered, so there is nothing to ask)

#### Changed
- `gigacheck-flow-schema.md` — "Handover point" → **"Test point"**; Service Area options → "Tested and working" / "Not tested"; Living Area's Router and Multimedia-Dose options → "Tested and working" / "Exchanged" with Router gaining **"Customer uses third-party device"**; Living Area branching recorded as observed in the static design (TV Only grays Router and Multimedia-Dose, drops their Mandatory label, leaves Connection Cable enabled); signature body copy re-confirmed as current, with a don't-introduce guard for the non-current alternative sentence; provenance note at the top of the file extended to describe both non-Figma passes
- `conversational-flow.md` — Coverage Area, Living Area, and Customer Signature remapped to the new labels and options; the branching paragraph's "deliberate improvement, not a like-for-like carryover" framing **softened** — the gating is now corroborated by the static design, so only the *mechanism* (skip the turn vs. show it grayed) remains our translation; decline → **waiver** wording throughout
- `signature-capture.md` — Decline affordance → **Waiver checkbox** ("Customer waives signature", no confirmation step, delegated to `checkbox-radio`'s Checkbox variant); `Declined` state renamed **`Waived`**; the "confirm before accidental tap" Do/Don't replaced with a don't-add-a-confirmation-step line that notes the accidental-check risk is real but unmitigated in the current design; Accessibility updated to checkbox semantics; `checkbox-radio` added to Related components
- `chat-composer.md` — terminal Submit gate, Anatomy's Send/submit control, and Related components updated from "decline" to "waiver"
- `top-navigation.md` — Title anatomy item now records the confirmed header copy **"Service and Product Check"** (previously a generic placeholder), with an explicit note that this is the header title only: the project name, file names, and Figma node paths intentionally keep the GigaCheck name
- `progress-indicator.md` — Anatomy's section-label list and the Do/Don't reference to "the original A–F structure" now use the same plain descriptive section names as `conversational-flow.md`, since lettering was dropped as a confirmed decision; no new section names invented, nothing else in the file touched

#### Flagged, not resolved
- `gigacheck-flow-schema.md` — five screens (Internet status, WLAN, Telefon, OptimiseInternet, TV/Internet usage check) marked **"status unconfirmed after 2026-10 screenshot pass"**: absent from the screenshots, with removal vs. folded-into-"Your products" vs. simply-not-captured undetermined. Entries deliberately retained, not deleted. **OptimiseTV** marked "not addressed either way" — it was neither shown nor named as missing
- `conversational-flow.md` — the workshop pass's informational-only trim of Optimization Options marked **possibly superseded, pending confirmation**, with an explicit "don't apply both versions" instruction, since "Your products" may replace that section outright
- Both pattern files — Summary step confirmed to persist (visible but unreadable in one screenshot) and its **recap mapping flagged as stale** against this pass's renames; Living Area's grayed-state option wording flagged as a probable mockup inconsistency (old wording survives only there) and deliberately **not normalized**; Multimedia-Dose's third option wording flagged unconfirmed (cut off in the screenshot); the three speed-test labels flagged for wording variance between screenshots; the intro screen's "Always On" offer and follow-up message from the workshop sketch flagged as still unconfirmed; the Coverage Area / Service Area screen-title conflict flagged for a separate terminology cleanup
- `gigacheck-flow-schema.md` — Key corrections now records that the **prototype click-path and the current static design disagree** on whether the Booked Products radio gates anything; the click-path's "Handover point" label annotated as the label *as walked*, not current

#### Follow-up (2026-10-05) — flow confirmed, screenshot-pass open items resolved

**Confirmed sequence:** "Could you resolve the issue?" → Coverage Area → Living Area → Your products → Summary → Consent (BEW) → Customer signature → Send/Success. Six screens are confirmed **removed** from the flow: the Internet status screen, WLAN, Telefon, the TV/Internet usage check, OptimiseInternet, and OptimiseTV.

- `gigacheck-flow-schema.md` — the six removed entries changed from "status unconfirmed" to **removed from the current flow, confirmed 2026-10**, each retained as a historical record with a strikethrough header and a note on where its content went (or that it appears dropped rather than relocated — Telefon's "Other provider" option and WLAN's signal-strength field both flagged that way). Section C's header marked section-wide superseded. **"Your products" moved to directly after Living Area**, replacing its earlier end-of-section placement. New **Confirmed current flow** click-path added as authoritative, with the prototype click-path retained below it labeled "original prototype, superseded." Open items 6 and 7 resolved (removals confirmed; "Your products" position confirmed), OptimiseTV's "not addressed either way" flag resolved, and a new item added for the still-unconfirmed Multimedia-Dose third-option wording.
- `conversational-flow.md` — active mapping **reordered to the confirmed sequence** with a flow-order note at the top; Internet Status, WLAN, Telefon, and the whole Optimization Options section removed from the active mapping and recorded in a new **Removed from the flow** section, one short note each. The workshop pass's "trim upsells to informational-only" instruction **removed as moot** (no upsell content remains to trim) rather than left standing. The "TV Nutzung - nur wenn kein TV gebucht" conflict flag **resolved by removal**. The two "proposed, not yet settled" BEW-consolidation notes replaced with **"not adopted — BEW stays separate,"** since the confirmed flow keeps Consent as its own step between Summary and Customer signature. Summary recap **rescoped** to what the flow now collects (resolve-the-issue answer and reasons, Coverage Area, Living Area including Connection Cable, Your products with the speed-test readout), with field-level wording still pending a readable Summary screen. Also fixed a dangling pointer the restructure created: the Introduction section had still directed readers to Internet Status "under Home & Connectivity Check below."
- `progress-indicator.md` — section list updated to the confirmed sequence using plain headers (Introduction, Coverage Area, Living Area, Your products, Summary, Consent (BEW), Customer Signature, Feedback); Optimization Options dropped as a section.

#### Flagged, not resolved (follow-up)
- `definition-toggle.md` — flagged as having **no current use in the flow**: its only confirmed source (OptimiseInternet) is removed, which also makes its Conditional-vs-Expandable ambiguity moot for this flow. Component **retained, not deleted**; keep/park/retire left as a component-set decision.
- `option-card.md` — the **Upsell offer card variant** flagged as having no source in the current flow. **Retained, not deleted.**
- Resolved-by-removal notes recorded where the questions used to live: the "show the booked bandwidth more prominently" and "is Maximum technical available bandwidth a field anyone needs" workshop questions both die with the Internet Status screen.
- Unchanged by design: Send/Error stays deferred, the "Your products" Functional-column enablement stays flagged as inferred, and the Multimedia-Dose third-option wording stays unconfirmed. The `No`-path tail of "Could you resolve the issue?" ("Always On" offer, follow-up message) also stays unconfirmed — the confirmed sequence covers the Yes path, and nothing in it addressed that branch.

#### Follow-up (2026-10-05) — removal fallout cleaned up

**Confirmed rationale recorded:** Telefon's "Other provider" option, WLAN's signal-strength field, and all sales/upsell content were removed **on purpose**, so the technician doesn't upset the client with sales-related topics. This is a confirmed product decision — the files no longer describe any of it as a gap, an unfilled slot, or a pending exclusion.

- `gigacheck-flow-schema.md` — **Context line rewritten**: "offer optimization upsells" removed, and the tool's purpose now describes only what the confirmed flow contains (issue resolution, coverage-area and living-area checks, product functionality, consent, signature, sending the report). Telefon's "Other provider" and WLAN's signal-strength field recorded as **intentionally dropped, confirmed 2026-10**, each with the rationale and an explicit "needs no equivalent in Your products" — replacing the earlier "may have been dropped rather than relocated" hedges. **Design principle** added at the removal list: the technician flow stays free of sales-related prompts, and future additions should be checked against that.
- `conversational-flow.md` — the two "appears dropped rather than relocated" observations in **Removed from the flow** rewritten as deliberate removals needing no replacement; the same **design principle** sentence added at the top of that section. Nothing added to "Your products" for the dropped fields.
- `voice-and-tone.md` — the **Sales/upsell register and its Do/Don't lines kept**, but the register is now marked **"not applied in the current flow (confirmed 2026-10)"** with the rationale, explicitly not framed as temporary, and its example noted as coming from the removed OptimiseInternet screen. The technician-register examples ("Internet Status — mandatory," "Booked Bandwidth (Mbit/s)" — both from removed screens) replaced with **"Test point"** and **"Router - Mandatory"**, taken verbatim from the schema's surviving Coverage Area and Living Area entries. No example gap needed flagging: both replacements exist in the schema, and one preserves the original's mandatory-marker point.
- `terminology.md` — the **DE/EN bilingual copy convention kept**, with its OptimiseInternet worked example marked historical and from a removed screen; no replacement example invented, and the absence of one in the confirmed flow stated outright. `Telefon | Phone` row annotated as a removed screen with the term retained for the historical entry. Also corrected the `DEIN AUFTRAG` row, which still read "real screens still unidentified" — section A's first screen is confirmed.
- `option-card.md` — four sourceless mentions annotated **"no source in the current flow"**: the leading-icon OptimiseInternet example, the upsell/offer helper-text description, the Disabled-state "upsell already active" example, and the `definition-toggle` cross-link. The Upsell offer card variant and all links **retained, not removed**.
- `definition-toggle.md` — Overview's closing line, which still told the reader to "confirm which is intended for OptimiseInternet," annotated **"no source in the current flow"**: there is no OptimiseInternet implementation left to confirm against, and the Conditional-vs-Expandable question would only need settling if the component is adopted somewhere new.
- `progress-indicator.md` — Accessibility announcement example changed from "Now on: Optimization Options" (a removed section) to **"Now on: Your products"**.

**Verified:** a repo-wide search for gap-language ("may have been dropped," "rather than relocated," "no equivalent," "still unidentified," "optimization upsells") returns no stale hits; the three remaining matches are the intended new wording and one unrelated use about the branching mechanism.

<!--
Entry format:

## 2026-08-01

### Added
- `button.md` component (variants, states, sizing, accessibility)

### Changed
- Updated `color.md` — added dark mode token variants

### Fixed
- Corrected touch target minimum in `spacing.md` (44pt, not 40pt)
-->