# Madeleine's Design System

Read this first. Then read the specific rules file for the task at hand.

## Who this is for

Two personal sites by Madeleine Herritage:
- `madeleine.dev` — portfolio, flat HTML + CSS
- `madeleine.cool` — writing, built with 11ty

Both share the same design system. Changes to tokens and base styles
affect both sites.

## What to read for each task

| Task | Read |
|---|---|
| Adding or changing colors | `.clinerules/colors.md` |
| Changing type, scale, or headings | `.clinerules/typography.md` |
| Padding, margins, layout, container | `.clinerules/spacing-layout.md` |
| Transitions, animations, blobs | `.clinerules/motion.md` |
| Building a new component or pattern | `.clinerules/components.md` |
| Anything touching CSS | `design-system.md` + the relevant file above |

## Stack

- Plain CSS (no preprocessors, no frameworks)
- CSS custom properties throughout — no utility classes except `.flow`
- Modern CSS: `oklch()`, `clamp()`, `pow()`, `@property`, CSS nesting,
  `clip-path: shape()`, scroll-driven animations
- 11ty for madeleine.cool (Nunjucks templates)
- No build step for madeleine.dev (flat HTML)

## Hard rules

1. **No raw values in CSS.** Every color, size, and duration comes from
   a token. If a token doesn't exist for what you need, add it to the
   right token file first, then use it.

2. **Don't modify token files to fix one component.** Token files are
   system-wide. Use component slots (see `.clinerules/components.md`).

3. **Preserve intentional design decisions:**
   - Headings are `font-weight: 400` — not a mistake
   - `.site-title` is `--type-sm` — not a mistake
   - Link transitions are `1200ms` — not a mistake
   - Container background is semi-transparent — the blobs show through

4. **Dark mode is automatic.** Semantic color tokens flip via
   `prefers-color-scheme: dark` in `tokens/color.css`. Don't write
   dark mode rules in components.

5. **Spelling:** It's `madeleine` (lowercase), `Herritage` (not Heritage).
