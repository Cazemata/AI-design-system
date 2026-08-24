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