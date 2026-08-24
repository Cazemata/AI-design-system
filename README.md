# [App Name] Design System

A mobile-first design system, written and maintained as plain markdown files. Structure is modeled on the Atlassian Design System, adapted for mobile (iOS + Android).

## Structure

| Folder | Contents |
|---|---|
| [`00-foundations/`](./00-foundations) | Color, typography, spacing, iconography, motion, elevation, grid & layout — the tokens everything else is built from |
| [`01-components/`](./01-components) | Individual UI components (button, input, card, etc.), one file each, following [`_template.md`](./01-components/_template.md) |
| [`02-patterns/`](./02-patterns) | Recurring combinations of components solving a specific problem (empty states, onboarding, forms) |
| [`03-content/`](./03-content) | Voice, tone, terminology, and microcopy guidelines |

## How to use this

- **Adding a component?** Copy `01-components/_template.md`, fill it in, reference foundation tokens rather than raw values, and link related components.
- **Adding a pattern?** Reference the components it composes rather than re-describing their specs.
- **Changing a foundation token?** Check which components reference it and update them too.
- See [`CLAUDE.md`](./CLAUDE.md) for the full set of authoring rules this project follows.

## Status

🚧 Early scaffolding — foundations and components are being filled in incrementally.

## Changelog

See [`CHANGELOG.md`](./CHANGELOG.md) for a dated history of additions and changes.