# Pageforge

A desktop visual HTML page editor: click, drag, and edit elements on a live canvas, tune their properties from a Figma/Framer-style panel, and export the result as a single self-contained HTML file — no frameworks, no build step, no backend.

Built with Python ([pywebview](https://pywebview.flowrl.com/)) for the desktop window, and plain HTML/CSS/JavaScript for the whole editor. The interface is available in English and Spanish (switch with the EN/ES toggle in the sidebar).

## Features

**Direct on-canvas editing**
- Click to select, drag to reorder, free-drag for absolutely-positioned elements.
- Resize by eye: drag handles on the selected element's edges/corners (all 8 for absolutely-positioned elements, 3 for normal-flow ones) instead of typing pixel values.
- Undo / redo.
- Hide/show, duplicate, wrap, and delete elements from a floating toolbar.
- "+" menu with element presets: text, button, image, color box, container, form, card, label (image + text, either side of it — see Layout's "Reverse order" below), code (raw HTML/CSS/JS escape hatch), divider.

**Properties panel**
- **Text** — font (includes a curated selection of Google Fonts), size, weight, color, alignment, line height, capitalization.
- **Layout** — size (hug/fixed/fill); position (inline, absolute, fixed, or sticky — fixed/absolute are free-draggable on the canvas); content layout as either Flex (direction + a reverse-order toggle, so a row/column container's children can sit on either end — e.g. a Label's text left, right, above, or below its image) or Grid (column count, gap, align/justify items, plus per-child column/row span).
- **Code** — an escape hatch for raw HTML/CSS/JS on any block, for anything the visual controls don't cover. HTML/CSS preview live on the canvas; JS only ever runs in the exported/previewed page, never while editing.
- **Responsive** — preview and edit at Tablet/Mobile breakpoints from a switch in the top bar; per-element overrides (hide, stack, width, text size) that compile to real `@media` rules on export without touching the Desktop styles.
- **Spacing** — padding and margin, with none/all/X & Y/individual modes.
- **Appearance** — solid, gradient, or pattern (stripes, dots, grid) background; solid or gradient borders; layered shadows; frosted glass (glassmorphism); CSS hover transitions.
- **Image** — upload from your computer (embedded as part of the exported file itself), drag-to-crop, filters (black & white, contrast, saturation, sepia, brightness), object-fit, directional or radial fade.
- **Animation** — a Premiere-Pro-style keyframe timeline with independent tracks per property (position, scale X/Y, rotation, opacity, color, glow/trail), a draggable playhead with a live preview, and a one-click effect library (bounce, zoom in, shake, attention pulse, slide up, stretch and move, trail and slide inward).
- **Logic** — no-code interactions (trigger → action → target): click, double click, mouse enter/leave, on load, on scroll into view, key pressed, timer. 20+ actions: show/hide, change styles, toggle classes, play animations, scroll, counters, forms, remember/recall values across visits, call any HTTP backend (Python, C#, or anything else — see `USER_GUIDE.md`), and more.
- **Advanced** — custom attributes, export the current selection.

See `USER_GUIDE.md` for a step-by-step walkthrough aimed at people using Pageforge to build a page (as opposed to this README, which is aimed at people working on Pageforge itself).

**Start and export**
- Start screen with templates (blank, landing, portfolio, blog, store, résumé) and canvas setup.
- Preview in the system browser and export to a single self-contained `.html` file — no external dependencies except, optionally, any Google Fonts used.

## Getting started

Requires Python 3.9+.

```bash
pip install -r requirements.txt
python main.py
```

## Project structure

```
main.py                  Desktop window and native bridge (save/export files)
web/
  index.html              Interface structure
  styles.css               Styles (dark theme, editor components)
  app.js                    Startup, orchestration, and exported-HTML generation
  controls/                 Reusable form controls (color, number, text, toggle, select)
  editor/
    i18n.js                  Translation dictionary + language switching
    registry.js, renderer.js, selection.js, binder.js, inspector.js
                             Properties panel and its rendering engine
    canvas.js                Canvas: selection, dragging, element insertion
    history.js                Undo / redo
    logic.js                  No-code interaction system
    animation.js               Keyframe animation
    hover.js                    CSS hover transitions
    fonts.js                     Google Fonts integration
    imageCrop.js                  Image cropping tool
    settings.js, startScreen.js    Project settings and start screen
    utils.js                        Misc utilities
tools/
  build_installer.py       Builds the single-file installer (see below) — the recommended GitHub release download
  installer_app.py          Source of the installer's desktop GUI (Tkinter), embedded by build_installer.py
  pack.py                  Builds a deduplicated, minified archive of the source (see below)
  unpack.py                 Reconstructs the project tree from that archive, and can build Pageforge.exe from it
```

## Release packaging

**`tools/build_installer.py` is what should be uploaded to GitHub Releases.** It's a two-stage build:

1. Copies the source (`main.py` + `web/`) to a temp folder, minifying JS/CSS on the way (via `rjsmin`/`rcssmin`, installed automatically if missing) and HTML with a small dependency-free minifier, and compiles it into `Pageforge.exe` with [PyInstaller](https://pyinstaller.org/) (also installed automatically if missing).
2. Embeds that `Pageforge.exe` inside a small Tkinter installer (`tools/installer_app.py`) and compiles *that* into `PageforgeSetup.exe`.

The result is a **single file**. Whoever downloads `PageforgeSetup.exe` just runs it — no separate archive to extract, nothing to unzip by hand. It asks for an install folder (with a sensible default and a "Browse..." button) and whether to create a desktop shortcut, then copies the embedded `Pageforge.exe` there and creates the shortcut with it if asked (via PowerShell/`WScript.Shell`, no extra dependencies needed). What you end up with, either way, is `Pageforge.exe` sitting in the folder you chose.

```bash
python tools/build_installer.py    # builds dist/PageforgeSetup.exe
```

PyInstaller doesn't cross-compile — run this on Windows to get a real `PageforgeSetup.exe`/`Pageforge.exe`. Running it on Linux/macOS instead produces native binaries for that platform (useful only for testing the embed/install mechanism, not for actual distribution).

The raw, human-readable source code is separately available as a plain `.zip` for anyone who wants to browse or modify it directly. `tools/pack.py`/`tools/unpack.py` still exist as a lighter-weight alternative — a deduplicated, minified `.bin` of just the source (see the tools themselves for details) — for anyone who wants that instead of a full installer.

## License

This project uses a custom "source-available" license — see [`LICENSE.md`](./LICENSE.md). In short: you can use, modify, and republish it non-commercially, as long as you share the source of your changes and don't claim original authorship. Commercial use isn't allowed.
