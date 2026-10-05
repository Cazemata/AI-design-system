# Progress Indicator

## Overview
A persistent, low-emphasis indicator of how far through the GigaCheck flow the technician is.
Replaces the static top progress bar (the red-fill segment under the screen title on every
original screen) — same underlying idea, adapted to a conversation where "one screen" no
longer maps to "one step," since a single original screen might now be 2-3 conversational
turns, and vice versa.

## Anatomy
1. **Track** — thin horizontal bar, same visual weight as the original.
2. **Fill** — proportional to section progress, not raw turn count (raw turn count would
   jitter unpredictably as validation follow-ups add turns).
3. **Section label** (optional, on tap/expand) — surfaces the flow's section names as a
   lightweight overlay, using the same plain descriptive headers as `conversational-flow.md`,
   in confirmed flow order: Introduction, Coverage Area, Living Area, Your products, Summary,
   Consent (BEW), Customer Signature, Feedback. Lettered names were dropped as a confirmed
   decision, so they aren't surfaced here either. (Optimization Options was removed from the
   flow in 2026-10 and is no longer a section.)

## Variants
- **Inline (default)** — thin bar pinned below the top nav, always visible, matching original
  placement.
- **Expanded** — tap-to-reveal section breakdown, useful for a technician who wants to jump
  back to a specific section rather than stepping back one conversational turn at a time.

## States
| State | Visual change | Description |
|---|---|---|
| Default | Fill occupies the proportion of the track matching current section progress | Reflects current section progress |
| Updating | Fill animates to its new width using `motion-duration-default` / `motion-ease-standard` | Fires only when advancing between sections, not on every single turn — turn-level advancement should feel conversational, not like a loading bar ticking |

## Sizing & spacing
- Height: 8px (unchanged from original spec). Surrounding padding: `spacing-8` above and below
  the track.
- Pinned below `top-navigation`, above the conversation thread's scrollable area.

## Platform behavior
Android is the default spec (see [`CLAUDE.md`](../CLAUDE.md)). iOS is documented only where it
meaningfully diverges.

- **Android (default)**: Thin bar / fill pattern as described above.
- **iOS (if different)**: No deviation currently scoped.

## Accessibility
- Announce section changes ("Now on: Your products") using the platform's native
  live-region announcement (TalkBack's `AccessibilityLiveRegion` on Android, VoiceOver's
  announcement API on iOS), not a web ARIA attribute, when the fill updates at a section
  boundary — don't announce on every conversational turn, which would be noisy.
- Expanded section list must be fully keyboard/switch-navigable, since it's the primary way
  to jump backward in a flow that otherwise has no persistent multi-step form to scan visually.

## Do / Don't
- **Do** tie progress to section boundaries (the descriptive sections listed in Anatomy,
  matching `conversational-flow.md`), not to conversational turn count, which will vary based
  on validation retries.
- **Don't** let the Updating animation fire on every single agent/response exchange — reserve
  it for genuine section transitions, or it undermines the calmer, conversational tone this
  redesign is going for.

## Related components
`agent-message` (Statement variant carries the section-transition announcement that pairs
with this indicator's Updating state), `chat-composer` (Continue affordance often coincides
with a section-boundary progress update), `top-navigation` (this component is pinned
directly beneath it)
