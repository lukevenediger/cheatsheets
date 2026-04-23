# cheatsheets

Personal cheatsheets cooked up from real work. Tools, patterns, gotchas.

Single-file HTML. No build step. Open in any browser or serve as a static site.

## Sheets

- [tmux](tmux.html) — keybindings & commands for the terminal multiplexer
- [zellij](zellij.html) — modal keybindings for the Rust multiplexer
- [tailscale](tailscale.html) — CLI for the WireGuard-based mesh VPN
- [docker](docker.html) — containers, images, volumes, networks, compose
- [agent-browser](agent-browser.html) — browser automation CLI for AI agents

Live: https://lukevenediger.github.io/cheatsheets/

## Design

See [DESIGN_SYSTEM.md](DESIGN_SYSTEM.md) for tokens, components, and conventions. Every cheatsheet follows the same visual language so they print consistently and feel familiar.

## Adding a new cheatsheet

1. Copy `tmux.html` → `<tool>.html`
2. Keep the `<style>` block as-is (the design system is inline)
3. Replace sections with content for the new tool
4. Add a link to `index.html`
5. Add a link to the "Sheets" list in this README
