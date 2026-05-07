---
paths:
  - "**/*.css"
  - "**/*.html"
  - "**/*.njk"
---

# Adding New Components

## Before writing anything

1. Check `base/type.css` — does the element already exist as a base style?
2. Check `site/site.css` — does a similar pattern already exist?
3. Check if it's really a variant of something existing vs a new component.

## Component file location

Site-level one-off styles → `site/site.css`
Reusable component → `site/components/[name].css`

## Component pattern

Every component follows this structure:

```css
.component-name {
  /* 1. Component slots — map from semantic tokens */
  --component-text:    var(--color-text-default);
  --component-bg:      var(--color-surface-container);
  --component-border:  var(--color-border-subtle);

  /* 2. Layout using space tokens */
  padding:  var(--space-sm) var(--space-md);
  gap:      var(--space-sm);

  /* 3. Typography using type tokens */
  font-size: var(--type-sm);

  /* 4. Apply slots */
  color:      var(--component-text);
  background: var(--component-bg);
}

/* State variants override slots, not token values */
.component-name:hover {
  --component-bg: var(--color-blue-lightest);
}

/* Modifier classes override slots */
.component-name--accent {
  --component-text: var(--primitive-lightbeige);
  --component-bg:   var(--color-accent);
}
```

## Links

Base link styles are set in `base/type.css` and apply automatically.
Don't rewrite link styles from scratch. Override slots instead:

```css
.my-context a[href] {
  --link-text:   var(--color-warm);
  --link-hover:  var(--color-warm-light);
}
```

To remove underline/border on a specific link (e.g. post titles):
```css
.postlist-title a {
  text-decoration: none;
}
```

## Checklist for new components

- [ ] Uses only token values (no raw hex, px, or magic numbers)
- [ ] Defines component slots before using them
- [ ] States (hover, focus, active) override slots not tokens
- [ ] Respects `prefers-reduced-motion` if it has animations
- [ ] Semantic HTML (don't use `<div>` where a better element exists)
- [ ] Works in both light and dark mode without extra media queries
      (dark mode is handled by token overrides automatically)
