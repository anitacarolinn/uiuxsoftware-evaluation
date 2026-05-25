# CLAUDE.md — Design System Rules for Figma MCP Integration

> Reference doc for AI agents (via Figma MCP) generating designs that match this project's visual system.
> Project: **UI/UX Design Tools Evaluation 2026** — a single-author HTML slide deck comparing 5 AI design tools.

---

## Project Type

**Vanilla HTML/CSS slide-deck** (no build system, no framework). Each `.html` file is a self-contained presentation with embedded `<style>` and `<script>` blocks. Three deck variants exist:

| File | Purpose |
|---|---|
| `design-tools-evaluation.html` | Full English version (13 slides, detail backup) |
| `design-tools-evaluation-short.html` | Short English version (12 slides) |
| `design-tools-evaluation-short-zh.html` | **Canonical visual reference** — Traditional Chinese short version (13 slides, latest design tokens) |
| `design-tools-evaluation.md` | Source-of-truth content document (Markdown) |
| `build_pptx.py` | Generates `design-tools-evaluation-zh.pptx` from same content |

> **When generating Figma designs**, mirror the styles in `design-tools-evaluation-short-zh.html` — it's the most up-to-date.

---

## 1. Token Definitions

Tokens are defined as CSS custom properties on `:root` in each HTML file. **No external token system, no JSON, no Style Dictionary.** Tokens are duplicated across the 3 HTML files (kept in sync manually).

### Source of truth
`design-tools-evaluation-short-zh.html` lines 12-28.

### Color tokens

```css
:root {
  /* Tool brand colors (1:1 mapping per tool) */
  --figma:    #7c3aed;  /* purple — Figma Make */
  --paper:    #dc2626;  /* red — Paper Design */
  --stitch:   #15803d;  /* green — Stitch AI */
  --aistudio: #1d4ed8;  /* blue — Google AI Studio */
  --claude:   #b45309;  /* amber — Claude Design */

  /* Surface tokens (warm cream theme) */
  --bg:       #f7f1e3;  /* page background */
  --surface:  #fdfaf2;  /* card / elevated surface */
  --surface2: #f0e8d3;  /* deeper elevated (table headers, etc.) */
  --border:   #d9cfb8;  /* subtle border */

  /* Text tokens */
  --text:     #2a2520;  /* primary warm-dark text */
  --text-dim: #6b6358;  /* secondary text */

  /* Semantic accent */
  --accent:   #4f46e5;  /* indigo — links, active states, callouts */
  --success:  #16a34a;  /* green — pros, ✓ */
  --danger:   #dc2626;  /* red — cons, ✗ */
  --warning:  #ca8a04;  /* amber — partial / caveat */
}
```

### Tool-color convention (CRITICAL)

Every reference to a tool — whether badge, table header, accent stripe, or text highlight — **must use that tool's dedicated color**:

| Tool | Color var | Hex | Use case |
|---|---|---|---|
| Figma Make | `--figma` | `#7c3aed` | All Figma branding, the "Late-Breaking" Figma pivot slide |
| Paper Design | `--paper` | `#dc2626` | Note: shares hex with `--danger` — that's intentional |
| Stitch AI | `--stitch` | `#15803d` | |
| Google AI Studio | `--aistudio` | `#1d4ed8` | |
| Claude Design | `--claude` | `#b45309` | |

There is a `.highlight-{tool}` utility class for inline text coloring (e.g., `<span class="highlight-figma">Figma</span>`).

### No token transformation

Tokens are consumed directly via `var(--name)`. No SCSS variables, no Tailwind config, no Style Dictionary build step.

---

## 2. Component Library

**No formal component library.** Components are defined as **CSS classes within the same file** and used by composing semantic HTML. Each slide is a `<section class="slide">` containing nested elements styled via these classes.

### Recurring "components" (CSS class patterns)

| Class | Purpose | Visual signature |
|---|---|---|
| `.slide` | Full-viewport slide container with scroll-snap | `min-height: 100vh`, centered content |
| `.slide-inner` | Inner content wrapper, max-width 1200px | |
| `.tool-card` | 5-tool comparison card (overview slide) | Cream surface, top accent stripe in tool color, centered text, emoji icon, badge |
| `.tool-badge` | Pill-shaped tool name | White text on tool-color bg, rounded 20px |
| `.matrix` | Comparison table | Cream surface, single-color border, header row in `--surface2` |
| `.pc-card` (`.good` / `.bad`) | Pros/cons card on tool deep-dive slides | Border + padding card, head with `+` (success) or `−` (danger) |
| `.verdict-bar` | Bottom summary bar on tool slides | Left-border accent in indigo, padding 18-24px |
| `.flow-input` / `.flow-out` | Methodology flow diagram cells | Indigo bg for input, cream for outputs |
| `.summary-pill` | Final-takeaway summary card | Small card with top accent stripe |
| `.timeline-card` | Figma pivot blog cards | Cream surface, full border in `--figma` color |
| `.pivot-callout` | Highlighted callout on Figma pivot slide | Cream + figma border, centered text |
| `.best-combo` | Final-takeaway hero block | Multi-color radial gradient bg, centered |
| `.fade-in` (+ `.visible`) | Scroll-triggered animation | `opacity` + `translateY` transition |

### Component documentation
None. Read the HTML file directly to see usage. Each slide demonstrates the patterns in context.

---

## 3. Frameworks & Libraries

| Layer | Tool |
|---|---|
| **Markup** | Vanilla HTML5 |
| **Styling** | Vanilla CSS (no preprocessor) |
| **Scripting** | Vanilla ES6+ JavaScript (~30 lines per file, inline `<script>`) |
| **Build** | None — open files directly in browser |
| **Bundler** | None |
| **Package manager** | None for the HTML; Python uses `pip` for `python-pptx` (PPTX generation) |
| **Fonts** | Google Fonts: `Inter` (Latin) + `Noto Sans TC` (Traditional Chinese) |

### Framework decisions worth noting
- **No Tailwind, no CSS-in-JS, no PostCSS.** Styling is a single embedded `<style>` block.
- **No JS framework.** Scroll-snap CSS + small IntersectionObserver for slide tracking.
- **Self-contained files.** Each HTML opens standalone — no shared CSS file, no shared JS.

---

## 4. Asset Management

### Image assets
Live in `img/` at the project root. Currently 3 PNGs (screenshots from each tested tool):

```
img/
├── googleaistudio-1.png
├── paper-1.png
└── stitch-1.png
```

These are referenced **by external link in the deck** (not embedded `<img>` tags in current slides). Used as reference material when reviewing tool outputs, not as deck visuals.

### No CDN, no optimization pipeline
Images are committed as-is. No WebP conversion, no responsive `srcset`, no lazy loading.

### When generating Figma designs
Use placeholder rectangles or Figma-native icon sets for any image regions. Don't assume specific image assets exist.

---

## 5. Icon System

**No icon library.** Icons are **Unicode emoji** placed inline as text or in `<span>` with `font-size`.

### Icon-emoji mapping conventions

Each tool has a "signature emoji" used at the top of its deep-dive slide:

| Tool | Emoji | Meaning |
|---|---|---|
| Figma Make | 🎨 | designer focus |
| Paper Design | 📐 | precision / code-native |
| Stitch AI | ⚡ | fast |
| Google AI Studio | 🚀 | ship / deploy |
| Claude Design | ✨ | AI / polished |

### Functional emoji used in body content

| Emoji | Used for |
|---|---|
| 🚀 | deploy / publish features |
| 🔌 | integrations |
| 📦 | packages, downloads |
| ⚙️ | settings, code editing |
| 🎯 | verdict, focus |
| 🖱️ | GUI editing |
| 📱 | responsive / mobile |
| ↩️ | one-way / sync issues |
| 🔗 | linking, MCP |
| ⚛️ | React / framework |
| 🚫 | not supported |
| 🎬 | interactive preview |
| 💰 / 💸 | pricing |
| 💬 | prompt-only / chat |
| 1️⃣ | single version |
| ❓ | unknown / Q&A |
| 🌐 | web / browser-only |
| 🤖 | AI |
| 📝 | prompt input |
| 📊 | metrics / measurement |
| 🔍 | analysis |
| 🛠️ | tools / multiple edit modes |
| ⏳ | quota / time limit |
| 🔁 | remix / fork |
| 📤 | export options |
| 📄 | HTML / document output |
| 📅 | dates (used in Figma pivot timeline) |

### Naming convention
None — emoji are inline characters, not named. When generating Figma equivalents, use Figma's icon plugins (e.g., Lucide, Material) and pick semantically equivalent icons.

---

## 6. Styling Approach

### Methodology
- **Plain CSS classes.** No BEM, no CSS Modules, no scoped styles.
- **Utility classes mixed with component classes.** E.g., `.highlight-figma` is utility; `.tool-card` is component.
- **Heavy use of inline styles for one-off visuals** (e.g., colored gradients, custom grid layouts on individual slides). This is intentional — the deck is single-file and one-off layouts don't justify class definitions.

### Global styles
- CSS reset at top of `<style>` block: `*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }`
- `html` gets `scroll-behavior: smooth` and `scroll-snap-type: y mandatory`
- `body` gets cream `--bg`, font stack, `overflow-x: hidden`

### Typography scale

```css
h1        clamp(40px, 6vw, 76px)   weight 900  line-height 1.05-1.15
h2        clamp(32px, 4.5vw, 56px) weight 800  line-height 1.15-1.2  margin-bottom 32px
h3        22px                     weight 700                        margin-bottom 14px
.subtitle clamp(16px, 1.8vw, 22px) weight 300  color text-dim
.label    14px                     weight 700  letter-spacing 2px    color accent (eyebrow)
body      Inter 400 (or Noto Sans TC for the -zh deck)
```

### Spacing scale
Pixel-based, roughly 4px-aligned: `4 / 6 / 8 / 10 / 12 / 14 / 16 / 18 / 20 / 22 / 24 / 28 / 32 / 36`. Card padding typically `18-24px`; section padding `100px 60px 60px` (top/horizontal/bottom).

### Border radii
- Pills/badges: `20-24px`
- Cards: `12-16px`
- Hero callouts: `16px`
- Small chips/code: `4-8px`

### Responsive design
2 breakpoints, defined at the bottom of the `<style>` block:

```css
@media (max-width: 1100px) {
  .tool-cards, .summary-grid { grid-template-columns: repeat(3, 1fr); }
  .flow { grid-template-columns: 1fr; }
  .flow-arrow { display: none; }
}
@media (max-width: 768px) {
  .slide { padding: 80px 20px 40px; }
  nav { padding: 12px 20px; }
  .tool-cards, .summary-grid, .pros-cons-grid, .timeline { grid-template-columns: 1fr; }
  .key-hint { display: none; }
}
```

### Gradients (notable)

Multi-color brand gradient (used on hero `.gradient-text` and `.best-combo` background):

```css
linear-gradient(135deg,
  var(--figma), var(--stitch), var(--aistudio), var(--claude), var(--paper))
```

For backgrounds, the same colors are used at `~0.08` alpha to create a subtle wash.

---

## 7. Project Structure

```
uiuxsoftware-evaluation/
├── design-tools-evaluation.md          ← Source-of-truth content (canonical MD)
├── design-tools-evaluation.html        ← Full English deck (13 slides)
├── design-tools-evaluation-short.html  ← Short English deck (12 slides)
├── design-tools-evaluation-short-zh.html ← Short Traditional Chinese deck (13 slides) ← VISUAL REFERENCE
├── design-tools-evaluation-zh.pptx     ← Generated PPTX (Chinese, A2-B1 vocab)
├── build_pptx.py                       ← Python script that generates the PPTX from MD content
├── figma-mcp-blog-notes.md             ← Reference notes on Figma's MCP blogs (Mar + Apr 2026)
├── CLAUDE.md                           ← This file
└── img/                                ← Tool screenshots (reference only)
    ├── googleaistudio-1.png
    ├── paper-1.png
    └── stitch-1.png
```

### Organization patterns

- **Single-file decks.** Each HTML deck is fully self-contained — CSS, JS, content all inline. No imports.
- **Slide structure.** Each slide is `<section class="slide" data-slide="N">` with `<div class="slide-inner fade-in">` inside. Slide order is sequential and numbered via `data-slide`.
- **Slide naming convention.** Each slide is preceded by an HTML comment marker: `<!-- N: SLIDE NAME -->`. Useful for navigation in source.
- **Three parallel HTML versions** (full / short EN / short ZH) — content is roughly synchronized but not strictly. The MD file is the canonical content source.
- **No subfolders for code.** Everything at root.

### Conventions worth preserving when generating new Figma designs

1. **5-tool grid** is the recurring layout — designs comparing tools should use a 5-column grid (or 3+2 / 1 column on mobile breakpoints).
2. **Tool color always sticks** — Figma is purple, Paper is red, etc. Never swap.
3. **Cream surface palette** — backgrounds are warm cream, not white. Pure white would feel out of place.
4. **Top accent stripe** on cards (4px tall, in tool color) is a recurring accent pattern.
5. **Eyebrow label + h2 title** is the standard slide intro.
6. **Pros/cons two-column** uses `+` (green) and `−` (red) prefixes — not `✓` / `✗` (those are reserved for the matrix-style comparison table).
7. **Verdict bar** at bottom of tool deep-dive uses left-border indigo accent.

---

## When Generating Figma Designs via MCP

1. **Match the cream theme** — set the canvas background to `#f7f1e3` and use `#fdfaf2` for cards.
2. **Use the exact tool-color hex codes** when designing anything related to a specific tool.
3. **Keep typography consistent** — Inter for Latin, Noto Sans TC for Chinese; use the documented weight scale.
4. **Default to rounded corners** (12-20px) on most surfaces.
5. **For comparison layouts**, use 5-column grid; for narrative layouts, max-width 1200px centered.
6. **For icons**, prefer flat single-color glyphs (Lucide-style) — they pair best with the typographic, low-chrome aesthetic.
7. **Generated designs should look like they belong in this slide deck.** If in doubt, open `design-tools-evaluation-short-zh.html` and copy the visual conventions of the closest analogous slide.

---

> Last updated: 2026-05-01
