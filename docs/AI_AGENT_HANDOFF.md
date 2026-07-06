# AI Agent Handoff Notes

This file is for future AI agents or developers working on the M45 Webflow site.

## Read These First

1. `README.md`
2. `CHANGELOG.md`
3. `docs/SITE_ARCHITECTURE.md`
4. `docs/CUSTOM_CODE_REFERENCE.md`
5. The current `m45-site.js`

## Current Important Facts

- The site is hosted by Webflow.
- The custom JavaScript is hosted by GitHub Pages.
- Webflow global custom code should stay minimal.
- `m45-site.js` is the active behaviour layer.
- The production loader should be cache-busted with a `v=` query string after script changes.

## Do Not Do This

- Do not paste the full script into Webflow global custom code unless intentionally abandoning GitHub Pages.
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

### Improve social preview cards

Best path:

- Create real Webflow CMS detail pages for papers.
- Give each page its own title, meta description, and Open Graph image.
- Share those canonical pages instead of JavaScript redirect routes.

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

