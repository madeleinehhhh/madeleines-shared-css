---
paths:
  - "**/*.css"
  - "**/*.html"
  - "**/*.njk"
---

# Color Rules

## Three tiers — always follow this chain

```
primitive → semantic → component slot → element
```

**Never skip tiers.** Don't use `--primitive-blue-dark` in a component.
Don't use `--color-blue-dark` for a button background. Go through slots.

## Primitive palette (tier 1)

Named by hue. Reference only from tier 2. Never use directly.

```
Neutrals:   --primitive-darkteal, --primitive-lightbeige
Blues:      --primitive-blue-dark, --primitive-blue, --primitive-blue-bright,
            --primitive-blue-light, --primitive-blue-lightest
Greens:     --primitive-green, --primitive-green-light
Golds:      --primitive-gold, --primitive-gold-dark
Warm/reds:  --primitive-warm, --primitive-warm-light
Accent:     --primitive-orange-dark (burnt orange — use sparingly)
Reserved:   --primitive-teal (unused, don't alias yet)
Also exist: --primitive-orange, --primitive-salmon, --primitive-beige
            (in palette but not aliased — add to tier 2 when first used)
```

## Semantic tokens (tier 2)

Use these in base styles and layout. Not in components.

```
Surfaces:
  --color-surface-page        page background
  --color-surface-container   container background (used at 0.6 opacity)
  --color-text-default        body text

Palette (flat):
  --color-blue-dark           --color-blue            --color-blue-bright
  --color-blue-light          --color-blue-lightest
  --color-green               --color-green-light
  --color-gold                --color-gold-dark
  --color-warm                --color-warm-light
  --color-accent              burnt orange, use sparingly

Interactive:
  --color-interactive         default link/action color
  --color-interactive-hover   hover state
  --color-interactive-active  active/pressed state
  --color-interactive-visited visited links
  --color-interactive-underline
  --color-interactive-focus-ring

Borders:
  --color-border-default      transparent (links at rest)
  --color-border-interactive  focus/hover border
  --color-border-subtle       light dividers

Decorative:
  --color-decor-blob-a        blob gradient color A (gold in light, dark blue in dark)
  --color-decor-blob-b        blob gradient color B (warm/maroon)
```

## Component slots (tier 3)

Define on the component selector, map from tier 2, use internally.

```css
/* Example: link */
a[href] {
  --link-text:       var(--color-interactive);
  --link-hover:      var(--color-interactive-hover);
  color:             var(--link-text);
}

/* Example: button */
.btn-primary {
  --button-text:     var(--primitive-lightbeige);
  --button-bg:       var(--color-blue-bright);
  --button-hover-bg: var(--color-blue);
  background:        var(--button-bg);
  color:             var(--button-text);
}
```

## Dark mode

Handled automatically via `@media (prefers-color-scheme: dark)` in
`tokens/color.css`. Semantic tokens flip automatically — don't write
dark mode overrides in components unless there's a genuine exception.

## Don't do this

```css
/* Raw value — wrong */
color: #0D6FBA;

/* Primitive in a component — wrong */
color: var(--primitive-blue);

/* Semantic in a component without a slot — wrong */
color: var(--color-interactive);

/* Right */
.my-component {
  --my-component-text: var(--color-interactive);
  color: var(--my-component-text);
}
```
