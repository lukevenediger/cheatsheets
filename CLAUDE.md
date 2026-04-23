# CLAUDE.md

Repo: personal single-file HTML cheatsheets. No build step. Deployed to GitHub Pages on push to `main` via `.github/workflows/pages.yml`.

## Workflow

- **Always commit and push when changes are complete.** Don't wait to be asked. User expects a clean working tree at end of every task.
- **Stay on `main`.** No branches, no PRs — this is a solo content repo.
- **Commit message style:** `<Verb> <what>` (imperative, no prefix/scope). Examples from history: `Add SVG favicon with stacked cards motif`, `Add agent-browser cheatsheet with Claude skill setup and screenshot tips`, `Add hover lift and glow to index cards`. Keep subject one line. Body rarely needed.
- **Always include co-author trailer** (as set up by global instructions): `Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>`.
- **Never** use `--no-verify`, `--amend`, `push --force`, or create public repos (user rule: all repos `--private`).

## Adding a new cheatsheet

When adding a new sheet, update **all** of these in one commit:

1. Create `<tool>.html` at repo root. Copy `tmux.html` or `zellij.html` as the template — keep the `<style>` block verbatim (design system is inline).
2. Link the favicon in `<head>`: `<link rel="icon" type="image/svg+xml" href="favicon.svg">` directly after `<title>`.
3. Add a card to `index.html` inside `<ul class="grid">` — name, one-line description, four top commands as `dl` rows.
4. Add a bullet to the `## Sheets` list in `README.md`.
5. Commit + push.

If any of steps 2–4 are missed, the sheet is orphaned.

## Design system

`DESIGN_SYSTEM.md` is the source of truth for tokens, components, layout. Key points:

- Tokens are CSS custom properties on `:root` with a `prefers-color-scheme: dark` override — **auto dark mode works out of the box**. Don't add a theme switcher.
- Accent color: `#c96442` (light) / `#d97757` (dark). Terracotta. Use sparingly — one anchor per sheet.
- Sections: 6–10 per sheet. One topic per `<section>`. Use `<dl>` for key-value (shortcuts, bindings) and `.cmd-list` for runs of `<code>` commands.
- Titles are **lowercase** (`tmux cheatsheet`, not `Tmux Cheatsheet`).
- `<kbd class="prefix">` for prefix keys (accent color). Plain `<kbd>` for regular keys. `<span class="plus">+</span>` between chorded keys.
- Wide section spanning full grid row: add `class="wide"` with `grid-column: 1 / -1` (see `agent-browser.html` screenshots section).
- Hairline borders (`0.5px`) everywhere. Don't thicken.
- Print CSS already handled — don't add page breaks.

## Favicon

`favicon.svg` — three stacked rounded cards, accent-orange top card with three text rows. SVG only (modern browsers). Already linked from every HTML file; keep it linked when adding new sheets.

## Deployment

- `.github/workflows/pages.yml` builds + deploys on push to `main`.
- Live at <https://lukevenediger.github.io/cheatsheets/>.
- No staging, no preview — push is publish.

## Header meta row

Every sheet's `<header>` should include a `.meta` row with at minimum:

```html
<span><span class="label">Home</span><a href="...">tool-home</a></span>
<span><span class="label">Install</span><code>brew install tool</code></span>
```

Add more meta items (Docs, Console, Then, etc.) when useful. This was added in commit `2f12ebc`.
