# Webflow Editing Runbook

Use this when making changes to the live M45 Capital Partners site.

## Repositories And URLs

GitHub repository:

```text
https://github.com/g-yeo11/m45-webflow-custom-code
```

GitHub Pages script:

```text
https://g-yeo11.github.io/m45-webflow-custom-code/m45-site.js
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
$node='C:\Users\gordo\.cache\codex-runtimes\codex-primary-runtime\dependencies\node\bin\node.exe'
@'
const fs = require('fs');
const js = fs.readFileSync('C:/Users/gordo/Documents/Codex/2026-07-01/are/work/m45-webflow-custom-code/m45-site.js', 'utf8');
new Function(js);
console.log('ok', js.length);
'@ | & $node -
```

Commit and push:

```powershell
git add m45-site.js CHANGELOG.md docs README.md
git commit -m "Describe change"
git push
```

## Publishing A Script Change

1. Push the GitHub commit.
2. Open the Webflow custom-code page.
3. In the footer code, update the query string:

```html
<script src="https://g-yeo11.github.io/m45-webflow-custom-code/m45-site.js?v=YYYYMMDDHHMM"></script>
```

4. Save.
5. Publish to staging and production.
6. Test with a cache-busting URL:

```text
https://www.m45capital.com/research-insights?verify=YYYYMMDDHHMM
```

## Publishing A Webflow-Only Change

1. Make the change in Webflow Designer or CMS.
2. Preview in Webflow.
3. Publish to staging and production.
4. Verify production.
5. Add a changelog entry if the change affects user-facing content, layout, navigation, or interactions.

## Cache Busting

If a script change is not visible:

- Confirm `m45-site.js` is updated on GitHub Pages.
- Confirm Webflow footer loader `v=` changed.
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

3. Bump the Webflow footer loader `v=`.
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
