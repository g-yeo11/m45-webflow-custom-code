# Custom Code Reference

The active custom script source is `m45-site.js`.

The live Webflow site should use an inline global Footer Code payload generated into `webflow-footer-inline-full.html`. This keeps the live behaviour inside Webflow while still preserving a version-controlled source of truth in this repo.

## Script Location

Local file:

```text
C:\Users\gordo\Documents\Codex\2026-07-01\are\work\m45-webflow-custom-code\m45-site.js
```

Webflow footer payload:

```text
C:\Users\gordo\Documents\Codex\2026-07-01\are\work\m45-webflow-custom-code\webflow-footer-inline-full.html
```

Webflow Head Code should be empty or contain only `<!-- M45 custom behaviour lives in Footer code. -->`. It must not contain a script, GitHub loader, or duplicate footer payload. Webflow Footer Code should contain the full contents of `webflow-footer-inline-full.html`.

The Webflow project setting `Run custom code in Preview` should remain on. Otherwise, Webflow's own site preview can look different from production and may show stale native fallback content instead of the canonical custom-code-rendered Research & Insights page.

For Codex-assisted Webflow navigation, paste verification, save/publish sequencing, and common issue recovery, use `docs/CODEX_WEBFLOW_OPERATIONS.md`.

## Module Map

`m45-site.js` is organized as a sequence of immediately invoked function expressions. Each block is self-contained and guarded to avoid running on unrelated pages where possible.

`webflow-footer-inline-full.html` contains one script tag:

1. The full `m45-site.js` payload.

The Research & Insights renderer and all global nav normalization live inside this single script. Avoid adding a second recovery script in Webflow; regenerate and paste the full footer payload instead.

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
- The mobile handler must cancel the desktop modal path before triggering the native link. This is especially important for the featured `The M45 Way` link because it shares the same desktop modal bindings.

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

Implementation note:

- On standard Webflow pages, the native nav often keeps the page labels inside a single `.navbar-linkwrapper`. Insert `Research & Insights` directly after the `Newsroom` anchor inside that wrapper when present. Adding a separate wrapper after the native wrapper creates a doubled final gap.
- On dark hero pages, copy the neighbouring native link class list so the item keeps `navlink-solstice` and inherits the correct white text treatment.
- On Research & Insights, the custom `.ri-nav .ri-links` header owns its own page-label structure.

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
- When a change is intended to be live, verify production HTML after publishing. A repo commit alone does not change the Webflow site.

## Syntax Check

Use Node to check the script before publishing:

```powershell
cd C:\Users\gordo\Documents\Codex\2026-07-01\are\work\m45-webflow-custom-code
node --check m45-site.js
```

Also check the single inline script tag in `webflow-footer-inline-full.html` before pasting into Webflow.
