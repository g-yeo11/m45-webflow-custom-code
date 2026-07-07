# AI Agent Handoff Notes

This file is for future AI agents or developers working on the M45 Webflow site.

## Read These First

1. `README.md`
2. `CHANGELOG.md`
3. `docs/SITE_ARCHITECTURE.md`
4. `docs/CUSTOM_CODE_REFERENCE.md`
5. `docs/CODEX_WEBFLOW_OPERATIONS.md`
6. `docs/WEBFLOW_EDITING_RUNBOOK.md`
7. `docs/VISUAL_STYLE_AND_ANIMATIONS.md`
8. The current `m45-site.js`

## Recommended Startup Prompt

When starting a new Codex chat, give it this context:

```text
We are editing the M45 Capital Partners Webflow site.
Repo: C:\Users\gordo\Documents\Codex\2026-07-01\are\work\m45-webflow-custom-code
Live custom code is pasted directly into Webflow global Footer Code from webflow-footer-inline-full.html.
Head Code should be empty.
Do not add the old GitHub Pages loader.
Use What We Do as the visual and animation reference page.
Before changing Webflow, read README.md, CHANGELOG.md, docs/AI_AGENT_HANDOFF.md, docs/CODEX_WEBFLOW_OPERATIONS.md, docs/WEBFLOW_EDITING_RUNBOOK.md, and docs/QA_CHECKLIST.md.
After publishing, verify production with a cache-busting URL.
```

## Current Important Facts

- The site is hosted by Webflow.
- The live custom JavaScript is pasted directly into Webflow global Footer Code.
- `m45-site.js` is the main source file, not the exact paste payload.
- `webflow-footer-inline-full.html` is the exact payload to paste into Webflow Footer Code.
- Webflow Head Code should be empty.
- The final Research & Insights featured-card recovery is embedded at the end of `m45-site.js` and guarded by `__m45WebflowFeaturedResearchPatch20260707`.
- Webflow pure Design mode may not show the final custom-code-rendered page. Preview mode with custom code enabled and production with a cache-busting URL are more reliable.
- Webflow custom-code edits require three separate steps after pasting: `Save & Close` in the expanded editor, main page `Save`, then `Publish`.

## Do Not Do This

- Do not add a GitHub Pages loader back into Webflow unless the owner explicitly changes the hosting model again.
- Do not remove the final Research & Insights featured-card recovery from `m45-site.js`.
- Do not create duplicate nav links manually in Webflow without checking the custom nav script.
- Do not remove the mobile direct-PDF behaviour without testing mobile pinch zoom and scroll.
- Do not assume LinkedIn/WhatsApp previews will use JavaScript-rendered metadata.
- Do not change leadership ordering without preserving Jason first and Leland last unless requested.
- Do not trust Webflow Design mode alone for Research & Insights. Check Preview with custom code enabled and the published site.
- Do not assume a Webflow paste is live until production HTML contains the expected markers and no GitHub loader.

## Likely Future Requests

### Add a whitepaper

Use `docs/RESEARCH_INSIGHTS.md`.

### Fix nav spacing

Look at the canonical global navigation block in `m45-site.js`.

Before changing nav:

- Read `docs/CODEX_WEBFLOW_OPERATIONS.md`.
- Check every desktop page for exactly one `Research & Insights`.
- Check mobile menu order and arrow position.
- Make sure injected nav links copy the neighbouring Webflow link classes.

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
- Production HTML markers after custom-code publish

## Common Recovery Path

If a future Codex chat inherits a half-finished Webflow change:

1. Run `git status --short`.
2. Read the latest `CHANGELOG.md` entry.
3. Confirm whether `m45-site.js` and `webflow-footer-inline-full.html` differ.
4. Inspect Webflow Head Code and Footer Code.
5. Verify whether the main Webflow `Save` button was clicked after the expanded editor was closed.
6. Publish if needed.
7. Check production with a cache-busting URL and a focused visual/DOM test.

## Communication Style

The site owner is visual and detail-oriented. When reporting results:

- State what changed.
- State what was verified.
- Mention any limitation plainly.
- Keep the answer concise.
