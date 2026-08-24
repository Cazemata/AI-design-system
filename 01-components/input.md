# Input

## Overview
A field for entering and editing free-form text (name, email, notes, search terms). Use Input for user-editable text; use a Button for triggering an action, and a Select/Picker (once documented) when the value must come from a fixed list rather than free text.

## Anatomy
1. Label
2. Container
3. Leading icon (optional)
4. Input text / placeholder
5. Trailing icon (optional — clear button, password visibility toggle)
6. Helper or error text

## Variants
- **Single-line** — default; one line of free text entry.
- **Multiline** — expands vertically for longer text (notes, descriptions); grows up to a capped height, then scrolls internally.
- **Password** — obscures entered characters by default; trailing icon toggles visibility.
- **Search** — leading search icon; trailing clear icon appears once the field is populated.

## States
| State | Visual change |
|---|---|
| Default (empty) | Resting container with placeholder text in `color-text-secondary` |
| Focused | Container outline changes to `color-border-focus`; label floats above the container (see Platform behavior) |
| Filled | Has a value, unfocused; outline returns to `color-border-default`, entered text in `color-text-primary` |
| Read-only | Value visible in `color-text-primary` but not editable; no focus outline on tap |
| Disabled | Container/label/text in `color-action-disabled` / `color-text-disabled`; not tappable |
| Error | Outline in `color-border-critical`; error message shown below in `color-critical` |

## Sizing & spacing
- Minimum height: `touch-target-min-android` (48dp), the default per `CLAUDE.md`. Only branch to `touch-target-min-ios` (44pt) for native iOS builds.
- Internal padding: `spacing-12` horizontal and vertical inside the container.
- Label-to-container gap: `spacing-4`.
- Container-to-helper/error text gap: `spacing-4`.
- Icon-to-text gap: `spacing-8`.
- Multiline default cap: 5 lines before the field becomes internally scrollable; adjust per context.
- Label and input text: `type-body-md`. Helper/error text: `type-body-sm`.

## Platform behavior
Android is the default spec (see [`CLAUDE.md`](../CLAUDE.md)). iOS is documented only where it meaningfully diverges.

- **Android (default)**: Material outlined text field. The label sits inside the outline at rest (placeholder position), then floats above the outline on focus or once filled, animating with `motion-duration-fast` and `motion-ease-standard` (see [`motion.md`](../00-foundations/motion.md)). Focus is indicated by the outline switching to `color-border-focus`.
- **iOS (if different)**: No floating-label animation — the label sits statically above the field at all times. Focus is indicated by the same outline color change, without the label motion.

## Accessibility
- Accessible name: the label must be programmatically associated with the field (not conveyed by placeholder text alone — placeholders disappear on input and are unreliable for screen readers).
- Minimum touch target: `touch-target-min-android` for the field itself and independently for any trailing icon button (password toggle, clear button) — see [`spacing.md`](../00-foundations/spacing.md).
- Contrast: label, input, and placeholder text against the container background must meet 4.5:1 (see [`color.md`](../00-foundations/color.md)); the error outline must also meet the 3:1 non-text contrast minimum against its surrounding background.
- Screen reader behavior: Error state announces the associated error message when the field receives focus or immediately on validation. Disabled fields are announced as disabled and excluded from the input focus order. Read-only fields are announced as read-only (not disabled), so the user understands the value is visible but not editable.

## Do / Don't
- **Do** give every input a visible, persistent label — don't rely on placeholder text as the only label.
- **Do** show the error message inline below the field the instant validation fails, without a fade/delay (see [`motion.md`](../00-foundations/motion.md) — validation errors should appear instantly, not animate in).
- **Don't** use placeholder text to convey formatting requirements that vanish once the user starts typing — put that in helper text instead.
- **Don't** rely on the error outline color alone to convey the error — always pair it with an inline error message.

## Related components
- [`button.md`](./button.md) — inputs are typically submitted via a Button.
- Icon Button (once documented) — the password-visibility toggle and clear icon behave as inline icon buttons and should follow that spec once it exists.
