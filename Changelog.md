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

**Source note:** this entire pass is sourced from a stakeholder workshop (hand-written German sticky-note photos), not a new Figma extraction. `gigacheck-flow-schema.md` and `conversational-flow.md` mark every workshop-derived item inline as a confirmed *decision*, distinct from the file's otherwise confirmed *pixel-level screens*.

### Changed
- `gigacheck-flow-schema.md` — added a top-level workshop-provenance note; removed the Morning/Afternoon scheduling question (nodes `1:2508`/`1:2697`) from the Confirmation/Consent section and the confirmed click-path, per the workshop instruction "Vormittags / Nachmittags raus" — kept as a historical record of what Figma originally showed, marked removed rather than deleted outright; labeled the existing consent checkboxes as **BEW (Beratungseinwilligung)** for the first time; added item 5 to Remaining open items — an unverified hypothesis (from a rough workshop sketch, not a confirmed screen) that a "Kannst Du das Anliegen lösen?" triage question might be the still-unidentified A. DEIN AUFTRAG intro section
- `gigacheck-flow-schema.md` — fixed two dangling references to the now-removed scheduling field ("mirroring the scheduling field's behavior" / "like the scheduling field did") in the signature-gate note and Key corrections, caught while verifying the schema and `conversational-flow.md` still agree with each other
- `conversational-flow.md` — removed the scheduling question and its Validation follow-up from Confirmation/Consent, same workshop source; added a "Proposed — not yet settled" note (both there and under Customer Signature) about possibly consolidating BEW onto the Customer Signature screen, hedged per the workshop's own "evtl." wording; added a Decline path to Customer Signature ("Kunde verweigert Unterschrift") and updated the hard-gate language so "Send report" unlocks on signature *or* recorded decline, not signature alone; trimmed Optimization Options to informational-only framing per the workshop's sales-vs-information scope line, flagging that the exact copy still needs review; flagged two open UX questions on the Internet Status screen (bandwidth prominence, whether "Maximum technical available bandwidth" is needed) and a potential conflict between a workshop note ("TV Nutzung - nur wenn kein TV gebucht") and the existing Wohnbereich branching, without guessing a resolution
- `conversational-flow.md` — fixed the same dangling scheduling-field comparison in Customer Signature's "Unconfirmed" bullet, found during the same consistency check

### Added
- `signature-capture.md` — added a Decline affordance (Anatomy) and a Declined state (States table), both marked as workshop-confirmed, not Figma-confirmed; updated Overview, Accessibility, and Do/Don't so Completed and Declined are equally valid ways to satisfy the signature gate
- `chat-composer.md` — updated the Submit (terminal) variant, Anatomy's Send/submit control, and the Related components note so the terminal gate reflects "signature or decline," matching `signature-capture.md`

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