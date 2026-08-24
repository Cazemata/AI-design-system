# Grid & Layout

## Purpose
Defines screen-level layout rules — safe areas, margins, and breakpoints — so screens compose predictably across devices.

## Safe areas
- Always respect the OS-reported safe area insets (notch, status bar, home indicator, dynamic island) — never hardcode top/bottom padding for these.
- Content should never render behind the status bar or home indicator; use the platform's safe-area API rather than fixed offsets, since these vary by device.

## Screen margins
| Token | Value | Usage |
|---|---|---|
| margin-screen-default | 16px | Standard left/right screen margin (see [`spacing.md`](./spacing.md)) |
| margin-screen-compact | 12px | Dense screens (settings lists, data-heavy views) |

## Column grid
- Phone: **4-column grid**, 16px gutters, 16px margins.
- Tablet: **8-column grid**, 24px gutters, 24px margins.

## Breakpoints
| Token | Range | Target |
|---|---|---|
| breakpoint-compact | up to 599px width | Phones (portrait) |
| breakpoint-medium | 600–839px width | Phones (landscape), small/split-screen tablets |
| breakpoint-expanded | 840px+ width | Tablets (portrait & landscape), foldables (unfolded) |

## Adaptive layout patterns
- **List/detail**: at `breakpoint-expanded`, show list and detail side by side (e.g. 4-column list / 4-column detail on the 8-column grid) instead of the phone's single-screen push/pop navigation.
- **Multi-column content**: grids of cards should add columns at wider breakpoints (e.g. 1 column at compact → 2 at medium → 3–4 at expanded) rather than stretching card width indefinitely.
- **Navigation**: bottom tab bars (phone) commonly shift to a side/rail navigation at `breakpoint-expanded` — confirm per-app rather than assuming universally.
- **Don't** simply scale up phone layouts — re-flow using the column grid at each breakpoint.

## Usage guidelines
- Default to single-column, full-width layouts at `breakpoint-compact`.
- At `breakpoint-medium`+, consider two-column layouts for list/detail patterns rather than simply stretching phone layouts wider.
- Maintain consistent screen margins (`margin-screen-default` / tablet's 24px margin) across all breakpoints unless a component explicitly bleeds to the edge (e.g. full-width imagery).
- Test orientation changes (portrait ↔ landscape) at tablet sizes — layout should reflow at the breakpoint, not just stretch.

## Platform behavior
- **iOS**: use `UILayoutGuide`/safe area layout guides; account for the home indicator inset on bottom-anchored elements (tab bars, sticky buttons).
- **Android**: use `WindowInsets` for system bars and gesture navigation; account for gesture nav bar inset on bottom-anchored elements.

## Accessibility
- Layouts must reflow (not clip or overlap) at the largest supported OS text-scaling setting — see [`typography.md`](./typography.md).
- Maintain minimum touch target spacing at every breakpoint (see [`spacing.md`](./spacing.md)).

## Do / Don't
- **Do** use safe-area APIs instead of fixed pixel offsets for top/bottom insets.
- **Do** reference `margin-screen-default` for standard screen padding.
- **Don't** hardcode layout values that differ from the tokens above without a documented reason.

## Related
- [`spacing.md`](./spacing.md) — spacing scale and touch targets
- [`typography.md`](./typography.md) — text reflow at large accessibility sizes