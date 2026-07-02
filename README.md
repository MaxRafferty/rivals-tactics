# Rivals Tactics

A Marvel Rivals companion app — single-file HTML, no build step. Open `index.html` in a browser.

Rebuilt locally from a claude.ai chat session (transcript in `.claude/Knowledge Base/Marvel Rivals App.txt`).

## Features

- **Squad Builder** — pick your 6 from the full Season 8.5 roster (51 heroes), get live role-balance feedback and warnings (no healer, too many Duelists, etc.).
- **Counter Intel** — build the enemy comp, hit *Lock in comp*, and a tag-based rule engine (dive, shield, healer-stack, sniper, flying, CC, AoE, brawl) surfaces counter-pick suggestions with reasoning. Heroes already in your squad get a ✓. Full-name chips under the slots verify scanned picks at a glance.
- **Ult Watch** — search any hero, track their ultimate with a countdown ring. Duration is editable since exact charge rates shift patch to patch. Card flashes when the ult is back up.
- **Voice input (hands-free)** — click 🎤 once before the match, then just say the enemy heroes out loud ("Venom, Spidey, Luna...") without ever taking your mouse off the game. Understands nicknames (cap, widow, jeff, bucky) and common mishears ("low key" → Loki). Say "remove X", "clear", or "lock it in". Auto-locks at 6 heroes and **reads the counter suggestions back out loud**. Uses the browser's built-in Web Speech API — no API key needed. Works in Edge/Chrome; keep the tab's mic permission allowed.
- **Screenshot scan** (fallback) — snip the hero-select/scoreboard screen (`Win+Shift+S`), press `Ctrl+V` on the page (or upload a file). The image is resized client-side (max 1400px), optionally cropped to the enemy column (Right/Left/Full toggle), and sent to Claude's vision model to auto-fill the picks.

## Screenshot scan setup

Scanning calls the Anthropic API directly from the browser, which requires an API key
(this is separate from a claude.ai Pro/Max subscription):

1. Create a key at [console.anthropic.com](https://console.anthropic.com)
2. Click **⚙ Settings** in the app header and paste it in

The key is stored only in your browser's localStorage. Everything except scanning works without a key.

## Updating the roster

Hero data lives in the `HEROES` array at the top of the `<script>` block in `index.html` —
name, role, and archetype tags (which drive the counter engine). Season 9 (July 10, 2026)
adds **Jubilee** and **The Hood**; add them there when their roles are confirmed.

## Counter engine disclaimer

Suggestions are archetype-based heuristics, not win-rate data. They explain *why*
(e.g. "healer-stacked → dive burst punishes that"), but they're a starting point, not gospel.
