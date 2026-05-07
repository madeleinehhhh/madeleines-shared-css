# Design System Overview

This is a token-based CSS design system shared across two sites:
- `madeleine.dev` — flat HTML + CSS
- `madeleine.cool` — 11ty

## File structure

```
tokens/         Pure custom properties. No selectors. No output.
  color.css     Primitives → semantic → component slot pattern
  type.css      Font families, fluid scale, leading, weights
  space.css     4-step spacing scale + layout tokens
  motion.css    Easing, duration, blob animation defaults

base/           Global element styles. Reference tokens only.
  fonts.css     @font-face, @view-transition
  reset.css     body, img, video, iframe, a11y utilities
  type.css      Headings, links, .flow utility
  layout.css    .container, header, nav, footer
  animation.css Blob decorative system

site/
  site.css      Site-specific styles shared across both sites
```

## Load order (every page)

```html
<link rel="stylesheet" href="/css/tokens/color.css">
<link rel="stylesheet" href="/css/tokens/type.css">
<link rel="stylesheet" href="/css/tokens/space.css">
<link rel="stylesheet" href="/css/tokens/motion.css">
<link rel="stylesheet" href="/css/base/fonts.css">
<link rel="stylesheet" href="/css/base/reset.css">
<link rel="stylesheet" href="/css/base/type.css">
<link rel="stylesheet" href="/css/base/layout.css">
<link rel="stylesheet" href="/css/base/animation.css">
<link rel="stylesheet" href="/css/site/site.css">
```

`animation.css` is optional — only load it on pages that use blobs.

## Three rules

1. **Tokens only in components.** Never use raw values (`#044488`, `1rem`)
   in base or site styles. Always reference a token.
2. **Don't modify token files to fix a component.** Add a component slot
   instead — see color.css tier 3 pattern.
3. **New components use existing scale steps.** `--space-xs/sm/md/lg`,
   `--type-xs` through `--type-6xl`. Don't invent new values.
