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

### Added client portal integration groundwork

Summary:

- Added a planning document for the future M45 client portal.
- Recommended keeping the public Webflow site as the marketing shell and building the client portal as a separate secure application.
- Documented the preferred future subdomain pattern, security boundary, Webflow handoff points, roles, app contract, and QA checklist.
- Added clear guidance not to store private client documents, secrets, client permissions, or sensitive data in Webflow.
- Added a startup prompt for the separate Codex chat building the portal.

Files changed:

- `README.md`
- `CHANGELOG.md`
- `docs/AI_AGENT_HANDOFF.md`
- `docs/CLIENT_PORTAL_INTEGRATION.md`
- `docs/QA_CHECKLIST.md`
- `docs/SITE_ARCHITECTURE.md`

Webflow actions:

- None. Documentation-only change.

Verification:

- Confirmed portal guidance is linked from the README, site architecture, AI handoff notes, and QA checklist.

### Added Codex Webflow operations documentation

Summary:

- Added a dedicated Codex Webflow operations guide covering how future Codex chats should navigate Webflow, paste and publish custom code, verify production, and recover from common failure modes.
- Documented key lessons from prior Webflow edits:
  - Webflow Head Code should stay empty.
  - Footer Code should contain the inline `webflow-footer-inline-full.html` payload.
  - Do not reintroduce the old GitHub Pages loader.
  - Webflow expanded editor `Save & Close`, main `Save`, and production publish are separate steps.
  - Webflow Design mode can differ from Preview and production when custom code is involved.
  - Production HTML markers and cache-busting URLs are required verification steps.
- Cross-linked the new guide from the README, AI handoff notes, editing runbook, custom-code reference, and QA checklist.

Files changed:

- `README.md`
- `CHANGELOG.md`
- `docs/AI_AGENT_HANDOFF.md`
- `docs/CODEX_WEBFLOW_OPERATIONS.md`
- `docs/CUSTOM_CODE_REFERENCE.md`
- `docs/QA_CHECKLIST.md`
- `docs/WEBFLOW_EDITING_RUNBOOK.md`

Webflow actions:

- None. Documentation-only change.

Verification:

- Confirmed repository docs include the Codex/Webflow navigation workflow, save/publish sequence, common issues, and mitigations.

### Fixed mobile Research featured teaser overflow

Summary:

- Updated the mobile Research & Insights featured module so the light teaser panel auto-expands for the long `The M45 Way` teaser.
- Prevented the teaser text from overflowing into the dark featured card below on phone-width screens.

Files changed:

- `m45-site.js`
- `webflow-footer-inline-full.html`
- `CHANGELOG.md`

Webflow actions:

- Regenerated the inline Footer Code payload.
- Pasted the updated payload into Webflow global Footer Code.
- Saved Webflow custom code.
- Published staging and production.

Verification:

- Confirmed the live production HTML contains the mobile overflow fix, still contains `20260707-nav2`, and has no GitHub loader.
- Verified at a 393px mobile viewport that the teaser is fully inside the light panel and the dark featured card starts below it with no overlap.

### Fixed global nav parity and featured teaser contrast

Summary:

- Updated the global nav normalizer so `Research & Insights` is inserted after `Newsroom` inside the native Webflow nav wrapper when that wrapper contains the existing page links.
- This removes the doubled spacing that occurred when `Research & Insights` was added as a separate wrapper.
- Copied the native link classes from the neighbouring page link so the item inherits the correct light/dark header treatment.
- Added a small fade-in for the injected `Research & Insights` item so it does not appear static compared with the native page labels.
- Added a more specific Research featured-teaser colour rule so the long `The M45 Way` teaser stays readable on the light left panel.

Files changed:

- `m45-site.js`
- `webflow-footer-inline-full.html`
- `CHANGELOG.md`
- `docs/CUSTOM_CODE_REFERENCE.md`
- `docs/QA_CHECKLIST.md`

Webflow actions:

- Regenerated the inline Footer Code payload for Webflow.
- Pasted the updated payload into Webflow global Footer Code.
- Removed the stale GitHub loader from the active published HTML path.
- Switched Webflow's `Run custom code in Preview` setting on so site preview uses the same custom code behaviour.
- Published staging and production.

Verification:

- Ran `node --check m45-site.js`.
- Tested a clean-page simulation with the old custom-code block stripped out and the new script injected.
- Confirmed Home, Our Investment Philosophy, What We Do, Our Leadership, Newsroom, and Research & Insights each have exactly one `Research & Insights` link.
- Confirmed desktop nav gaps are consistently 45px between adjacent labels across all six tested pages.
- Confirmed `Research & Insights` is white on dark hero pages and dark on light hero pages.
- Confirmed `Research & Insights` uses the same Ovo 18.375px desktop nav typography and hover underline behaviour.
- Confirmed the production HTML contains `20260707-nav2`, the teaser override, and no GitHub loader.
- Confirmed Webflow site preview can see the Research teaser inside the preview canvas.
- Confirmed the Research featured teaser text computes to `rgb(77, 83, 96)` instead of white.

### Consolidated Research & Insights into one canonical renderer

Summary:

- Replaced the layered Research & Insights patch stack with one canonical Webflow-owned script in `m45-site.js`.
- The renderer now targets both the published `ri-*` structure and Webflow's native Designer `research-*` structure.
- Restored the featured `The M45 Way` teaser, featured `Share` action, new document taxonomy, and three-paper inventory deterministically.
- Removed the old placeholder cards from the rendered page:
  - `Private Markets Outlook`
  - `Public Markets Review`
  - `Portfolio Construction Framework`
  - `M45 Platform Overview`
- Normalized the nav so each page gets exactly one `Research & Insights` link.
- Documented the important Webflow distinction: pure Design mode can show static native fallback content, while Preview mode with `Enable custom code?` shows the actual site behaviour.

Files changed:

- `m45-site.js`
- `webflow-footer-inline-full.html`
- `CHANGELOG.md`
- `docs/RESEARCH_INSIGHTS.md`
- `docs/WEBFLOW_EDITING_RUNBOOK.md`

Webflow actions:

- Pasted the regenerated `webflow-footer-inline-full.html` into global Footer Code.
- Saved Webflow custom code.
- Published staging and production.
- Verified Webflow Designer Preview with `Enable custom code?` switched on.

Verification:

- Ran `node --check m45-site.js`.
- Confirmed production HTML contains `canonical-research-native-sync`, `m45-research-canonical`, the long featured teaser, and no GitHub loader.
- Confirmed rendered production has:
  - one featured share button
  - tabs `All`, `Whitepapers`, `Value-Chain`, `Company`, `Others`
  - cards `The M45 Way`, `Global Luxury`, `AI Foundation Models`
  - no old placeholder documents
  - exactly one `Research & Insights` nav link
- Confirmed Webflow Preview canvas text contains the same teaser, share action, filters, and cards.

### Moved live custom code back into Webflow Footer Code

Summary:

- Replaced the GitHub Pages loader contract with a Webflow-owned inline footer payload.
- Added `webflow-footer-inline-full.html` as the exact paste payload for Webflow global Footer Code.
- Kept `m45-site.js` as the version-controlled main source file.
- Moved the Research & Insights featured-paper recovery into `m45-site.js` so Webflow only needs to preserve one inline script tag.
- Removed older duplicate featured-paper recovery blocks from `m45-site.js`.
- Updated documentation so future edits do not reintroduce the GitHub loader.

Files changed:

- `m45-site.js`
- `webflow-footer-inline-full.html`
- `README.md`
- `CHANGELOG.md`
- `docs/AI_AGENT_HANDOFF.md`
- `docs/CUSTOM_CODE_REFERENCE.md`
- `docs/RESEARCH_INSIGHTS.md`
- `docs/SITE_ARCHITECTURE.md`
- `docs/WEBFLOW_EDITING_RUNBOOK.md`

Webflow actions:

- Cleared Head Code.
- Pasted the one-script `webflow-footer-inline-full.html` payload into Footer Code.
- Published staging and production.

Verification:

- Ran `node --check m45-site.js`.
- Confirmed `webflow-footer-inline-full.html` contains one script tag with `__m45WebflowFeaturedResearchPatch20260707`, `m45-feature-share`, and no GitHub loader reference.

### Restored featured whitepaper teaser and share action

Summary:

- Added a defensive Research & Insights recovery patch for the featured whitepaper module.
- Restores the long `The M45 Way` teaser in the left feature panel when Webflow renders the native feature classes.
- Restores a featured `Share` action beside `View PDF` with copy, LinkedIn, WhatsApp, and mobile native-share support.
- Follow-up: added a stronger final pass for Webflow's native `.research-feature-*` module so the teaser and featured share action are restored even if another script rewrites the block after initial load.

Files changed:

- `m45-site.js`
- `CHANGELOG.md`

Webflow actions:

- Superseded by the inline footer payload entry above.

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
