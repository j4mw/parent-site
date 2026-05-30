# Voidframe
### A design system for focused, browser-based tools

---

## What it is

Voidframe is a minimal dark UI system built for single-purpose tools. It prioritises function over decoration — every element earns its place. The aesthetic sits between engineering software and modern developer tooling: precise, legible, slightly industrial.

---

## Foundations

### Colour

Each Voidframe product has one accent colour. The base palette is shared across all products.

| Token | Value | Usage |
|---|---|---|
| `--bg` | `#0d0d0d` | Page background |
| `--surface` | `#161616` | Header, sidebar, cards |
| `--surface2` | `#1e1e1e` | Input backgrounds, nested surfaces |
| `--border` | `rgba(255,255,255,0.08)` | Subtle dividers |
| `--border2` | `rgba(255,255,255,0.14)` | Visible borders, input outlines |
| `--text` | `#f4f4f4` | Primary text |
| `--text2` | `#c0c0c0` | Secondary text, labels |
| `--text3` | `#707070` | Muted text, hints, placeholders |
| `--danger` | `#f87171` | Errors, destructive actions |

**Accent colours** are assigned per-product and should not be shared:

| Product | Accent | Accent2 |
|---|---|---|
| 0layer (brand/home) | `#f97316` — burnt orange | `#ea580c` |
| DXF Studio | `#fbbf24` — amber | `#f59e0b` |
| Bar Optimiser | `#7dd3fc` — sky blue | `#38bdf8` |

Accent colours are used for: wordmark icon background, interactive highlights, active states, glow effects, badges, stat values, and hover transitions. Never use more than one accent per page.

### Typography

```
--font-sans:  'Geist', sans-serif
--font-mono:  'Geist Mono', monospace
```

- **Geist** for all UI labels, buttons, navigation, body copy
- **Geist Mono** for all data values, coordinates, measurements, code, hints, metadata
- Base size: `13px`
- Use `-webkit-font-smoothing: antialiased` always

### Spacing & Radius

```
--radius:     6px   (cards, toasts, dropdowns)
--radius-sm:  4px   (buttons, inputs, badges)
```

Spacing is not tokenised — use multiples of `4px` as a mental guide.

---

## Layout

### App Shell

Every Voidframe app uses the same shell:

```
┌─────────────────────────────────────┐
│ Titlebar (52px fixed height)        │
├──────────┬──────────────────────────┤
│ Sidebar  │ Main content area        │
│ (240px)  │                          │
│          │                          │
└──────────┴──────────────────────────┘
```

- `body` and `html` are `height: 100vh`, `overflow: hidden`
- Sidebar scrolls internally; main area scrolls internally
- On mobile (`≤600px`) sidebar stacks above main content

### Titlebar

- Height: `52px`
- Background: `var(--surface)`
- Bottom border: `1px solid var(--border)`
- Contains: wordmark (left), file/status badge (left of centre), actions (right)
- Wordmark icon: `26×26px`, `border-radius: 5px`, `background: var(--accent)`, SVG fill `#0d0d0d`
- Dividers between titlebar sections: `1px × 20px`, `background: var(--border2)`

### Sidebar

- Width: `240px` desktop, full-width stacked on mobile
- Background: `var(--surface)`
- Right border: `1px solid var(--border)`
- Sections separated by `border-bottom: 1px solid var(--border)`, `padding: 12–16px`
- Section titles: `10px`, `600` weight, `0.08em` letter-spacing, uppercase, `var(--text2)`

---

## Components

### Buttons

Three variants only:

```
.btn-primary   background: accent, dark text, bold — main CTA
.btn-outline   transparent, accent border on hover — secondary actions
.btn-ghost     transparent, subtle border — tertiary / destructive
```

All buttons: `height: 32px`, `padding: 0 12px`, `font-size: 12px`, `font-weight: 500`, `border-radius: var(--radius-sm)`. Disabled state: `opacity: 0.3`, `pointer-events: none`.

Icons in buttons: `13×13px`, left of label.

### Inputs

```css
background: var(--surface2);
border: 1px solid var(--border2);
border-radius: var(--radius-sm);
padding: 6-7px 10px;
font-family: var(--font-mono);
font-size: 12px;
color: var(--text);
```

Focus state: `border-color: rgba(R,G,B, 0.5)` where RGB is the accent colour. No box-shadow.

### Stat Cards

Used in sidebars and stats strips for key numbers.

```
background: var(--surface2)
border: 1px solid var(--border)
border-radius: var(--radius-sm)
padding: 8-10px
label: 10px, var(--text2), font-mono
value: 14-18px, 600 weight, font-mono, tabular-nums
```

### Badges / Pills

Small inline labels for status, counts, tags:

```
font-size: 10px
font-family: var(--font-mono)
padding: 2px 6-8px
border-radius: 4-10px
border: 1px solid rgba(accent, 0.2)
background: rgba(accent, 0.08-0.12)
color: var(--accent)
```

### Toasts

```
position: fixed, top: 16px, centered
border-radius: var(--radius)
font-size: 12px
animation: slide in from top, 0.2s ease
auto-dismiss: 4 seconds
```

Two states: error (red tint) and success (accent tint).

### Dropdowns

```
background: var(--surface)
border: 1px solid var(--border2)
border-radius: 6px
padding: 4px
box-shadow: 0 8px 32px rgba(0,0,0,0.5)
```

Items: `padding: 7px 10px`, `border-radius: 4px`, hover `background: var(--surface2)`.

---

## Backgrounds

### App viewport / canvas areas

Use a two-level grid to give depth without noise:

```css
background-color: #080b0f;
background-image:
  linear-gradient(rgba(R,G,B, 0.05) 1px, transparent 1px),
  linear-gradient(90deg, rgba(R,G,B, 0.05) 1px, transparent 1px),
  linear-gradient(rgba(R,G,B, 0.018) 1px, transparent 1px),
  linear-gradient(90deg, rgba(R,G,B, 0.018) 1px, transparent 1px);
background-size: 160px 160px, 160px 160px, 32px 32px, 32px 32px;
```

RGB should be the accent colour. Major grid at 160px, minor at 32px.

### Home/marketing pages

Same grid but slightly more muted. Background `#080b0f`.

---

## Navigation (cross-product)

Every sub-page includes the 0layer nav in the top-right of the titlebar:

- 0layer wordmark (links to `/`)
- Divider
- "Tools" dropdown button — lists all tools, highlights current page in accent

The nav should never compete with the product's own wordmark. Keep it small and right-aligned.

---

## About & Footer

Every page ends with:

1. **About section** — `var(--surface)`, top border. Contains the product's wordmark icon, product name, one-sentence description, link back to all tools.
2. **Footer** — `var(--surface)`, top border, `10px` mono text. Left: `© 0layer · James Wright [year]`. Right: Ko-fi link or utility text.

---

## Glow / rendering effects

For canvas-rendered content (DXF viewer etc):

- `ctx.shadowColor = strokeColour`
- `ctx.shadowBlur = 4` (fixed, not scale-dependent)
- `ctx.lineWidth = 1.5` (fixed)
- `ctx.fillStyle = 'transparent'` unless explicitly filling
- Wrap each entity in `ctx.save()` / `ctx.restore()`

---

## Responsive breakpoints

| Breakpoint | Behaviour |
|---|---|
| `≤900px` | Sidebar flips horizontal across top |
| `≤600px` | Full single column, sidebar sections stack, compact titlebar |
| `≤380px` | Stat strip goes 2-column |

---

## Tone & copy

- Short, factual, no marketing language
- No em-dashes (`—`), no ellipses for drama, no exclamation marks
- Labels in ALL CAPS at `10px` with `0.08-0.1em` letter-spacing
- Describe what the thing does, not what it "enables" or "empowers"
- Numbers and measurements in `font-mono`

---

## Naming convention

Products are named like tools, not apps:
- `DXF Studio` — noun + context
- `Bar Optimiser` — verb + noun

The parent brand `0layer` uses a zero, not the letter O.

---

*Voidframe v1 — 0layer design system*
