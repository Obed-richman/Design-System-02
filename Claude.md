# Design System — Claude Instructions

## Project overview
This is a plain HTML/CSS design system used for rapid prototyping. There is no JavaScript framework. 
All components are built from tokens, following BEM naming, and output as snippet-only HTML files 
with separate CSS files.

## Stack
- Plain HTML + CSS only — no React, no Vue, no Tailwind, no build tools
- Token variables from `tokens/tokens.css` — always loaded first
- Typography utility classes from `tokens/typography.css`
- SVG icon sprite at `icons/icons.svg` with helper classes in `icons/icons.css`
- Components previewed via VS Code Live Server

## File structure
```
index.html                          ← component sandbox, shows all components
tokens/
  tokens.css                        ← all design tokens (primitive + semantic + size)
  typography.css                    ← utility classes for type styles
components/
  [name]/
    [name].css                      ← component styles only, token variables only
    [name].html                     ← snippet-only markup, no demo page
icons/
  icons.svg                         ← SVG sprite, all icons as <symbol> elements
  icons.css                         ← icon size and colour helper classes
screens/
  template.html                     ← blank screen template to duplicate
  [screen-name].html                ← prototype screens
```

## Non-negotiable rules
1. **No hardcoded values** — every colour, spacing, radius and border must use a CSS variable from `tokens/tokens.css`. Never write a hex value or raw pixel number in a component CSS file.
2. **Tokens always load first** — in every HTML file, `tokens/tokens.css` is always the first `<link>` tag.
3. **BEM naming** — all class names follow BEM: `.block`, `.block__element`, `.block--modifier`.
4. **CSS files contain styles only** — no demo layout, no inline styles, no `<style>` blocks.
5. **HTML files contain snippets only** — no full page structure, no demo wrappers, no `<style>` blocks.
6. **Dark mode via `.dark` parent class** — all dark mode overrides use `.dark .component { }` pattern, never separate stylesheets or media queries.
7. **Components never duplicate each other** — if a component is used inside another (e.g. `.radio` inside `.comparison-tile`), the inner component's CSS is not rewritten. It is linked separately in the screen.
8. **Atoms before molecules** — always build the smallest reusable component first before building the component that contains it.
9. **Read existing files before writing** — always read `tokens/tokens.css` and at least one existing component CSS file before generating a new component, to stay consistent with naming and structure.
10. **Update `index.html` with every new component** — every new component gets a section added to `index.html` so it can be previewed and tested.

## Token naming convention
```css
/* Primitive */        --colour-aqua-40
/* Spacing */          --gap-medium, --gap-large
/* Border radius */    --radius-small, --radius-round
/* Border width */     --border-s, --border-m, --border-focused
/* Semantic — text */  --text-primary, --text-disabled, --text-negative
/* Semantic — bg */    --bg-primary, --bg-brand-aqua, --bg-negative
/* Semantic — border */ --border-color-primary, --border-color-active
/* Semantic — icon */  --icon-primary, --icon-secondary, --icon-negative
```

## Component CSS structure (always follow this order)
```css
/* ============================================
   COMPONENT NAME
   Depends on: tokens/tokens.css, [other dependencies]
   ============================================ */

/* --- Base --- */
/* --- Variants --- */
/* --- States --- */
/* --- Dark mode --- */
```


## Icon usage
```html
<!-- Always use the SVG sprite pattern -->
<svg class="icon icon--xs icon--primary">
  <use href="../../icons/icons.svg#icon-name"></use>
</svg>
```

Icon sizes — full scale from Figma:
| Class | Size | Use case |
|---|---|---|
| `.icon--3xs` | 12px | Micro indicators only (rare) |
| `.icon--xxs` | 16px | Inline icons, inside buttons, tight UI |
| `.icon--xs` | 24px | Default UI icon size |
| `.icon--s` | 32px | Slightly larger UI contexts |
| `.icon--m` | 48px | Feature icons, empty states |
| `.icon--l` | 64px | Large feature icons |
| `.icon--xl` | 72px | Hero icons, onboarding |
| `.icon--xxl` | 96px | Artwork, splash screens |

Icon colour classes (uses currentColor):
.icon--primary, .icon--secondary, .icon--brand,
.icon--positive, .icon--negative, .icon--warning,
.icon--disabled, .icon--on-colour





## Screen template pattern
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <link rel="stylesheet" href="../tokens/tokens.css" />
  <link rel="stylesheet" href="../tokens/typography.css" />
  <!-- component CSS files here — dependencies first -->
</head>
<body>
  <div class="screen">
    <!-- prototype content here -->
  </div>
  <script>
    /* copy JS from component html files here */
  </script>
</body>
</html>
```

## Brand colours (from tokens)
- Brand aqua (primary CTA): `--bg-brand-aqua` / `#12EFD4`
- Brand navy (dark bg): `--bg-brand-navy` / `#09002D`
- Brand purple: `--base-brand-purple` / `#371987`
- Semantic positive: green (`--base-positive`)
- Semantic negative: red (`--base-negative`)
- Semantic warning: yellow (`--base-warning`)
- Font family: Modern Era (Bold, Medium, Regular)
