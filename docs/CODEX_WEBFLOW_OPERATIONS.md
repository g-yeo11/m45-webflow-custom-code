# Codex Webflow Operations Guide

This guide captures the practical workflow learned while editing the M45 Capital Partners Webflow site with Codex.

Use it when a new Codex chat, developer, or agent needs to make Webflow edits without re-learning the same issues.

## Operating Model

Webflow owns the live site. This repository owns the custom-code source and documentation.

Current live-code model:

- Webflow Head Code should be empty or contain only `<!-- M45 custom behaviour lives in Footer code. -->`.
- Webflow Head Code must not contain a script, GitHub loader, or duplicate footer payload.
- Webflow global Footer Code should contain the full inline payload from `webflow-footer-inline-full.html`.
- `m45-site.js` is the source file to edit.
- `webflow-footer-inline-full.html` is the generated paste payload.
- Do not reintroduce the old GitHub Pages loader unless the owner explicitly changes the hosting model.

The repo is documentation and source control. The live site does not need GitHub to run.

## Best Way To Start A New Codex Chat

Tell Codex:

```text
We are editing the M45 Capital Partners Webflow site.
Repo: C:\Users\gordo\Documents\Codex\2026-07-01\are\work\m45-webflow-custom-code
Read README.md, CHANGELOG.md, docs/AI_AGENT_HANDOFF.md, docs/CODEX_WEBFLOW_OPERATIONS.md, and docs/WEBFLOW_EDITING_RUNBOOK.md first.
Live custom code is pasted directly into Webflow Footer Code from webflow-footer-inline-full.html.
Head Code must stay empty or contain only the harmless footer-code note.
Use What We Do as the visual and animation reference page.
Verify on production with cache-busting URLs after publishing.
```

For a visual/layout request, also provide:

- The Webflow or production URL currently open.
- The exact page being edited.
- A screenshot with circles/arrows if possible.
- The reference page to match, usually `/what-we-do`.
- Whether the change should affect desktop, mobile, or both.

## Codex Browser Navigation Principles

When controlling Webflow:

1. Use the active in-app browser or the logged-in Chrome session.
2. Inspect the visible DOM before clicking.
3. Treat Webflow `node_id` values as temporary. They can change after every click, save, modal open, or page refresh.
4. After any major UI change, inspect the visible DOM again before the next click.
5. When a click helper needs a `node_id`, pass it as a string.
6. Keep progress notes short but explicit: what is being changed, what was saved, what was published, and what was verified.

Common Codex/browser gotchas:

- The Webflow expanded code editor is separate from the page-level Save button.
- Pasting into the expanded editor is not enough. You must click `Save & Close`, then click the main Webflow `Save`, then publish.
- The publish menu can stay open after publishing. Confirm the production HTML or page behaviour, not just the button state.
- Webflow can show stale content in Design mode when custom code is not running. Use Preview with custom code enabled for behaviour checks.

## Custom Code Update Procedure

1. Check repo status:

```powershell
cd C:\Users\gordo\Documents\Codex\2026-07-01\are\work\m45-webflow-custom-code
git status --short
```

2. Edit `m45-site.js`.

3. Run syntax check:

```powershell
node --check m45-site.js
```

4. Regenerate Webflow Footer Code:

```powershell
$repo='C:\Users\gordo\Documents\Codex\2026-07-01\are\work\m45-webflow-custom-code'
$main=Get-Content -LiteralPath (Join-Path $repo 'm45-site.js') -Raw
$payload="<!-- M45 Webflow-owned custom behaviour; update this marker when publishing a material custom-code change. Source files are maintained in the local documentation repo. -->`r`n<script>`r`n$main`r`n</script>`r`n"
Set-Content -LiteralPath (Join-Path $repo 'webflow-footer-inline-full.html') -Value $payload -Encoding UTF8
```

5. Open Webflow custom code:

```text
https://webflow.com/dashboard/sites/m45capital/custom-code
```

6. Clear Head Code, or leave only:

```html
<!-- M45 custom behaviour lives in Footer code. -->
```

It should contain no scripts, loaders, or duplicate footer payload.

7. Expand Footer Code editor.

8. Paste the full contents of `webflow-footer-inline-full.html`.

9. Verify the paste before saving:

- It starts with the `M45 Webflow-owned custom behaviour` comment.
- It contains one `<script>` block.
- It contains the expected current marker or changed code.
- It does not contain `github`, `g-yeo11`, or an external loader.

10. Click `Save & Close` in the expanded editor.

11. Click the main Webflow `Save`.

12. Publish to both staging and production.

13. Verify production with a cache-busting URL.

14. Update `CHANGELOG.md`, commit, and push.

## Verify The Published HTML

Use this after publishing:

```powershell
$html=(Invoke-WebRequest -Uri "https://www.m45capital.com/research-insights?verify=$([DateTimeOffset]::UtcNow.ToUnixTimeMilliseconds())" -UseBasicParsing).Content
[pscustomobject]@{
  hasHeadNote = ($html -match 'M45 custom behaviour lives in Footer code')
  hasNav2 = ($html -match '20260707-nav2')
  hasGithubLoader = ($html -match 'github|g-yeo11')
  hasResearchCanonical = ($html -match 'm45-research-canonical')
  hasM45WayTeaser = ($html -match 'A short note on how we think about investing')
  hasMobilePdfNative = ($html -match 'nativeLink')
} | ConvertTo-Json
```

Expected:

- `hasGithubLoader` should be `false`.
- The relevant markers for the change should be `true`.
- `hasMobilePdfNative` should be `true` after Research PDF changes.

## Automated Browser Verification

The bundled Codex runtime may need `NODE_PATH` set for Playwright:

```powershell
$node='C:\Users\gordo\.cache\codex-runtimes\codex-primary-runtime\dependencies\node\bin\node.exe'
$env:NODE_PATH='C:\Users\gordo\.cache\codex-runtimes\codex-primary-runtime\dependencies\node\node_modules;C:\Users\gordo\.cache\codex-runtimes\codex-primary-runtime\dependencies\node\node_modules\.pnpm\node_modules'
```

Use automated checks for:

- Nav count and spacing across pages.
- Research featured teaser visibility and colour.
- Mobile Research teaser containment.
- PDF modal/native PDF behaviour.
- Share button behaviour.

Always also do a visual check when the user is asking for design precision.

## Webflow Designer Vs Preview

Important distinction:

- Design mode can show old static fallback elements.
- Preview mode with `Enable custom code?` should show the actual custom-code-rendered page.
- Production is the final source of truth after publishing.

For Research & Insights:

- The Webflow native fallback can use classes like `research-main-native`, `research-feature-native`, and `research-grid-native`.
- The live canonical page is normalized by `m45-site.js`.
- If Design mode looks wrong but Preview and production look right, do not rebuild the page unless the user specifically wants Design mode to visually match too.

## Common Issues And Mitigations

### Change is not visible on production

Likely causes:

- Main Webflow `Save` was not clicked after `Save & Close`.
- Site was saved but not published.
- Browser cache is showing the old page.
- Code was pasted into the wrong field.
- Head Code still contains an old loader or a duplicate copy of the footer payload.

Mitigation:

- Confirm Footer Code contains the latest payload.
- Confirm Head Code is empty or note-only.
- Publish staging and production.
- Test with a cache-busting query string.
- Inspect production HTML for markers.

### Webflow custom code is duplicated in Head and Footer

Likely causes:

- The full payload was accidentally pasted into Head Code.
- Webflow's code editor focus moved to the wrong editor after a save, modal, or scroll.
- A stale GitHub loader was left in Head Code while the inline footer payload was also active.

Mitigation:

- Set Head Code to empty or `<!-- M45 custom behaviour lives in Footer code. -->`.
- Paste the full `webflow-footer-inline-full.html` payload into Footer Code only.
- Before saving, use select-all/copy on the active editor and verify the clipboard contents are the intended field.
- After publishing, inspect production HTML for one custom behaviour script, no GitHub loader, and the latest marker.
- If Webflow keeps focusing the wrong editor, click inside the lower Footer Code editor by coordinates, then verify with clipboard readback before saving.

### Webflow preview looks different from production

Likely causes:

- `Run custom code in Preview` is off.
- Webflow pure Design mode is being viewed instead of Preview.
- Native fallback elements are stale.

Mitigation:

- Turn on `Run custom code in Preview`.
- Use Preview and `Enable custom code?`.
- Compare production with a cache-busting URL.

### Research & Insights fallback cards reappear

Likely causes:

- Custom code did not run.
- Footer Code is missing or stale.
- The page is in pure Design mode.

Mitigation:

- Confirm the canonical renderer is in Footer Code.
- Confirm production HTML contains `m45-research-canonical`.
- Use Preview with custom code enabled.
- If Design mode must match, manually update the native Webflow fallback elements.

### Research featured teaser is missing or unreadable

Likely causes:

- Old footer payload.
- Text colour inherited white on the light panel.
- Mobile fixed-height panel clipping the long teaser.

Mitigation:

- Verify the long teaser exists in `m45-site.js`.
- Verify production HTML contains the teaser.
- Check computed teaser colour on desktop.
- On mobile, confirm the light panel auto-heights and the dark card starts below it.

### Nav spacing, colour, or duplicate Research links are wrong

Likely causes:

- `Research & Insights` was inserted as a separate wrapper.
- The injected link did not copy neighbouring nav classes.
- An old duplicate link remains in a page template.
- Page-specific header structure differs.

Mitigation:

- Insert `Research & Insights` after `Newsroom` inside the native link wrapper when possible.
- Copy nearby link classes so dark/light header colour is inherited.
- Remove duplicate injected links.
- Run the automated nav check across:
  - `/`
  - `/our-investment-philosophy`
  - `/what-we-do`
  - `/our-leadership`
  - `/newsroom`
  - `/research-insights`

### Mobile menu arrows appear below labels

Likely causes:

- Webflow interactions move or reveal menu elements after custom code runs.

Mitigation:

- Keep the mobile menu arrow normalization block.
- Re-run it after clicks, resizes, and DOM mutations.
- Check all mobile menu items after tapping each label.

### Mobile PDF is blurry or cannot scroll

Likely causes:

- Embedded PDF iframe is being used on mobile.
- A desktop modal click handler is still winning before the mobile native branch.
- Duplicate Head/Footer scripts are competing.

Mitigation:

- Keep mobile PDF links opening directly in the native browser PDF viewer.
- Use the desktop modal only for desktop.
- For `The M45 Way`, verify mobile taps do not open `.ri-pdf-reader`.
- Confirm production HTML contains `nativeLink` and does not contain the old mobile branch that only set `link.target = "_self"`.

### LinkedIn or WhatsApp preview is generic

Likely causes:

- Social crawlers scrape raw HTML and often do not execute JavaScript.
- JavaScript routes cannot reliably set unique Open Graph metadata.

Mitigation:

- Create real Webflow pages or CMS detail pages for papers.
- Set paper-specific title, meta description, and Open Graph image.
- Share the real paper page URL, not a JavaScript route or direct PDF URL.
- Follow `docs/WHITEPAPER_SHARING_PAGES.md`.

### Footer height or disclaimer wrapping differs

Likely causes:

- New page uses a different footer structure or extra band.
- Page content width differs from `What We Do`.

Mitigation:

- Use `What We Do` as the footer reference.
- Remove extra dark bands unless intentionally part of the page.
- Compare footer container height, top padding, legal line wrapping, and text colour.

## Design Review Standard

For visual changes, compare side by side with `What We Do`.

Check:

- Header logo size.
- Nav font size and baseline.
- Nav spacing.
- Current-page underline and hover underline.
- Hero height.
- Hero text baseline.
- First section spacing.
- Footer height and disclaimer wrapping.
- Desktop and mobile animations.

If the user says "exact", measure the layout rather than judging by eye only.

## Recovery If Codex Stops Mid-Task

1. Check git status.
2. Read the latest `CHANGELOG.md` entry.
3. Inspect Webflow custom code to see whether the footer payload was pasted.
4. Confirm whether Webflow main Save was clicked.
5. Confirm whether production was published.
6. Verify production HTML markers.
7. Verify the visual symptom with a cache-busting URL.

Do not assume the last step completed just because the repo changed or Webflow editor was open.
