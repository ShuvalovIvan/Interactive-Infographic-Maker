# Interactive Infographic Builder

A browser-based tool for creating interactive infographics — draw clickable zones on any image and attach customizable hoverboxes with rich HTML content. No dependencies, no build step, just one HTML file.

![License](https://img.shields.io/badge/license-MIT-blue)
![No Dependencies](https://img.shields.io/badge/dependencies-none-brightgreen)

---

## Table of Contents

- [Quick Start](#quick-start)
- [Features Overview](#features-overview)
- [How to Use](#how-to-use)
  - [Getting Started](#getting-started)
  - [Drawing Zones](#drawing-zones)
  - [Editing Zones](#editing-zones)
  - [Moving & Duplicating](#moving--duplicating)
  - [Multi-Select, Merge & Disconnect](#multi-select-merge--disconnect)
  - [Customizing Hoverboxes](#customizing-hoverboxes)
  - [Hoverbox Positioning](#hoverbox-positioning)
  - [HTML/CSS Code Editor](#htmlcss-code-editor)
  - [Pulse Effect](#pulse-effect)
  - [Zone Visibility](#zone-visibility)
  - [Preview Mode](#preview-mode)
  - [Saving Your Work](#saving-your-work)
  - [Exporting](#exporting)
- [Keyboard Shortcuts](#keyboard-shortcuts)
- [Deploying to GitHub Pages](#deploying-to-github-pages)
- [Embedding in WordPress](#embedding-in-wordpress)
- [Storage Backends](#storage-backends)
- [Browser Support](#browser-support)

---

## Quick Start

1. Download or clone this repository.
2. Open `index.html` in any modern browser — that's it.
3. Upload a background image, draw zones, customize hoverboxes, and export.

No server, no install, no build tools required.

---

## Features Overview

- **Three shape tools** — Polygon (click-to-place), Rectangle, and Oval (click-and-drag)
- **Fully editable zones** — Drag points to reshape, double-click edges to add points, right-click points to remove them
- **Move & duplicate** — Drag entire zones to reposition; Ctrl+D to duplicate
- **Multi-select** — Shift+click to select multiple zones for batch operations
- **Merge & disconnect** — Combine multiple zones into one multi-part zone, or split them back apart
- **Rich hoverboxes** — Customize colors, border radius, and write raw HTML/CSS for title and description
- **Hoverbox positioning** — Follow the cursor or pin to a fixed location on the image
- **No-color zones** — Make zones completely invisible (useful for clean overlays)
- **Autosave** — Works on Claude, GitHub Pages, and local development (IndexedDB → localStorage fallback)
- **Project files** — Save/load `.json` project files for portability and backups
- **One-file export** — Export a standalone `.html` file with everything embedded, ready to host

---

## How to Use

### Getting Started

1. Click **Image** in the toolbar (or drag-and-drop an image onto the canvas).
2. Your image appears centered on the canvas and serves as the background for your infographic.

### Drawing Zones

Select a shape tool from the toolbar:

| Tool | How to Draw |
|------|-------------|
| **Poly** | Click to place each vertex. Double-click or press **Enter** to close the shape. Right-click to undo the last point. |
| **Rect** | Click and drag from one corner to the opposite corner. Release to create. |
| **Oval** | Click and drag to define the bounding box. Release to create. |

Press **Esc** at any time to cancel the current drawing.

After drawing, the zone editor modal opens automatically so you can configure the hoverbox.

### Editing Zones

Once a zone is created, click it to select it. While selected:

- **Drag any vertex point** to reshape the zone (a grab cursor appears within the buffer zone around each point).
- **Double-click on an edge** to insert a new point at that location (cursor changes to a crosshair cell).
- **Right-click a point** to delete it (minimum 3 points per part).
- Press **Delete** to remove the selected zone entirely.
- Click the **Edit** button in the sidebar to reopen the zone editor modal.

### Moving & Duplicating

- **Move** — Click and drag anywhere inside a selected zone's filled area to reposition the entire zone. All points (and the fixed hoverbox pin, if set) move together. Works with multi-selected zones too.
- **Duplicate** — Three ways:
  - Press **Ctrl+D** (or **Cmd+D** on Mac) to duplicate all selected zones.
  - Click the **Duplicate** button in the sidebar action bar.
  - Click the **Dup** button on any individual zone in the sidebar list.

Duplicates appear offset 20px down-right from the original and are automatically selected.

### Multi-Select, Merge & Disconnect

- Hold **Shift** and click zones (on the canvas or in the sidebar) to select multiple zones.
- **Merge** — When 2+ zones are selected, a **Merge** button appears. This combines all selected zones into a single multi-part zone sharing one hoverbox. The first zone's properties (title, colors, etc.) are preserved.
- **Disconnect** — When a multi-part zone is selected, a **Disconnect** button appears. This splits it back into individual zones, each inheriting the original's properties.

### Customizing Hoverboxes

Click **Edit** on any zone to open the editor modal. You can configure:

| Setting | Description |
|---------|-------------|
| **Title** | The heading displayed in the hoverbox |
| **Description** | The body text displayed in the hoverbox |
| **Zone Color** | The highlight color shown over the zone area |
| **Zone Opacity** | How transparent the zone highlight is (0–100%) |
| **Hoverbox BG** | Background color of the hoverbox popup |
| **Hoverbox Text** | Text color inside the hoverbox |
| **Border Radius** | Roundness of the hoverbox corners (0–40px) |

### Hoverbox Positioning

Each zone's hoverbox can be set to one of two modes:

- **Follow cursor** (default) — The hoverbox follows the mouse pointer and repositions automatically to stay within bounds.
- **Fixed position** — The hoverbox appears at a specific location on the image. When selected:
  - Enter X/Y coordinates manually in image pixels.
  - Or click **Pick on canvas** — the modal hides and a crosshair appears. Click anywhere on the canvas to place the hoverbox. Press **Esc** to cancel.
  - A orange pin icon appears on the canvas in edit mode showing where the hoverbox will appear.
  - The pin moves with the zone when dragged and offsets correctly when duplicated.

### HTML/CSS Code Editor

Both the Title and Description fields have three tabs:

- **Visual** — Plain text input (default). Simple and quick.
- **HTML** — A code editor where you can write raw HTML with inline CSS. When this field is not empty, it overrides the Visual tab content. Example:
  ```html
  <h3 style="color: gold; font-family: Georgia; font-size: 18px;">
    Historic District
  </h3>
  ```
- **Preview** — Renders your HTML live so you can see exactly what it will look like.

This lets you fully control the typography, layout, colors, and formatting of each hoverbox.

### Pulse Effect

Zones can have an animated pulse glow to draw attention and signal interactivity. In the zone editor, under the **Pulse Effect** section:

- Click the **Pulse** toggle to enable/disable the effect.
- **Color** — The glow color. Use white for a universal shimmer, or match your design palette.
- **Speed** — How fast the pulse cycles: Slow (3s), Medium (2s), Fast (1s), or Rapid (0.6s).
- **Intensity** — How bright the glow gets at its peak: Subtle (15%), Medium (30%), Strong (50%), or Bright (70%).
- A live **preview** animates in the modal showing the actual radial gradient effect, including a zone outline hint so you can see whether the glow is contained or spilling.

The pulse is visible in both Edit and Preview modes in the builder, and exports cleanly to the final HTML file. Contained pulses use SVG `<clipPath>` elements to restrict the glow, while spill pulses use unclipped `<circle>` elements that radiate freely. The animation is pure CSS — no JavaScript needed for the effect in the exported file. The pulse automatically pauses when the user hovers over the zone.

Pulse works with all zone types including "No Color" zones — an invisible zone with a contained pulse creates a subtle inner glow, while an invisible zone with spill creates a mysterious floating light effect.

The sidebar marks pulsing zones with ✨glow or ✨spill.

### Zone Visibility

- By default, zones are semi-transparent with a colored fill in the editor.
- Click **No Color** in the zone editor to make a zone completely invisible. In the editor, invisible zones show a dashed outline and points so you can still work with them. In preview and the exported file, they are truly invisible — only the hoverbox appears on hover.
- The sidebar marks invisible zones with an "invisible" label.

### Preview Mode

Click **Preview** in the toolbar to test your infographic as users will see it:

- The sidebar hides for a full-width view.
- Zones are invisible by default (no highlight until hovered).
- Hover over zones to see hoverboxes appear with your configured styles and content.
- Click **Edit** to return to the editor.

### Saving Your Work

The builder offers multiple ways to save:

| Method | How | Where It Works |
|--------|-----|----------------|
| **Autosave** | Triggers 1.5s after any change | Everywhere (Claude, GitHub Pages, local) |
| **Autosave button** | Forces an immediate save | Everywhere |
| **Save .json** | Downloads a portable project file | Anywhere — share, backup, or move between machines |
| **Load .json** | Imports a previously saved project file | Anywhere |
| **Reset** | Clears all data (with confirmation) | Everywhere |

The save status indicator in the toolbar shows:
- 🟢 **Saved** — All changes persisted
- 🟡 **Saving...** — Write in progress
- ⚪ **Unsaved** — Changes pending

A small badge next to the indicator shows which storage backend is active (IndexedDB, localStorage, or Claude Storage).

### Exporting

Click **Export** to download a standalone `infographic.html` file:

- The background image is embedded as base64 (no external files needed).
- All zones are rendered as invisible SVG polygons that highlight on hover.
- Hoverboxes include your custom HTML content and styles.
- Fixed-position hoverboxes scale correctly at any viewport size.
- The file is fully self-contained — upload it anywhere and it just works.

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| **Enter** | Close current polygon |
| **Esc** | Cancel current drawing / cancel hoverbox placement |
| **Right-click** | Undo last polygon point / remove a vertex point |
| **Double-click** | Close polygon / add point on edge |
| **Delete** | Remove selected zone(s) |
| **Ctrl+D** / **Cmd+D** | Duplicate selected zone(s) |
| **Shift+Click** | Multi-select zones |

---

## Deploying to GitHub Pages

1. Create a new GitHub repository.
2. Add the `index.html` file (the builder) to the root of the repo.
3. Go to **Settings → Pages → Source** and select the `main` branch.
4. Your builder will be live at `https://yourusername.github.io/your-repo-name/`.

To host **exported infographics**:

1. Export your infographic from the builder.
2. Rename the downloaded file (e.g., `my-infographic.html`).
3. Add it to the same repo (or a separate one).
4. It will be accessible at `https://yourusername.github.io/your-repo-name/my-infographic.html`.

---

## Embedding in WordPress

Once your exported infographic is hosted (on GitHub Pages or any web server), embed it in WordPress using a **Custom HTML** block:

```html
<div style="display: flex; justify-content: center; width: 100%;">
  <iframe 
    src="https://yourusername.github.io/your-repo-name/my-infographic.html" 
    width="100%" 
    style="max-width: 900px; border: none; overflow: hidden;" 
    height="700px" 
    scrolling="no"
    title="Interactive Infographic">
  </iframe>
</div>
```

You can also store it on wordpress itself by adding the html file to `\htdocs\website-name\wp-content\uploads` using File Manager and the src will be 
```html
<div style="display: flex; justify-content: center; width: 100%;">
  <iframe 
    src=https://website-name.com/wp-content/uploads/infographic.html
    width="100%" 
    style="max-width: 900px; border: none; overflow: hidden;" 
    height="700px" 
    scrolling="no"
    title="Interactive Infographic">
  </iframe>
</div>
```

**Tips for WordPress embedding:**

- Adjust `max-width` and `height` to match your infographic's aspect ratio.
- If your infographic feels cramped, increase the `height` value.
- The outer `div` with `display: flex` and `justify-content: center` keeps the iframe centered in your post or page layout.
- Make sure your hosting URL uses **HTTPS** — WordPress sites on HTTPS will block HTTP iframes.
- If using a page builder (Elementor, Divi, etc.), look for an "HTML" or "Code" widget and paste the same snippet.

**Responsive tip:** For better mobile behavior, you can wrap the iframe in a responsive container:

```html
<div style="display: flex; justify-content: center; width: 100%;">
  <div style="position: relative; width: 100%; max-width: 900px; padding-bottom: 78%;">
    <iframe 
      src="https://yourusername.github.io/your-repo-name/my-infographic.html" 
      style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;" 
      scrolling="no"
      title="Interactive Infographic">
    </iframe>
  </div>
</div>
```

Adjust `padding-bottom` to match your image's aspect ratio (e.g., `56.25%` for 16:9, `75%` for 4:3, `78%` for a slightly taller layout).

---

## Storage Backends

The builder automatically selects the best available storage:

| Priority | Backend | When Used | Limits |
|----------|---------|-----------|--------|
| 1st | **Claude Storage** | Inside Claude artifacts | Managed by Anthropic |
| 2nd | **IndexedDB** | GitHub Pages, local dev, most browsers | Effectively unlimited |
| 3rd | **localStorage** | Fallback for restricted environments | ~5–10MB per domain |

The active backend is shown as a small badge in the toolbar. The `.json` project file import/export works independently of all storage backends and is the most portable option for sharing or backing up work.

---

## Browser Support

Works in all modern browsers:

- Chrome / Edge 80+
- Firefox 78+
- Safari 14+

Canvas rendering and IndexedDB are the core requirements. No polyfills needed.

---

## License

MIT — use it however you like.