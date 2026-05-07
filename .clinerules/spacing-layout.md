---
paths:
  - "**/*.css"
  - "**/*.html"
  - "**/*.njk"
---

# Spacing & Layout Rules

## Spacing scale

Four steps. Use these. Don't invent new values.

```
--space-xs    0.5em    tight insets, nav padding
--space-sm    0.75em   comfortable insets, header gap
--space-md    1rem     prose margin, base unit
--space-lg    2em      section separation, header below
```

Two special-purpose tokens:
```
--space-flow        clamp(0.5em, 0.5em + 1vw, 1em)   flow utility rhythm
--space-link-inset  2px                                link border + padding
```

When in doubt: `--space-md` for breathing room, `--space-sm` for
tight component internals, `--space-lg` for section-level separation.

## Layout tokens

```
--layout-max-width        70ch     container max-width
--layout-gutter-inline    8vw      container side padding
--layout-gutter-block     4vw      container top/bottom padding
--layout-section-padding  calc(0.5vh + 0.5vw)   direct children of .container
--layout-footer-size      0.8em
--layout-nav-size         var(--type-xs)
```

## Container

Every page uses `.container` as the outer wrapper:

```html
<div class="container">
  <header>...</header>
  <main>...</main>
  <footer>...</footer>
</div>
```

Container is max `70ch` wide, centered, with fluid gutters.
Background is semi-transparent (`oklch ... / 0.6`) so blobs show through.
Don't add a second wrapper inside container — it already handles centering.

## Page header pattern

```html
<header>
  <h1 class="site-title"><a href="/">madeleine.dev</a></h1>
  <nav>
    <ul class="nav">
      <li><a href="/work">Work</a></li>
      <li class="current-page"><a href="/">Home</a></li>
    </ul>
  </nav>
</header>
```

Header is flex row, nav takes full width below, nav list is flex justified right.
Current page gets `font-style: italic` via `.current-page`.

## Blob system

Blobs are decorative background elements. Add them as empty divs
directly inside `.container`, before `<header>`:

```html
<div class="blob-01"></div>
<div class="blob-02"></div>
...
<div class="blob-06"></div>
```

Only include `base/animation.css` on pages that use blobs.
Colors are driven by `--color-decor-blob-a` and `--color-decor-blob-b`
from `tokens/color.css` — change colors there, not in `animation.css`.

## Don't do this

```css
/* Magic number — wrong */
margin-top: 24px;

/* Step that doesn't exist — wrong */
padding: var(--space-xl);

/* Right */
padding: var(--space-md);
margin-top: var(--space-lg);
```
