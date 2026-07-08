# Webflow Editing Runbook

Use this when making changes to the live M45 Capital Partners site.

## Repositories And URLs

GitHub repository:

```text
https://github.com/g-yeo11/m45-webflow-custom-code
```

Production site:

```text
https://www.m45capital.com
```

Webflow custom-code page:

```text
https://webflow.com/dashboard/sites/m45capital/custom-code
```

## Before Editing

1. Check repository status.
2. Pull latest changes if another person may have edited.
3. Read the latest entries in `CHANGELOG.md`.
4. Read `docs/CODEX_WEBFLOW_OPERATIONS.md` if Codex will navigate Webflow.
5. Identify whether the change belongs in:
   - Webflow Designer or CMS
   - `m45-site.js`
   - both

If the request is visual, open `What We Do` as the reference page and compare it side by side with the target page.

## Editing `m45-site.js`

Local path:

```text
C:\Users\gordo\Documents\Codex\2026-07-01\are\work\m45-webflow-custom-code\m45-site.js
```

Standard commands:

```powershell
cd C:\Users\gordo\Documents\Codex\2026-07-01\are\work\m45-webflow-custom-code
git status --short
```

Run syntax check:

```powershell
node --check m45-site.js
```

Regenerate Webflow footer payload:

```powershell
$repo='C:\Users\gordo\Documents\Codex\2026-07-01\are\work\m45-webflow-custom-code'
$main=Get-Content -LiteralPath (Join-Path $repo 'm45-site.js') -Raw
$payload="<!-- M45 Webflow-owned custom behaviour; update this marker when publishing a material custom-code change. Source files are maintained in the local documentation repo. -->`r`n<script>`r`n$main`r`n</script>`r`n"
Set-Content -LiteralPath (Join-Path $repo 'webflow-footer-inline-full.html') -Value $payload -Encoding UTF8
```

Commit and push:

```powershell
git add m45-site.js webflow-footer-inline-full.html CHANGELOG.md docs README.md
git commit -m "Describe change"
git push
```

## Publishing A Script Change

1. Open the Webflow custom-code page.
2. Clear Head Code, or leave only `<!-- M45 custom behaviour lives in Footer code. -->`.
3. Paste the full contents of `webflow-footer-inline-full.html` into Footer Code.
4. Verify the pasted Footer Code:
   - It starts with the `M45 Webflow-owned custom behaviour` comment.
   - It contains one `<script>` tag.
   - It contains the expected current change.
   - It does not contain `github`, `g-yeo11`, or an external loader.
5. If using the expanded editor, click `Save & Close`.
6. Click the main Webflow `Save` button.
7. Publish to staging and production.
8. Test with a cache-busting URL:

```text
https://www.m45capital.com/research-insights?verify=YYYYMMDDHHMM
```

9. Confirm the live HTML:

```powershell
$html=(Invoke-WebRequest -Uri "https://www.m45capital.com/research-insights?verify=$([DateTimeOffset]::UtcNow.ToUnixTimeMilliseconds())" -UseBasicParsing).Content
[pscustomobject]@{
  hasHeadNote = ($html -match 'M45 custom behaviour lives in Footer code')
  hasNav2 = ($html -match '20260707-nav2')
  hasGithubLoader = ($html -match 'github|g-yeo11')
  hasM45WayTeaser = ($html -match 'A short note on how we think about investing')
  hasMobilePdfNative = ($html -match 'nativeLink')
} | ConvertTo-Json
```

Expected:

- `hasGithubLoader` is `false`.
- The marker for the changed feature is `true`.
- `hasMobilePdfNative` is `true` after Research PDF behaviour changes.

For Research & Insights, also test the Webflow Designer preview:

1. Open `Research & Insights` in Webflow Designer.
2. Click Preview.
3. Switch on `Enable custom code?` if it is not already on.
4. Confirm the preview shows the canonical Research page:
   - featured teaser in the left panel
   - featured `Share`
   - `All / Whitepapers / Value-Chain / Company / Others`
   - only `The M45 Way`, `Global Luxury`, and `AI Foundation Models`

Note:

- Webflow pure Design mode does not reliably execute global footer custom code.
- If pure Design mode shows old fallback cards, verify Preview before assuming production is broken.
- If the static Designer fallback must match exactly, edit the native Webflow elements manually as a separate Designer task.

## Codex Navigation Notes

When Codex controls Webflow:

- Inspect the visible DOM before clicking.
- Re-inspect after every modal open, save, publish, or navigation event because Webflow node IDs change.
- Treat `node_id` values as temporary and pass them as strings when using click helpers.
- Keep the Webflow Custom Code page open until save and publish are confirmed.
- Do not stop after pasting into the footer editor. The required sequence is:
  1. Paste into Footer Code.
  2. Verify the paste.
  3. `Save & Close` the expanded editor.
  4. Main Webflow `Save`.
  5. Publish selected domains.
  6. Verify production HTML and rendered page.

If Codex stops working mid-change, follow the recovery checklist in `docs/CODEX_WEBFLOW_OPERATIONS.md`.

## Publishing A Webflow-Only Change

1. Make the change in Webflow Designer or CMS.
2. Preview in Webflow.
3. Publish to staging and production.
4. Verify production.
5. Add a changelog entry if the change affects user-facing content, layout, navigation, or interactions.

## Cache Busting

If a script change is not visible:

- Confirm Webflow Footer Code contains the current `webflow-footer-inline-full.html`.
- Confirm Webflow Head Code is empty or note-only, with no scripts or loaders.
- Confirm Webflow was published.
- Test with a query string on the page URL.
- Hard refresh the browser.
- Confirm the production HTML contains the expected markers.
- Confirm the old GitHub loader is not present.

## Rollback

To roll back a script change:

1. Find the previous good commit:

```powershell
git log --oneline
```

2. Revert the bad commit:

```powershell
git revert <commit-sha>
git push
```

3. Paste the previous good `webflow-footer-inline-full.html` into Webflow Footer Code.
4. Publish Webflow.
5. Verify production.

Avoid destructive git commands such as `git reset --hard` unless the intent is explicit and the user understands the impact.

## When To Use Webflow CMS Pages For Papers

Use CMS or real Webflow pages if:

- Each paper needs unique LinkedIn/WhatsApp preview metadata.
- Each paper needs a public standalone landing page.
- Marketing wants custom Open Graph titles, descriptions, and images.

Use the current JavaScript share routes if:

- The goal is fast sharing from the existing Research & Insights page.
- Perfect social preview cards are not mandatory.

For the recommended full setup, follow `docs/WHITEPAPER_SHARING_PAGES.md`.
