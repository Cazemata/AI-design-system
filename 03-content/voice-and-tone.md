# Voice & Tone

## Purpose
Defines how this app sounds in different contexts — technician-facing procedural copy,
customer-facing legal/consent copy, and the conversational agent voice introduced by the
GigaCheck redesign are not the same register, and shouldn't be written as if they were.

## Registers by audience
The confirmed GigaCheck flow (`gigacheck-flow-schema.md`) already contains several distinct
registers, carried forward as-is by the conversational redesign (`conversational-flow.md`)
unless noted:

- **Technician — procedural/checklist**: terse, functional, no persuasion needed (e.g.
  "Test point," "Router - Mandatory"). The technician is a professional completing a task,
  not a customer being sold to.
- **Customer — legal & consent**: formal, first-person declarative, verbatim (e.g. "I hereby
  confirm that the technical order has been fulfilled..."). See Legal & consent copy below —
  this register is never paraphrased.
- **Customer — confirmation/success**: informative, directed at the technician about what to
  tell the customer (e.g. "The report was successfully sent. Please inform the customer...").
- **Sales/upsell** — **not applied in the current flow (confirmed 2026-10).** Benefit-led,
  plain (e.g. "Internet connection can be increased to 1,000 Mbit/s"), distinct from both the
  checklist and legal registers — persuasive but not hype-driven. All sales/upsell content was
  removed from the flow on purpose, so the technician doesn't upset the client with
  sales-related topics — a confirmed product decision, not a pending exclusion. The register
  is documented here for reference; it should not be introduced into technician-facing copy.
  The example above comes from the removed OptimiseInternet screen.
- **Validation/error**: direct and imperative in the source flow (e.g. "Mandatory field
  hasn't been filled!"). The conversational redesign softens this into plain-language
  restatement via `agent-message`'s Validation follow-up variant rather than a generic error
  string — see that component's Variants section.
- **Conversational agent** (new, introduced by this redesign): warm, direct address,
  contractions welcome (e.g. "Let's get started — I'll walk through a few checks with you,"
  "Anything to change?"). This register doesn't exist in the original source flow — it's
  this project's own addition, used only for the agent's own turns (Statement/Question),
  never as a substitute for the legal or upsell registers above.

## Legal & consent copy
Consent and legal declaration copy (the Confirmation section's consent checkboxes, the
Customer Signature declaration) is used **verbatim, never paraphrased or adapted to the
conversational agent register above** — the exact confirmed text lives in
`gigacheck-flow-schema.md` and is the single source for it; this file doesn't restate it.
When this copy renders inside an `agent-message` Statement turn, it still renders exactly as
confirmed, not rewritten into the agent's usual conversational voice.

## Do / Don't
- **Do** match the technician-checklist register for any new mandatory-field Question turns
  — brief, no persuasion.
- **Do** keep the conversational agent register for the agent's own Statement/Question
  framing, never for legal or upsell copy.
- **Don't** paraphrase consent or legal declaration copy into the conversational agent's
  voice, however natural that might read.
- **Don't** invent a new register for validation/error copy — reuse `agent-message`'s
  Validation follow-up pattern.

## Related
- [`terminology.md`](./terminology.md) — German/English term glossary and bilingual copy
  convention
- `gigacheck-flow-schema.md` — authoritative source for all quoted copy referenced above
- `conversational-flow.md` — where these registers are applied across the redesigned flow
- `agent-message.md` — the component carrying the new conversational agent register
