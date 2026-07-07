# AI Agent Handoff Notes

This file is for future AI agents or developers working on the M45 Webflow site.

## Read These First

1. `README.md`
2. `CHANGELOG.md`
3. `docs/SITE_ARCHITECTURE.md`
4. `docs/CUSTOM_CODE_REFERENCE.md`
5. `docs/VISUAL_STYLE_AND_ANIMATIONS.md`
6. The current `m45-site.js`

## Current Important Facts

- The site is hosted by Webflow.
- The live custom JavaScript is pasted directly into Webflow global Footer Code.
- `m45-site.js` is the main source file, not the exact paste payload.
- `webflow-footer-inline-full.html` is the exact payload to paste into Webflow Footer Code.
- Webflow Head Code should be empty.
- The final Research & Insights featured-card recovery is embedded at the end of `m45-site.js` and guarded by `__m45WebflowFeaturedResearchPatch20260707`.

## Do Not Do This

- Do not add a GitHub Pages loader back into Webflow unless the owner explicitly changes the hosting model again.
- Do not remove the final Research & Insights featured-card recovery from `m45-site.js`.
- Do not create duplicate nav links manually in Webflow without checking the custom nav script.
- Do not remove the mobile direct-PDF behaviour without testing mobile pinch zoom and scroll.
- Do not assume LinkedIn/WhatsApp previews will use JavaScript-rendered metadata.
- Do not change leadership ordering without preserving Jason first and Leland last unless requested.

## Likely Future Requests

### Add a whitepaper

Use `docs/RESEARCH_INSIGHTS.md`.

### Fix nav spacing

Look at the canonical global navigation block in `m45-site.js`.

### Fix Research & Insights layout

Look at:

- Research document taxonomy block
- Research animation parity block
- Desktop PDF modal block
- Share tools block
- `docs/VISUAL_STYLE_AND_ANIMATIONS.md`

### Improve social preview cards

Best path:

- Create real Webflow CMS detail pages for papers.
- Give each page its own title, meta description, and Open Graph image.
- Share those canonical pages instead of JavaScript redirect routes.
- Follow `docs/WHITEPAPER_SHARING_PAGES.md`.

## Verification Priorities

Always check:

- Desktop Chrome
- Mobile Safari or mobile-width Chrome
- Published production, not only Webflow Designer
- The page after a hard refresh or cache-busting query string

## Communication Style

The site owner is visual and detail-oriented. When reporting results:

- State what changed.
- State what was verified.
- Mention any limitation plainly.
- Keep the answer concise.
