# CSSOS — Technical Report

**ConsciousNode SoftWorks** · MIT License · Zero JavaScript · Offline Self-Contained (`cssos.html`)

## 1. No-JS Self-Check

Output of searching `cssos.html` for `<script`, ` on[a-z]+=`, and `javascript:`:

```text
$ grep -inE '<script' cssos.html
(empty)

$ grep -inE ' on[a-z]+=' cssos.html
(empty)

$ grep -inE 'javascript:' cssos.html
(empty)
```

All three checks return zero matches.

## 2. What Works

| Subsystem | Implementation & CSS Mechanism |
| :--- | :--- |
| **Boot Sequence** | `@keyframes boot-line-in`, `boot-bar-fill`, and `boot-fade-out` reveal 6 POST lines and a logo before fading into the desktop; a `#skip-boot:checked` checkbox bypasses POST immediately. |
| **Desktop & Window Manager** | 8 app windows controlled by hidden `#open-*` checkboxes (open/close), `#focus-*` radios + `:focus-within` (`tabindex="0"`) for bring-to-front `z-index`, and `#snap-*` radios (`:has()`) for 4 preset positions (Default, Left Half, Right Half, Maximize). |
| **Taskbar & Start Menu** | Taskbar buttons stay hidden until `#open-*:checked` (or `.viewer-doc:target`) and highlight on `#focus-*:checked`. Start Menu toggles via `#start-menu-open:checked`. |
| **Filesystem & File Viewer** | `<details>` / `<summary>` folder tree in Files; clicking any file sets the URL `#hash`, activating `.viewer-doc:target` and opening `#win-viewer` via `.os-root:has(.viewer-doc:target)`. Includes `README.md`, `manifesto.txt`, `drivers.txt`, `.hidden_note.txt`, and `sunset.cssimg` (drawn with CSS gradients and borders). |
| **Shell (`cssh`)** | Text `<input>` with `required pattern="help\|ls\|cat readme\|whoami\|date\|uptime\|clear\|toast"` validates commands in real time (`:valid` vs `:invalid:not(:placeholder-shown)` for `"cssh: command not found"`), paired with 8 radio command chips for output switching (`toast` is the secret easter egg). |
| **Uptime Clock & Balanced Ternary** | `@property --up-sec` (`<integer>`) animated with `steps(86400, end)` drives `HH:MM:SS` via `mod()`, `round(down, ...)`, and `counter(..., decimal-leading-zero)`, plus a live 10-trit balanced ternary (`T, 0, 1`) readout. |
| **Paint** | 12×12 grid of 144 `<input type="checkbox">` pixels inside a `<form>` (so `<button type="reset">` clears the canvas), 5-color radio palette, and a round/square pixel toggle. |
| **Calculator** | Radio buttons for Operand A (`0–9`), Operator (`+`, `−`, `×`, `÷`), and Operand B (`0–9`) wired to `--a`, `--b`, `calc()`, `round(down, ...)`, and `counter()` — including `ERR: DIV / 0` detection via `:has(#cb-0:checked):has(#cop-div:checked)`. |
| **Lights Out (3×3)** | 9 move checkboxes (`#lo-1`..`#lo-9`) compute each cell's GF(2) parity using `mod(calc(...), 2)` so clicking a tile flips itself and its orthogonal neighbors. Win screen is detected purely by `:has()` matching the unique 4-move solution (`{1, 3, 5, 8}`). |
| **Settings (Themes)** | 4 radio themes (**Nordic Dark**, **CRT Amber**, **95 Classic**, **Vaporwave**) override CSS custom properties on `.os-root:has(#theme-*:checked)` to recolor the entire OS. |
| **Drivers / System Info** | Lists the actual CSS mechanisms powering Pointer (`:hover`/`:active`), Keyboard (`:focus`/inputs), Display (the cascade), Window Bus (`:checked`/`:target`/`:has()`), Clock (`@property`), Storage (volatile DOM), and Audio (offline). |

## 3. What Doesn't Work (Honest CSS Limitations)

- **Persistence:** Zero JavaScript means zero `localStorage` or `IndexedDB`. Nothing survives a page reload except the URL `#hash` (`:target` for the File Viewer).
- **Single-Input Shell Output Routing:** CSS `:valid` is a 1-bit boolean per `<input>`, and CSS selectors cannot read live typed `.value` strings (`[value="..."]` only matches the initial HTML attribute). The text `<input>` genuinely validates all 8 commands vs. `"command not found"`, while radio chips select which command's output buffer is shown.
- **Per-Pixel Color Memory in Paint:** Each checkbox stores 1 bit (`:checked` or not), so switching the active palette color recolors all currently checked pixels rather than storing independent per-pixel colors.
- **Free Window Dragging & Wall-Clock RTC:** CSS cannot track arbitrary pointer drag deltas across frames (windows snap between 4 preset geometries instead) and cannot read the system wall-clock date/time (`date` notes this honestly; `uptime` counts from page load).
- **Browser Support:** Targets modern **Chromium** (Chrome 125+ / Edge 125+) for `mod()`, `round(down, ...)`, `@property <integer>`, and `:has()`. Older browsers without CSS Values Level 4 math (`mod`/`round`) will not render the clock, division, or Lights Out parity correctly.

## 4. The Trick I'm Proudest Of

The **live Balanced Ternary (`T, 0, 1`) Uptime Clock** computed every second in pure CSS:

1. `@property --up-sec` animates an `<integer>` from `0` to `86400` using `steps(86400, end)`.
2. For each trit $k \in [0, 9]$, CSS computes:
   $$\text{trit}_k = \left(\left\lfloor \frac{\text{sec} + (3^k - 1)/2}{3^k} \right\rfloor \bmod 3\right) + 1$$
   using `round(down, ...)` and `mod(..., 3)`.
3. A custom `@counter-style btrit { system: cyclic; symbols: "0" "1" "T"; }` maps `1 → "0"`, `2 → "1"`, and `3 → "T"`, rendering a live ticking balanced-ternary clock in `::after` `content:` with zero JavaScript.

## 5. Inspired By

- Lyra Rebane's [x86CSS](https://lyra.horse/x86css/) ([GitHub](https://github.com/rebane2001/x86CSS)) — a working CSS-only 8086 CPU emulator.
- Lyra Rebane's **CSS-DOS** — DOS, Windows 1.01, and Doom in CSS.

CSSOS takes a complementary path: instead of emulating an x86 CPU inside stylesheets, the stylesheet *is* the operating system.
