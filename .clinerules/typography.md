---
paths:
  - "**/*.css"
  - "**/*.html"
  - "**/*.njk"
---

# Typography Rules

## Font families

```css
--font-body:     'Inter', sans-serif       /* all body copy */
--font-heading:  'Space Grotesk', sans-serif  /* all headings */
--font-mono:     monospace                 /* code */
```

Space Grotesk is self-hosted (variable, 200–800 weight range).
Inter loads from system/CDN.

## Type scale

All steps are fluid — derived from a base clamp via `pow()`.
Use these tokens. Never write `font-size: 1.2rem` directly.

```
--type-xs      captions, fine print, nav
--type-sm      body copy (default font-size on body)
--type-base    medium/base
--type-lg      large body, intro text
--type-xl      h6
--type-2xl     h5
--type-3xl     h4
--type-4xl     h3
--type-5xl     h2
--type-6xl     h1
```

Heading → scale mapping is set in `base/type.css`. Don't override
heading sizes in components — add a modifier class instead.

## Heading style

All headings use Space Grotesk at `font-weight: 400` (intentional —
not a mistake). The elegance comes from the typeface, not weight.
Don't change headings to bold.

## Site title

`.site-title` uses `--type-sm` deliberately — kept small so the long
site name doesn't overflow on small screens and keeps emphasis on content.
Don't increase this size.

## Line height

```
--leading-tight    1      headings, display text
--leading-normal   1.5    body copy, lists
--leading-loose    1.9    long-form prose paragraphs
```

## Weights

```
--weight-normal    400    body text
--weight-bold      700    inline bold, links in prose
--weight-heading   400    all headings
```

## Flow utility

`.flow` adds vertical rhythm between siblings:
```html
<div class="flow">
  <p>...</p>
  <p>...</p>  <!-- gets margin-top: --space-flow -->
</div>
```

Override rhythm for a section:
```html
<div class="flow flow-tight">  <!-- tighter spacing -->
<div class="flow" style="--flow-space: var(--space-lg)">  <!-- custom -->
```

Legacy aliases still work: `.little-to-no-spacing`, `.coursework`.

## Display type (homepage only)

These classes exist for the madeleine.dev homepage intro block only.
Don't repurpose them for other large text — add new classes instead.

```
.welcome    clamp(1.4em, 4vw, 2.2em)
.intro      clamp(1.2em, 3.2vw, 2em)
.name       clamp(2rem, 5vw, 3.6em) + letter-spacing: 0.01em
```
