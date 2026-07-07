# Changelog

All meaningful Webflow, custom-code, content, and documentation changes should be recorded here.

Use reverse chronological order. Each entry should include:

- Date
- Summary
- Files changed
- Webflow actions
- Verification performed
- Follow-ups or risks

## 2026-07-07

### Restored featured whitepaper teaser and share action

Summary:

- Added a defensive Research & Insights recovery patch for the featured whitepaper module.
- Restores the long `The M45 Way` teaser in the left feature panel when Webflow renders the native feature classes.
- Restores a featured `Share` action beside `View PDF` with copy, LinkedIn, WhatsApp, and mobile native-share support.

Files changed:

- `m45-site.js`
- `CHANGELOG.md`

Webflow actions:

- None yet. Publish or cache-bust the Webflow custom-code loader if production does not pick up the GitHub Pages script update quickly.

Verification:

- Ran `node --check m45-site.js`.

## 2026-07-06

### Added visual style and animation documentation

Summary:

- Added a dedicated guide for page visuals, typography, layout rhythm, nav behaviour, mobile menu behaviour, page-load animation, scroll reveals, tab transitions, contact panel animation, PDF modal treatment, and footer consistency.
- Documented `What We Do` as the primary visual reference page for matching new or rebuilt pages.

Files changed:

- `README.md`
- `CHANGELOG.md`
- `docs/VISUAL_STYLE_AND_ANIMATIONS.md`
- `docs/AI_AGENT_HANDOFF.md`
- `docs/QA_CHECKLIST.md`
- `docs/SITE_ARCHITECTURE.md`

Webflow actions:

- None for this documentation-only entry.

Verification:

- Confirmed the new guide is linked from `README.md`.

### Added whitepaper sharing pages documentation

Summary:

- Added a dedicated guide explaining how each whitepaper should have its own real Webflow page or CMS item for clean LinkedIn, WhatsApp, and direct-link sharing.
- Documented recommended CMS fields, URL structure, Open Graph requirements, share-button behaviour, migration steps, and QA checks.

Files changed:

- `README.md`
- `CHANGELOG.md`
- `docs/WHITEPAPER_SHARING_PAGES.md`

Webflow actions:

- None for this documentation-only entry.

Verification:

- Confirmed the new guide is linked from `README.md`.

### Created documentation source of truth

Summary:

- Established this repository as the long-term documentation and custom-code home for the M45 Capital Partners Webflow site.
- Added site architecture, custom-code, Research & Insights, Webflow editing, QA, and AI handoff documentation.
- Added this changelog so future edits have a durable audit trail.

Files changed:

- `README.md`
- `CHANGELOG.md`
- `docs/SITE_ARCHITECTURE.md`
- `docs/CUSTOM_CODE_REFERENCE.md`
- `docs/RESEARCH_INSIGHTS.md`
- `docs/WEBFLOW_EDITING_RUNBOOK.md`
- `docs/QA_CHECKLIST.md`
- `docs/AI_AGENT_HANDOFF.md`

Webflow actions:

- None for this documentation-only entry.

Verification:

- Confirmed repository exists at `https://github.com/g-yeo11/m45-webflow-custom-code`.
- Confirmed GitHub Pages script URL is live via the existing production loader contract.

Follow-ups:

- Keep this changelog updated after every production-facing change.
- Consider adding screenshots to a future `docs/screenshots/` folder for visual regression reference.

### Moved Webflow custom code to GitHub Pages

Summary:

- Reduced Webflow custom-code fields from a large inline script to a small external loader.
- Hosted the full custom site script through GitHub Pages.
- Solved the Webflow custom-code character-limit issue.

Files changed:

- `m45-site.js`
- `README.md`

Webflow actions:

- Head code reduced to a one-line explanatory comment.
- Footer code reduced to the hosted script loader.
- Published to staging and production.

Verification:

- Confirmed production pages load `m45-site.js`.
- Confirmed the old duplicate inline custom-code blocks are not present in live HTML.

### Standardized global navigation

Summary:

- Added `Research & Insights` to the global navigation.
- Removed duplicate `Research & Insights` links from affected pages.
- Normalized desktop nav typography, spacing, active underline, and hover underline behaviour across pages.
- Fixed mobile menu `Research & Insights` visibility and arrow placement.

Files changed:

- `m45-site.js`

Webflow actions:

- Published after cache-busting the footer loader.

Verification:

- Checked `/our-investment-philosophy`, `/what-we-do`, `/our-leadership`, `/newsroom`, and `/research-insights`.
- Confirmed desktop nav order:
  - `Our Investment Philosophy`
  - `What We Do`
  - `Our Leadership`
  - `Newsroom`
  - `Research & Insights`
- Confirmed exactly one `Research & Insights` link appears on each page.
- Confirmed mobile menu shows exactly one `Research & Insights` link.

### Built Research & Insights custom behaviour

Summary:

- Built and refined the `Research & Insights` page.
- Added document taxonomy:
  - `Whitepapers`
  - `Value-Chain`
  - `Company`
  - `Others`
- Added featured document support.
- Added PDF reader modal on desktop.
- Set mobile PDF links to open the native PDF directly for sharper viewing and pinch zoom.
- Added share tools with copy, LinkedIn, and WhatsApp actions.
- Added paper-specific share routes that redirect into `Research & Insights`.

Files changed:

- `m45-site.js`

Webflow actions:

- Published page and global custom-code changes.

Verification:

- Confirmed desktop PDF modal opens for all active papers.
- Confirmed mobile PDF links open the native PDF viewer.
- Confirmed category filters show and hide cards.
- Confirmed share popover appears on desktop.

Current papers:

- `The M45 Way`
- `Global Luxury`
- `AI Foundation Models`

### Updated contact panel map behaviour

Summary:

- Updated `Locate Us` to point to the official Google Maps location supplied by M45 Capital Partners.

Files changed:

- `m45-site.js`

Webflow actions:

- Published after script update.

Verification:

- Confirmed contact panel still opens from `Get In Touch`.

### Earlier Webflow content and layout edits

Summary:

- Reordered global page sequence so `Our Investment Philosophy` appears before `What We Do`.
- Updated `What We Do` page order so `Investment Management` appears before `Wealth Management`.
- Set `Investment Management` as the default `What We Do` tab.
- Replaced Asset Management wording with Investment Management where requested.
- Replaced the investment-management image.
- Added Denny Christian and Yvett Kang to leadership.
- Updated Gordon Yeo biography wording.
- Adjusted leadership ordering and visual grouping.
- Rebuilt `Research & Insights` after Webflow Designer blank-page behaviour.

Files changed:

- Webflow page and CMS content.
- Later behaviour consolidated in `m45-site.js`.

Webflow actions:

- Multiple Designer/CMS edits and publishes.

Verification:

- Visual review in Webflow Designer, Webflow preview, and production pages.
