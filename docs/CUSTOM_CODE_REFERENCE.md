# Custom Code Reference

The active custom script is `m45-site.js`.

It is intentionally loaded externally from GitHub Pages because Webflow's global custom-code fields have a practical character limit and are harder to version-control.

## Script Location

Local file:

```text
C:\Users\gordo\Documents\Codex\2026-07-01\are\work\m45-webflow-custom-code\m45-site.js
```

Hosted file:

```text
https://g-yeo11.github.io/m45-webflow-custom-code/m45-site.js
```

Production loader:

```html
<script src="https://g-yeo11.github.io/m45-webflow-custom-code/m45-site.js?v=YYYYMMDDHHMM"></script>
```

## Module Map

`m45-site.js` is organized as a sequence of immediately invoked function expressions. Each block is self-contained and guarded to avoid running on unrelated pages where possible.

### Research document taxonomy and featured document

Runs on:

- `/research-insights`

Responsibilities:

- Defines the current document list.
- Defines the current featured PDF URL.
- Builds the Research & Insights document cards.
- Replaces the featured left-side panel with the M45 Way teaser text.
- Replaces old filter labels with:
  - `All`
  - `Whitepapers`
  - `Value-Chain`
  - `Company`
  - `Others`
- Binds filter buttons.

Important data:

- `docs` array
- `pdfUrl`
- `card()`
- `bindFilters()`
- `patch()`

### Research filter animation parity

Runs on:

- `/research-insights`

Responsibilities:

- Adds a short opacity and movement transition when document filters are clicked.
- Keeps Research & Insights closer to the feel of the existing `What We Do` interactions.

### Mobile direct PDF handling

Runs on:

- `/research-insights`

Responsibilities:

- On mobile, PDF links open directly in the browser's native PDF viewer.
- This preserves pinch zoom and clearer rendering on mobile.

Reason:

- Embedded PDF iframes on mobile can be blurry or hard to scroll.

### Desktop PDF modal reader

Runs on:

- `/research-insights`

Responsibilities:

- On desktop, PDF links open inside a modal reader.
- The modal includes:
  - Title
  - `Open PDF` link
  - Close button
  - PDF iframe

### Mobile menu arrow fix

Runs on:

- All pages

Responsibilities:

- Moves `.mobilemenu-arrowdiv` to the top of each `.navbar-linkwrapper`.
- Re-runs after menu clicks, resizes, and DOM mutations.

Reason:

- Some mobile menu items placed the arrow below the label after Webflow interactions.

### Research share tools

Runs on:

- `/research-insights`

Responsibilities:

- Adds `Share` next to PDF links.
- Provides:
  - Copy link
  - LinkedIn share
  - WhatsApp share
- Creates clean paper-specific URLs:
  - `/the-m45-way`
  - `/global-luxury`
  - `/ai-foundation-models`
- Redirects those paper URLs back to `/research-insights?paper=...`.

Current limitation:

- LinkedIn and WhatsApp previews depend on the Open Graph tags returned by the shared URL.
- Pure client-side redirects cannot fully control social preview metadata because link preview bots often do not execute JavaScript.
- If paper-specific social previews must be perfect, use real Webflow pages or CMS pages with unique title, description, and Open Graph image for each paper.

### Share icon polish

Runs on:

- `/research-insights`

Responsibilities:

- Converts LinkedIn and WhatsApp share actions into compact icon-style buttons.

### Canonical global navigation

Runs on:

- All pages

Responsibilities:

- Adds `Research & Insights` after `Newsroom` if missing.
- Removes duplicate `Research & Insights` links.
- Normalizes desktop nav typography and spacing.
- Applies active/current state to `Research & Insights`.
- Aligns Research & Insights nav with Webflow's standard page nav.

Expected desktop nav order:

1. `Our Investment Philosophy`
2. `What We Do`
3. `Our Leadership`
4. `Newsroom`
5. `Research & Insights`

## Editing Guidelines

- Keep blocks small and page-scoped.
- Prefer adding a new guarded block over editing unrelated logic.
- Add clear comments before complex behaviour.
- Do not remove Webflow-native classes unless the page has been tested in Designer, staging, and production.
- Update `CHANGELOG.md` every time behaviour changes.

## Syntax Check

Use Node to check the script before publishing:

```powershell
$node='C:\Users\gordo\.cache\codex-runtimes\codex-primary-runtime\dependencies\node\bin\node.exe'
@'
const fs = require('fs');
const js = fs.readFileSync('C:/Users/gordo/Documents/Codex/2026-07-01/are/work/m45-webflow-custom-code/m45-site.js', 'utf8');
new Function(js);
console.log('ok', js.length);
'@ | & $node -
```

