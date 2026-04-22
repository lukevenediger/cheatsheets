# cheatsheets design system

Extracted from `tmux.html`. Reference for future cheatsheets. Goal: dense, scannable, print-friendly, auto light/dark.

## Principles

- **Density first.** Multi-column grid with compact cards. One topic per section.
- **Hairline borders.** `0.5px` everywhere for crisp separation without visual weight.
- **Muted chrome, bright content.** Labels and borders fade back; content and accents pop.
- **Auto dark mode** via `prefers-color-scheme`.
- **Print-ready** by default. Sections avoid breaking mid-card.

## Tokens

### Colors — light (default)

| Token | Value | Use |
|---|---|---|
| `--bg` | `#faf9f5` | Page background (warm off-white) |
| `--surface` | `#ffffff` | Card / section background |
| `--border` | `rgba(0, 0, 0, 0.12)` | Hairline dividers |
| `--border-strong` | `rgba(0, 0, 0, 0.2)` | Emphasis borders |
| `--text` | `#1a1a1a` | Primary text |
| `--text-muted` | `#666` | Secondary text, section labels |
| `--text-faint` | `#888` | Tertiary, footer, separators |
| `--accent` | `#c96442` | Brand accent (terracotta) |
| `--kbd-bg` | `#f3f1e9` | kbd / code background |
| `--kbd-border` | `rgba(0, 0, 0, 0.15)` | kbd border |
| `--code` | `#3c3a34` | Inline code text |

### Colors — dark

| Token | Value |
|---|---|
| `--bg` | `#1a1a1a` |
| `--surface` | `#242424` |
| `--border` | `rgba(255, 255, 255, 0.1)` |
| `--border-strong` | `rgba(255, 255, 255, 0.18)` |
| `--text` | `#f0ece3` |
| `--text-muted` | `#a8a59b` |
| `--text-faint` | `#7a776e` |
| `--accent` | `#d97757` |
| `--kbd-bg` | `#2f2f2f` |
| `--kbd-border` | `rgba(255, 255, 255, 0.18)` |
| `--code` | `#d0ccc0` |

### Radius

- `--radius: 8px` — kbd, prefix-note right side, small cards
- `--radius-lg: 12px` — section cards
- `4px` — kbd, inline code (hardcoded, not token)

### Typography

- **Sans stack:** `-apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif`
- **Mono stack:** `ui-monospace, "SF Mono", Menlo, Consolas, monospace`
- **Base:** `15px / 1.6`, antialiased

| Element | Size | Weight | Notes |
|---|---|---|---|
| `h1` | 28px | 500 | `letter-spacing: -0.01em` |
| `h2` | 14px | 500 | UPPERCASE, `letter-spacing: 0.06em`, muted color |
| `.subtitle` | 14px | 400 | muted |
| `dt` | 13px | 400 | nowrap |
| `dd` | 14px | 400 | muted |
| `kbd` | 12px | 500 | mono |
| `code` | 12.5px | 400 | mono |
| `footer` | 13px | 400 | faint, centered |

### Spacing

- `.container`: `max-width: 1100px`, padding `3rem 1.5rem 4rem`
- Section padding: `1.25rem 1.5rem 1.5rem`
- Grid gap: `1.25rem`
- `dl` gap: `0.5rem 1rem` (row / col)
- Header: `margin-bottom: 2.5rem`, `padding-bottom: 1.5rem`

## Layout

```
.container → .grid (auto-fit, minmax(320px, 1fr)) → section cards
```

- Grid auto-collapses at narrow widths. Cards keep min 320px so content stays readable.
- Each `section` is self-contained (title + data list). Never breaks across columns mid-item.

## Components

### Section card

```html
<section>
  <h2>TITLE</h2>
  <dl>...</dl>
</section>
```

- `--surface` bg, `0.5px` border, `--radius-lg` corners
- `h2` has hairline bottom border, uppercase + wide letter-spacing

### Key-value list (`dl`)

```html
<dl>
  <dt><kbd class="prefix">pre</kbd> <kbd>d</kbd></dt>
  <dd>Detach from session</dd>
</dl>
```

- 2-col grid: `auto 1fr`, baseline-aligned
- `dt` = trigger (keys/command), `dd` = description

### Keyboard key (`kbd`)

```html
<kbd>Ctrl</kbd><span class="plus">+</span><kbd>b</kbd>
<kbd class="prefix">pre</kbd>   <!-- accent-colored for prefix keys -->
```

- `--kbd-bg` bg, `0.5px` border, `4px` radius, `1px 6px` padding
- `.prefix` variant uses `--accent` text color for chord anchors
- `.plus` span between keys: `11px` faint, margin `0 2px`

### Inline code (`code`)

```html
<code>tmux new -s mywork</code>
```

- Same visual family as `kbd` but `--code` text color
- Use for shell commands, config lines, command-mode invocations

### Command list

```html
<div class="cmd-list">
  <code>tmux ls</code>
  <code>tmux attach -t name</code>
</div>
```

- Vertical stack of `<code>` blocks, `0.5rem` gap
- Use when items are commands, not key-chords

### Meta links (`.meta`)

```html
<div class="meta">
  <span><span class="label">Home</span><a href="...">example.com</a></span>
  <span><span class="label">Install</span><code>brew install tool</code></span>
</div>
```

- Sits under the subtitle in `<header>`. Shows tool homepage, install command, docs, admin console, etc.
- `.label` is tiny uppercase eyebrow (`11px`, wide letter-spacing, `--text-faint`).
- Link style: `--text-muted` with hairline underline; hover switches to `--accent`.
- Items wrap on narrow screens via `flex-wrap`.

### Prefix note / callout

```html
<div class="prefix-note">
  <strong>Prefix key:</strong> ...
</div>
```

- `--surface` bg, `0.5px` all borders, `3px solid --accent` on left
- `border-radius: 0 8px 8px 0` (sharp left, rounded right)
- Use for "read this first" context at top of page

### Header / Footer

- Header: title + subtitle + optional prefix-note, bottom hairline divider
- Footer: centered tip text, top hairline divider, `--text-faint`

## Print

```css
@media print {
  body { background: white; color: black; }
  .container { padding: 1rem; max-width: none; }
  section { break-inside: avoid; page-break-inside: avoid; }
  .grid { gap: 0.75rem; }
}
```

- Full-width layout, tighter gaps, cards stay whole.

## Conventions for new cheatsheets

1. **Copy `tmux.html` as template.** Keep `<style>` block verbatim — design system lives inline for single-file portability.
2. **One `<section>` per topic cluster.** Aim for 6–10 sections total.
3. **Use `dl` for shortcuts / bindings / key-value facts.** Use `.cmd-list` for runs of commands.
4. **Accent sparingly.** Only for the primary anchor (prefix key, most-used command). Don't accent everything.
5. **Subtitle says what / footer says tip.** Header subtitle describes the tool; footer gives one pro-tip.
6. **Lowercase `h1` title.** e.g. `tmux cheatsheet`, `git cheatsheet`. Keeps voice consistent.
7. **File name = `<tool>.html`** at repo root.
