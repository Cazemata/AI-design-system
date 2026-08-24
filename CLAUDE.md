# Design System — Project Instructions for Claude

## What this project is

A mobile app design system, written and maintained manually as `.md` files (no build tooling, no token-generation scripts — plain markdown is the source of truth). The structure is modeled on the Atlassian Design System, adapted for mobile.

## Folder structure

```
design-system/
├── 00-foundations/     # color, typography, spacing, iconography, motion, elevation, grid-layout
├── 01-components/      # one file per component (button.md, input.md, card.md, etc.)
│   └── _template.md    # canonical component template — copy this for every new component
├── 02-patterns/        # recurring combinations of components (empty-states.md, onboarding.md, forms.md, etc.)
├── 03-content/         # voice-and-tone.md, terminology.md, microcopy-guidelines.md
├── README.md           # index / table of contents
└── CHANGELOG.md        # dated log of additions and changes
```

## Content rules

- **Every component file follows `01-components/_template.md`.** Sections, in order: Overview, Anatomy, Variants, States, Sizing & spacing, Platform behavior, Accessibility, Do/Don't, Related components. Don't add or remove sections without updating the template first.
- **Foundations are the source of truth for tokens.** Components should reference foundation tokens (e.g. `color-action-primary`, `spacing-16`) rather than hardcoding raw values. When drafting or editing a component, check `00-foundations/` for the correct token names before inventing new ones.
- **Patterns compose components — they don't duplicate specs.** A pattern file describes when/how components are combined and links to the component files involved, rather than re-describing each component's states or sizing.
- **Cross-link aggressively.** Component files should link back to the foundation tokens they use. Pattern files should link to the components they compose. When you create or edit a file, add/update the relevant links in both directions.
- **Mobile-specific, not web-specific.** Always account for: touch target minimums (44pt iOS / 48dp Android), safe areas, platform differences (iOS vs Android), and how components behave under OS-level text scaling (Dynamic Type / font scaling).
- **Keep it lean.** Prefer GOV.UK-level brevity over Material Design's exhaustive depth — cover the same categories, but don't over-document.

## Workflow expectations

- When asked to draft a new component, use `01-components/_template.md` as the structural base and match the tone/detail level of existing component files (e.g. `button.md`) rather than starting from a blank format.
- When adding or changing a token in `00-foundations/`, check whether any existing component files reference it and flag ones that may need updates.
- After creating or substantively editing a file, add a dated entry to `CHANGELOG.md`.
- Show a diff/plan before writing to any file — don't silently overwrite existing component or foundation docs.

## Platform priority

**Android-first.** When a component or pattern needs a primary spec (sizing, motion, iconography style), default to Android/Material conventions first, then note iOS deviations explicitly rather than documenting both as equal defaults. Touch target minimums, spacing, and elevation values should be sized to Android's 48dp baseline by default; call out iOS's 44pt only where it actually differs in practice.

## Not yet decided / ask before assuming

- Whether tablet/adaptive layout is in scope (affects `grid-layout.md` and any responsive components). — **Resolved: in scope.** See `00-foundations/grid-layout.md`.