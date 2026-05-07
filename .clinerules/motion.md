---
paths:
  - "**/*.css"
---

# Motion Rules

## Tokens

```
--ease-default      cubic-bezier(0.07, 1.00, 0.00, 1.00)   fast in, slow settle
--duration-fast     200ms    subtle state changes
--duration-ui       1200ms   link/hover transitions (slow by design — the
                             easing curve front-loads the visible change)
--duration-entrance 600ms    elements appearing
```

All durations zero out automatically under `prefers-reduced-motion`.

## Transitions

Scope transitions to only the properties that change.
Never use `transition: all`.

```css
/* Wrong */
transition: all var(--duration-ui) var(--ease-default);

/* Right */
transition:
  color         var(--duration-ui) var(--ease-default),
  border-color  var(--duration-ui) var(--ease-default);
```

## Blob system

Blob animations are self-contained in `base/animation.css`.
Don't add new blobs beyond `.blob-06` without checking available
class names first. Don't modify `--_timing-*` variables from outside
`animation.css` — they're private (underscore prefix = internal).

To change blob colors: update `--color-decor-blob-a` and
`--color-decor-blob-b` in `tokens/color.css`.

To add a blob variant: copy an existing blob block in `animation.css`,
give it a new class name, adjust `--blob-size`, `--_timing-*`,
`--movementLength-*`, and `--_i` as needed.

## Reduced motion

Already handled at the token level and in `base/animation.css`.
Don't write `prefers-reduced-motion` overrides in component files
unless the component has its own non-token animations.
