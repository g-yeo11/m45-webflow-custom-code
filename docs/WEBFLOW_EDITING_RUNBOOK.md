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
4. Identify whether the change belongs in:
   - Webflow Designer or CMS
   - `m45-site.js`
   - both

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
2. Clear Head Code.
3. Paste the full contents of `webflow-footer-inline-full.html` into Footer Code.
4. Save.
5. Publish to staging and production.
6. Test with a cache-busting URL:

```text
https://www.m45capital.com/research-insights?verify=YYYYMMDDHHMM
```

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

## Publishing A Webflow-Only Change

1. Make the change in Webflow Designer or CMS.
2. Preview in Webflow.
3. Publish to staging and production.
4. Verify production.
5. Add a changelog entry if the change affects user-facing content, layout, navigation, or interactions.

## Cache Busting

If a script change is not visible:

- Confirm Webflow Footer Code contains the current `webflow-footer-inline-full.html`.
- Confirm Webflow Head Code is empty.
- Confirm Webflow was published.
- Test with a query string on the page URL.
- Hard refresh the browser.

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
