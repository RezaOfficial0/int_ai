# INT.AI — Company Website
 
A single-page marketing site for INT.AI, built as a static HTML/CSS/JS file with no build step or dependencies.
 
## Live design direction
 
The visual identity is a **blueprint / infrastructure schematic** aesthetic — a graph-paper grid backdrop, monospaced technical labels, and a signature animated pipeline diagram in the hero that traces the company's actual reference architecture (Data Sources → ETL → Embedding → Vector DB → Foundation Model → Business Logic → Applications), with a signal pulse animating through it.
 
- **Colors:** graphite/near-black background (`#090C10`) with a signal-teal accent (`#4FD8B0`) and a sparing copper accent (`#D98B4F`) for tags.
- **Type:** [Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk) for headlines, [Inter](https://fonts.google.com/specimen/Inter) for body copy, [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) for labels, tags, and data.
- **Numbered sequences** (the 5-phase methodology, the 8-step engagement process) reflect genuine order in the source content; other content (services, industries) is presented as unordered sets/grids.
## Files
 
```
index.html   → the entire site (HTML + CSS + JS in one file)
README.md    → this file
```
 
There's no separate CSS/JS file and no build tooling — everything lives in `index.html` so it can be opened or hosted as-is.
 
## Running it locally
 
Just open the file in a browser:
 
```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html        # Windows
```
 
Or serve it (recommended, avoids any `file://` quirks):
 
```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```
 
## Deploying it
 
Since it's a single static HTML file with no dependencies beyond Google Fonts (loaded via CDN `<link>` tags), you can drop it on any static host:
 
- **Netlify / Vercel:** drag-and-drop the file (rename to `index.html` if needed) or connect a repo.
- **GitHub Pages:** push to a repo, enable Pages, point it at the branch/root.
- **Any web server:** copy `index.html` into the server's public/www directory.
No environment variables, no `npm install`, no build command required.
 
## Structure of the page
 
Sections appear in this order (each is a `<section id="...">` you can jump to or reorder):
 
| # | Section | id |
|---|---------|-----|
| 1 | Hero + architecture diagram | *(top, no id)* |
| 2 | The enterprise AI problem | `#problem` |
| 3 | Our solution / ecosystem | `#solution` |
| 4 | Core services | `#services` |
| 5 | Delivery methodology (5 phases) | `#methodology` |
| 6 | Industries we serve | `#industries` |
| 7 | Technology stack | `#stack` |
| 8 | Security & compliance | `#security` |
| 9 | Deployment options | `#deployment` |
| 10 | Why choose INT.AI (comparison table) | `#why` |
| 11 | Engagement process (8 steps) | `#engagement` |
| 12 | Commercial models | `#commercial` |
| 13 | Company roadmap | `#roadmap` |
| 14 | Contact / footer | `#contact` |
 
The nav bar at the top links to a subset of these anchors.
 
## Customizing
 
**Colors & fonts** — everything is driven by CSS custom properties at the top of the `<style>` block in `index.html`:
 
```css
:root{
  --bg: #090C10;          /* page background */
  --surface: #10151C;     /* card/panel background */
  --accent: #4FD8B0;      /* signal teal — links, highlights, active states */
  --accent-warm: #D98B4F; /* copper — service tags */
  --display: 'Space Grotesk', sans-serif;
  --body: 'Inter', sans-serif;
  --mono: 'JetBrains Mono', monospace;
  ...
}
```
 
Change a value once here and it updates everywhere it's used.
 
**Content** — all copy lives directly in the HTML markup for each `<section>`, in plain sentence form (no CMS/data file), so edits are a matter of finding the relevant section and changing the text or list items directly.
 
**The hero diagram** — it's hand-built inline SVG (`<svg class="pipeline">`) with `<rect>` nodes and `<path>` connectors; the flowing dashes are a CSS `stroke-dashoffset` animation (`.flow-dash` / `@keyframes dash-move`). Add or remove a pipeline stage by adding a node `<rect>`/`<text>` pair and a connecting `<path>`.
 
**Scroll animations** — sections fade/slide in via an `IntersectionObserver` at the bottom of the file, toggling the `.in` class on any element with `.reveal`. Add `class="reveal"` to any wrapper you want to animate in on scroll.
 
## Browser support
 
Uses modern but well-supported CSS (custom properties, CSS Grid, `backdrop-filter`) and vanilla JS (`IntersectionObserver`). Works in current Chrome, Firefox, Safari, and Edge. No polyfills included.
 
## Accessibility notes
 
- Semantic landmarks (`header`, `main`, `section`, `footer`) are in place.
- Color contrast for body text and links against the dark background meets WCAG AA.
- If you extend the page, keep interactive elements (links, buttons) reachable by keyboard and visibly focusable — the current build inherits default browser focus outlines, which you may want to restyle rather than remove.
