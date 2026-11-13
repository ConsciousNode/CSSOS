# CSSOS

**A graphical operating system made entirely of CSS. Zero JavaScript.**

▶ **Try it:** https://consciousnode.github.io/CSSOS/ (current Chrome/Edge)

The stylesheet *is* the OS. Windows open, close, focus and snap through hidden checkboxes and radios plus `:has()`. Files live in `<details>` folders and open through `:target`. The terminal recognizes commands with an input `pattern` and `:valid`. The taskbar clock counts uptime with an animated `@property`, in decimal and **balanced ternary**. Paint is a grid of checkboxes, the calculator is `calc()` plus counters, and Lights Out works out its parity with `mod()`. The file has no `<script>` tag and no event handler anywhere.

![Lights Out solved; uptime 00:00:18 = 0000001T00 in balanced ternary](screenshots/lights-out-and-uptime.png)

Nothing survives a reload except the URL `#hash`. That's honest: there's no storage without JS.

## Things to try (no experience needed)
Download `index.html`, open it in a text editor, change something, save, and reload the page in your browser. You can't break anything that Ctrl+Z won't fix.

1. **Make the whole OS mint green.** Near the top, find the `.os-root {` block and change `--accent: #38bdf8;` to `--accent: #3eb489;`. Every highlight, button and selection follows along. That's *propagation*: change one thing at the root, and everything that depends on it changes too.
2. **Teach the terminal a word.** Find `pattern="help|ls|cat readme|...|toast"` and add `|grue` before the closing quote. Now typing `grue` turns the ✓ green. The pattern is the terminal's vocabulary.
3. **Invent a theme.** Copy the whole `.os-root:has(#theme-vapor:checked) { ... }` block, rename `theme-vapor` to something of your own, and pick new colors. Then copy one `<input type="radio" name="os-theme" ...>` line and one `<label for="theme-vapor" class="theme-card">` card, and rename those too. Your theme now shows up in Settings.
4. **Wonder why it works.** Every window is shown or hidden by a checkbox you never see. Find `#open-paint:checked ~ .desktop #win-paint` and read it out loud: "when the open-paint box is checked, show the paint window." That's the whole trick, repeated a hundred ways.

## Credits
- Idea: Kham, ConsciousNode SoftWorks. Spec: Kehai Interim ([SPEC.md](SPEC.md)).
- Built by Gemini 4 Hydrogen, whose build report is in [REPORT.md](REPORT.md).
- Inspired by Lyra Rebane's [x86CSS](https://lyra.horse/x86css/) and Ahmed Amer's CSS-DOS, which proved CSS can compute. CSSOS has no emulated CPU: the cascade is the kernel.

MIT License.
