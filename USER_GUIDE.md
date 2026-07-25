# Pageforge — User Guide

Pageforge is a desktop app for building web pages visually. You place and style elements on a live canvas, adjust them from a properties panel on the right, and export the result as a single HTML file you can put anywhere — no coding, no build tools, no server required.

This guide walks through the app screen by screen. It's written for people *using* Pageforge to build a page, not for developers working on Pageforge itself (see `README.md` for that).

## Contents

1. [Installing Pageforge](#1-installing-pageforge)
2. [The main window](#2-the-main-window)
3. [Starting a project](#3-starting-a-project)
4. [Selecting and editing elements](#4-selecting-and-editing-elements)
5. [Adding elements: the "+" menu](#5-adding-elements-the--menu)
6. [Resizing by eye](#6-resizing-by-eye)
7. [The properties panel](#7-the-properties-panel)
8. [Undo, redo, and the floating toolbar](#8-undo-redo-and-the-floating-toolbar)
9. [Previewing and exporting your page](#9-previewing-and-exporting-your-page)
10. [Switching language](#10-switching-language)
11. [Tips and troubleshooting](#11-tips-and-troubleshooting)

---

## 1. Installing Pageforge

Download `PageforgeSetup.exe` from the project's GitHub Releases page and run it.

- It will ask where to install (a sensible default is pre-filled — you can just click through).
- It will ask whether to create a desktop shortcut. Leave this checked if you want to launch Pageforge from your desktop afterward.
- Click **Install**. When it finishes, it offers to launch Pageforge right away.

That's it — `PageforgeSetup.exe` is the only file you need to download. It's a self-contained installer; nothing else needs to be extracted or copied by hand.

If you'd rather look at or modify the raw source code instead of using the installer, a separate plain `.zip` of the source is also available — see `README.md`.

## 2. The main window

When Pageforge opens, you'll see three areas:

- **Left sidebar** — a project explorer (currently informational) and a component list, plus the language switch (EN/ES) and a settings button (⚲) at the top.
- **Center — the canvas** — this is your page. Whatever you see here is what gets exported.
- **Right sidebar — the inspector** — properties for whichever element is currently selected. Empty until you click something on the canvas.

The top bar above the canvas has undo/redo arrows, the breakpoint switch (Desktop/Tablet/Mobile — see [section 7.4](#74-responsive)), and **Preview**/**Export** buttons.

## 3. Starting a project

The first thing you'll see is a start screen with a template picker:

- **Blank** — start from nothing.
- **Simple landing page** — headline, text, and a call-to-action button.
- **Basic portfolio** — a header and a project grid.
- **Blog** — a header and a list of posts.
- **Simple store** — a header and a product grid.
- **Résumé** — name, experience, and skills.

Pick one, set the canvas width and background color if you want to change them from the defaults (you can always change these later from the ⚲ settings button), and click through to start editing. Templates are just a starting point — everything they contain is regular, fully editable canvas elements.

## 4. Selecting and editing elements

Click any element on the canvas to select it — you'll see an accent-colored outline around it, and its properties appear in the right-hand inspector.

- **Reordering**: for normal (non-absolute, non-fixed) elements, click and drag to reorder them among their siblings — a placeholder line shows where it'll land.
- **Free positioning**: elements set to *Position: Absolute* or *Fixed* (see [Layout](#71-text-layout--spacing)) can be dragged anywhere on the canvas; the cursor turns into a move icon over them.
- **Editing text**: select a text element and type directly into the **Content** field in the Text section of the inspector — this is safer than trying to click and type in-place, since some element types don't have a single editable text block.
- **Escape** clears the current selection.

## 5. Adding elements: the "+" menu

Click the **+** button in the floating toolbar at the bottom of the canvas to insert a new element. You can choose from:

Text, Button, Image, Color box, Container, Form, Card, Label, Code, Divider.

Multi-piece presets (Form, Card, Label) insert several elements at once, each individually selectable and editable — a Card, for instance, gives you an image, a title, a description, and a button, all as separate elements you can restyle independently. Image placeholders (Image, Card, Label, and the Portfolio/Store template slots) are real `<img>` elements from the start, not styled boxes, so clicking one immediately gives you the full Image section — upload, crop, filters, and so on.

**Label** is an image next to a short piece of text, meant for things like a small profile blurb, an icon-with-caption, or a feature bullet. By default the text sits to the right of the image — see [Content layout](#71-text-layout--spacing) below for how to move it to the other three sides instead.

**Code** is a raw HTML/CSS/JS block — see [section 7.6](#76-code) below.

## 6. Resizing by eye

Instead of typing pixel values, you can resize the selected element directly on the canvas: 8 small square handles appear all around it (on every edge and corner) once it's selected — drag any of them to change its size.

- **Elements set to Position: Absolute or Fixed** can move their anchor point too — dragging a top or left handle resizes *and* repositions the element in one motion, the same way it would in Figma or Framer.
- **Normal-flow and Sticky elements** don't have a fixed top-left point to move (their position comes from the page layout, not a coordinate), so dragging a top or left handle on one of these only resizes it — the box grows away from that edge instead of visually following the cursor. Still useful, just not perfectly cursor-tracking on those two edges.

This is a shortcut for the same width/height/position fields in the Layout section — either method updates the same underlying styles, so you can mix and match (drag roughly into place, then fine-tune the exact pixel value in the inspector, or vice versa).

Resize handles are only available while previewing the **Desktop** breakpoint. Switch to Tablet or Mobile to work on responsive overrides instead (see below) — dragging a handle there would be ambiguous about whether you meant to change the base Desktop size or just this size's override, so it's disabled and the inspector's Responsive fields are the way to do that instead.

## 7. The properties panel

The inspector is organized into collapsible sections. Which ones you see depends on what kind of element is selected (an image, for instance, shows an **Image** section instead of **Text**).

### 7.1 Text, Layout & Spacing

- **Text** — the element's content, font (including a curated set of Google Fonts — picking one downloads and applies the real typeface), size, color, weight, bold/italic/underline/strikethrough, alignment, line height, and capitalization (uppercase/lowercase/title case).
- **Image** (replaces Text for `<img>` elements) — upload an image from your computer (it's embedded directly into the page, so it still works once exported — no broken links), or paste an external URL instead. Also: crop, filters (black & white, contrast, saturation, sepia, darken), how the image fits its box (cover/contain/fill/etc.), alt text, and directional or radial fade-out.
- **Layout** — size mode for width/height (Hug the content, Fixed pixel value, or Fill the available space); position (Inline in the normal flow, Absolute/free-floating, Fixed to the browser window, or Sticky — sticks in place once scrolling passes a chosen offset from the top); and content layout, in either of two modes:
  - **Flex** — row/column direction, a **Reverse order** toggle (combine with direction to place children on any of the 4 sides — e.g. a Label's text right, left, below, or above its image), gap, alignment, and justification.
  - **Grid (Cuadrícula)** — a column count (rows are created automatically as needed), gap, and align/justify items. To make a specific child span more than one column or row, select *that* child and use its own Layout section's "Grid position" fields — grid placement is a property of the item, not the container.
- **Spacing** — padding and margin, with a mode switch (None / All sides equal / separate X-and-Y / fully individual per side).

### 7.2 Appearance

- **Background** — solid color, gradient (linear or radial), or a repeating pattern (stripes, dots, grid).
- **Border** — solid or gradient border, with radius (rounded corners).
- **Shadow** — layered box shadows, with quick presets.
* **Frosted glass** — glassmorphism: a translucent, blurred background.
- **Hover transition** — define what changes when the mouse hovers the element in the exported page (pure CSS, no JavaScript).

### 7.3 Animation

A keyframe timeline, similar to a simplified Premiere Pro: independent tracks for position, X/Y scale, rotation, opacity, color, and a glow/trail effect, with a draggable playhead and a live preview as you scrub. A one-click effect library covers common cases without hand-building keyframes: bounce, zoom in, shake, attention pulse, slide up, stretch-and-move, and trail-and-slide-in. Animations can autoplay on export or be triggered from Logic (see below, the "Play animation" action).

### 7.4 Responsive

Pick **Tablet** or **Mobile** from the switch in the top bar (next to Undo/Redo) to preview and edit how the page looks at that size — the canvas itself narrows to match. While a non-Desktop size is active, the Responsive section on any selected element lets you:

- **Hide at this size** — the element disappears at this breakpoint only.
- **Stack vertically** — for flex containers, switch their children from a row to a column at this size.
- **Override width** / **Override text size** at this size specifically.

These overrides never change how the element looks on Desktop — they're layered on top, only active at that breakpoint, both in the editor's preview and in the exported page (which gets real CSS `@media` rules generated for it). Switch back to **Desktop** at any point to keep editing the base version normally.

### 7.5 Logic

No-code interactivity: **when** (a trigger) → **do** (an action) → optionally **to** (a target element). Triggers include click, double-click, mouse enter/leave, page load, scrolling into view, a specific key press, or a timer/delay. Available actions include showing/hiding elements, changing a style or CSS class, playing an animation, scrolling to another element, focusing a field, incrementing a counter, opening a URL, showing an alert, copying text to the clipboard, submitting/resetting a form, logging to the console, running a countdown to a date, remembering/recalling a value between visits (stored in the visitor's browser), and calling an API over HTTP (see below). Rules compile down to plain JavaScript in the exported page — nothing runs while you're still editing on the canvas.

#### Connecting your page to a backend (Python, C#, or anything else)

The **"Call an API (HTTP)"** action is a deliberately simple bridge between your exported page and a program running anywhere else — a local script, a desktop app, a server, whatever you're building. It works with *any* language, because the only requirement on the other end is that it can speak HTTP.

The action's fields:

- **URL** — where to send the request, e.g. `http://localhost:8000/greet`.
- **Method** — GET, POST, PUT, PATCH, or DELETE.
- **Body** — optional, sent as-is (ignored for GET). Usually a JSON string, e.g. `{"name": "Ada"}`.
- **Target** — which element (usually itself, or another element by name) should show the result.
- **On response** — what to do with whatever comes back: do nothing, put it as the target's text, put it as the target's value (for form fields), or just log it to the browser console.

This exports as a plain `fetch()` call — nothing pywebview- or Pageforge-specific, so the exported page still works as a completely standalone `.html` file. You only need something listening on the other end while you're actually using that button.

**A five-line server in Python**, using only the standard library (no install needed):

```python
from http.server import BaseHTTPRequestHandler, HTTPServer

class Handler(BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.send_header("Content-Type", "text/plain")
        self.send_header("Access-Control-Allow-Origin", "*")  # needed for the browser to accept the response
        self.end_headers()
        self.wfile.write(b"Hello from Python!")

HTTPServer(("localhost", 8000), Handler).serve_forever()
```

**The equivalent in C# (.NET)**, using `HttpListener`:

```csharp
using System.Net;

var listener = new HttpListener();
listener.Prefixes.Add("http://localhost:8000/");
listener.Start();

while (true)
{
    var ctx = listener.GetContext();
    ctx.Response.AddHeader("Access-Control-Allow-Origin", "*");
    var bytes = System.Text.Encoding.UTF8.GetBytes("Hello from C#!");
    ctx.Response.OutputStream.Write(bytes, 0, bytes.Length);
    ctx.Response.Close();
}
```

A couple of things worth knowing:

- **CORS**: browsers block a page from reading a response from a different origin unless the server explicitly allows it — that's what the `Access-Control-Allow-Origin` header above is for. Without it, the request still reaches your server, but the browser hides the response from the page.
- This is one-directional per click: the page calls your server when the trigger fires. If you need your backend to push updates to the page on its own (without the visitor clicking anything), that's a different, more involved pattern (WebSockets/Server-Sent Events) that this simple action doesn't cover.
- Since this compiles to a real `fetch()` call, anyone who views the page's source can see the URL it calls — don't rely on it for anything that needs to stay secret (API keys, etc.).

### 7.6 Code

Available on the **Code** preset (see [section 5](#5-adding-elements-the--menu)): three plain-text fields — HTML, CSS, and JavaScript — for anything the visual controls don't cover. This is unmanaged and unscoped, the same idea as Webflow's "Embed" element: whatever you write is exactly what ends up in the page, so it's on you to keep it valid and to scope your own CSS selectors if you don't want them affecting the rest of the page.

- **HTML and CSS preview live** on the canvas as you type, so you can see roughly what it'll look like while you work.
- **JavaScript never runs while editing** — only once you Preview or Export. This is deliberate: letting arbitrary hand-written JS run during editing could interfere with selecting or dragging elements elsewhere on the canvas.

### 7.7 Advanced

Custom HTML attributes (for anything not covered by a dedicated field), and a button to export just the current selection as its own standalone snippet.

## 8. Undo, redo, and the floating toolbar

- **Undo/Redo** — the ↩/↪ buttons in the top bar, or Ctrl+Z / Ctrl+Y.
- **Floating toolbar** (bottom of the canvas, appears once something is selected) —
  - **+** insert a new element
  - **⧉** duplicate the selected element
  - **◰** wrap it in a container
  - **⊘** show/hide it (stays selected while hidden, so the same button un-hides it)
  - **✕** delete it

## 9. Previewing and exporting your page

- **Preview** opens the page as it currently stands in your system browser — a genuine rendering test, not a simulation.
- **Export** saves a single self-contained `export.html` file: all your styling, images (embedded), animations, hover effects, responsive rules, and Logic interactions included, no external files needed except, optionally, Google Fonts if you used any (those load from Google's CDN, so an internet connection is needed for those specifically — everything else works completely offline).

## 10. Switching language

The **EN/ES** toggle at the top of the left sidebar switches the entire interface between English and Spanish instantly — nothing about your page's content changes, only the editor's own UI.

## 11. Tips and troubleshooting

- **Element seems "stuck" and won't reorder** — check whether it's set to *Position: Absolute* in Layout; absolute elements move freely instead of reordering among siblings.
- **A Google Font isn't showing up** — Google Fonts need an internet connection to download, both in the editor and once the page is exported and opened.
- **Made a mess of an animation or Logic rule** — each section that supports it has a plain "remove" option; you don't need to undo one field at a time.
- **Want to reuse just one element elsewhere** — select it and use **Export selection** in the Advanced section instead of exporting the whole page.
