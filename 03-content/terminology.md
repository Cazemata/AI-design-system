# Terminology

## Purpose
A canonical reference for vocabulary used across this app's copy — where a term has a
confirmed German source name, an established English equivalent, or a fixed bilingual
pairing, it's indexed here so copy stays consistent across components and patterns.

## Bilingual (DE/EN) copy convention
**The worked example below is historical.** The only screen confirmed to carry paired German
and English copy variants was OptimiseInternet's upsell offers, and that screen has been
**removed from the flow (confirmed 2026-10)** — so it describes a removed screen, not current
content. No equivalent example exists in the confirmed flow, and none is invented here.

The convention itself still stands for any future bilingual copy: follow the paired DE/EN
format recorded in `gigacheck-flow-schema.md` rather than inventing a new bilingual pattern,
and treat the schema as the single source for those pairs. This file doesn't restate them —
duplicating them here would create two places that could drift out of sync.

## German section/screen name glossary
The confirmed flow uses German section and screen names throughout, most already glossed
inline in `gigacheck-flow-schema.md`'s own section headers. This table is an index for
discoverability, not a second copy of that translation.

**Note on provenance:** every pairing below is sourced from `gigacheck-flow-schema.md` —
that file is the single source of truth for each translation, not this table. If a term's
English form ever changes there, update it here too rather than letting the two drift apart;
this repo has already had one instance of a term disagreeing across files (Wohnbereich's
field names — see `Changelog.md`), and this table exists to be looked up, not to repeat that.

| German term | English equivalent | Where confirmed |
|---|---|---|
| DEIN AUFTRAG | Your Order | `gigacheck-flow-schema.md`, section A — first screen now confirmed ("Could you resolve the issue?") |
| DEIN ZUHAUSE | Your Home | `gigacheck-flow-schema.md`, section B |
| Versorgungsbereich | Service Area | `gigacheck-flow-schema.md`, node `1:2052` |
| Wohnbereich | Living Area | `gigacheck-flow-schema.md`, nodes `1:2844`/`1:2773`/`1:2920` |
| Telefon | Phone | `gigacheck-flow-schema.md`, nodes `1:3067`–`1:3172` — **screen removed from the flow (confirmed 2026-10)**; term retained for the historical entry |
| Zurück | Back | Confirmed button label, node `1:3224` (Customer Signature) |

Also referenced but not a translation pair: **VF KDG** — a client/brand variant named
alongside "Vodafone West" in the schema's context line; not further defined there, and
whether it's in scope for this redesign is still an open item (see
`gigacheck-flow-schema.md`'s Remaining open items). Don't expand or guess what "KDG" stands
for beyond what's confirmed.

## Do / Don't
- **Do** treat this table as an index — look up the actual current pairing in
  `gigacheck-flow-schema.md` before relying on it for anything load-bearing.
- **Do** add a new row here when a new German term is confirmed elsewhere, rather than
  letting it exist only in one file.
- **Don't** let this table and the schema disagree — if you're updating one, check the other.
- **Don't** invent an English equivalent for a term that hasn't been confirmed — flag it as
  unconfirmed instead (see `gigacheck-flow-schema.md`'s Remaining open items for the current
  list).

## Related
- [`voice-and-tone.md`](./voice-and-tone.md) — legal & consent copy handling rule
- `gigacheck-flow-schema.md` — authoritative source for every term above
- `conversational-flow.md` — where these terms appear in the redesigned flow
