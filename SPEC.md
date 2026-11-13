# CSSOS: a graphical operating system made entirely of CSS

ConsciousNode SoftWorks goof build, a sibling of ToastOS. One self-contained HTML file, MIT licensed, works offline. The fun is in the constraint: **zero JavaScript**, so the stylesheet *is* the operating system.

## The one hard rule
- **No JavaScript of any kind.** No `<script>` tags, no `on*` attributes (`onclick` and friends), no `javascript:` URLs, no WebAssembly, no external files.
- All state lives in HTML form controls (checkboxes, radios, inputs), `<details>`, and the URL `#hash` (`:target`). All behavior comes from CSS selectors, custom properties, `@property`, animations, counters and `calc()`.
- Target current Chromium; using the newest CSS features is encouraged. If something needs another browser, say so.
- Include a self-check line in REPORT.md: the output of searching the file for `<script`, ` on[a-z]+=` and `javascript:`. All three must be empty.

## Prior art: credit it, don't copy it
Lyra Rebane's **x86CSS** (a CSS-only x86 CPU) and **CSS-DOS** (DOS, Windows 1.01 and Doom in CSS) proved CSS can compute. CSSOS is different: there's no emulated CPU, because the OS itself is native CSS. Credit both projects in an "Inspired by" section of REPORT.md and in a footer note in the page. Don't copy their code.

## What to build
1. **Boot.** A boot screen animated purely in CSS (POST lines appearing in sequence, a logo), then the desktop.
2. **Desktop and window manager.** At least 5 app windows, each with open, close and focus/bring-to-front. Pick any CSS technique (`:checked`, `:target`, `:has()`). Windows may snap between preset positions instead of dragging freely; document what you chose.
3. **Taskbar** that shows which apps are open and lets you switch between them.
4. **Filesystem.** A folder tree built from `<details>`/`<summary>`. Files open into a viewer window. Include a README, a few text files and an image drawn in CSS.
5. **Shell.** A terminal window with a text `<input>`. Use `pattern` + `:valid` (or anything else that works without JS) so CSS recognizes typed commands and reveals their output. Support at least 8 commands: `help`, `ls`, `cat readme`, `whoami`, `date`, `uptime`, `clear`, and one secret easter-egg command. Unknown input shows a friendly "command not found".
6. **Clock.** CSS can't read wall-clock time, so build an **uptime clock** that counts hours:minutes:seconds since the page loaded, using animated typed properties or counters. Bonus: also show the uptime in balanced ternary (digits T, 0, 1).
7. **Apps** (at least 4 working ones):
   - **Paint**: a pixel grid of checkboxes with a palette of radio buttons.
   - **Calculator**: digits and + − × ÷ for at least small numbers, built with counters, custom properties and `calc()`.
   - **A game**: Lights Out or tic-tac-toe, with a win screen detected by `:has()`.
   - **Settings**: at least 3 themes that recolor the whole OS.
8. **"Drivers" page.** A cheeky System Information window listing CSSOS's drivers: the mouse driver is `:hover`/`:active`, the keyboard driver is `:focus`/inputs, the display driver is the cascade. Keep it accurate to what you actually used.

## Honesty
- Persistence is impossible without JS. Don't fake saving: say plainly in the UI and the report that nothing survives a reload, except whatever the URL hash carries.
- If a feature can't be done in pure CSS, leave it out and say so in REPORT.md. Never add even one line of JS to make it work.

## Deliver
- `cssos.html`
- `REPORT.md`: what works, what doesn't, which CSS tricks power each part, the no-JS self-check, and the trick you're proudest of.
