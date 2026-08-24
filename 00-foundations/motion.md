# Motion

## Purpose
Defines duration, easing, and usage rules for animation, so motion feels consistent and purposeful rather than decorative.

## Duration tokens
| Token | Value | Usage |
|---|---|---|
| motion-duration-fast | 100ms | Micro-interactions (button press, toggle, checkbox) |
| motion-duration-default | 200ms | Standard transitions (sheet open, tab switch) |
| motion-duration-slow | 300ms | Larger surface transitions (full-screen navigation, modal) |
| motion-duration-emphasis | 400ms | Rare — used only for onboarding/celebratory moments |

## Easing tokens
| Token | Curve | Usage |
|---|---|---|
| motion-ease-standard | cubic-bezier(0.4, 0.0, 0.2, 1) | Default for most transitions (accelerate then decelerate) |
| motion-ease-decelerate | cubic-bezier(0.0, 0.0, 0.2, 1) | Elements entering the screen |
| motion-ease-accelerate | cubic-bezier(0.4, 0.0, 1, 1) | Elements exiting the screen |

## When to animate
Use motion to:
- Show relationships between states (e.g. a sheet sliding up from the element that triggered it)
- Provide feedback that an action registered (button press, toggle flip)
- Guide attention during navigation transitions

Don't animate:
- Text content changes that need to be read immediately (e.g. form validation errors — appear instantly, don't fade in)
- Anything that would delay a user completing a frequent, repetitive task
- For decoration alone, without a functional reason

## Platform behavior
- **iOS**: match native transition conventions where possible (push/pop navigation, sheet presentation) rather than inventing custom equivalents.
- **Android**: match Material motion conventions (shared axis, fade-through) for consistency with the platform's other apps.
- Respect the OS-level **Reduce Motion** accessibility setting — when enabled, replace movement-based transitions with simple cross-fades or instant changes.

## Accessibility
- Always honor **Reduce Motion** (iOS) / **Remove animations** (Android) system settings.
- Avoid motion that flashes more than 3 times per second (seizure risk).
- Don't rely on motion alone to convey information — pair with a static state change (color, icon, text) too.

## Do / Don't
- **Do** use `motion-duration-fast` for anything triggered directly by a tap.
- **Do** check the Reduce Motion setting before playing non-essential animations.
- **Don't** introduce a new duration or easing curve without checking this list first.

## Related
- [`elevation-shadow.md`](./elevation-shadow.md) — surfaces that animate in/out often change elevation simultaneously