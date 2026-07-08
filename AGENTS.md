# M45 Webflow Agent Instructions

This repository is the portable handoff point for Codex Web, Codex desktop, and human editors working on the M45 Capital Partners Webflow site.

## First Read

Before making changes, read:

1. `README.md`
2. `CHANGELOG.md`
3. `docs/AI_AGENT_HANDOFF.md`
4. `docs/CODEX_WEBFLOW_OPERATIONS.md`
5. `docs/WEBFLOW_EDITING_RUNBOOK.md`
6. `docs/QA_CHECKLIST.md`

For visual or animation work, also read `docs/VISUAL_STYLE_AND_ANIMATIONS.md`.

For Research & Insights or whitepaper work, also read:

- `docs/RESEARCH_INSIGHTS.md`
- `docs/WHITEPAPER_SHARING_PAGES.md`

For client portal work, also read `docs/CLIENT_PORTAL_INTEGRATION.md`.

## Operating Model

- Webflow owns the live website and publishing.
- This repo owns the custom-code source, generated Webflow footer payload, documentation, and changelog.
- `m45-site.js` is the source file to edit.
- `webflow-footer-inline-full.html` is the exact payload to paste into Webflow global Footer Code.
- Webflow Head Code must be empty or contain only `<!-- M45 custom behaviour lives in Footer code. -->`.
- Webflow Head Code must not contain a script, GitHub loader, or duplicate footer payload.

Codex Web can safely work on the repo, regenerate payloads, update docs, and create commits or pull requests. Publishing to Webflow still requires a logged-in Webflow session and should be done from Webflow or a Codex desktop/browser session with access.

## Standard Change Flow

1. Check `git status --short`.
2. Edit `m45-site.js` or docs.
3. Regenerate `webflow-footer-inline-full.html` after any `m45-site.js` change.
4. Run `node --check m45-site.js`.
5. Update `CHANGELOG.md`.
6. Commit and push.
7. If the change affects the live site, paste the generated footer payload into Webflow Footer Code, save, publish staging and production, and verify with a cache-busting URL.

## Regenerate Footer Payload

```powershell
$repo='C:\Users\gordo\Documents\Codex\2026-07-01\are\work\m45-webflow-custom-code'
$main=Get-Content -LiteralPath (Join-Path $repo 'm45-site.js') -Raw
$payload="<!-- M45 Webflow-owned custom behaviour; update this marker when publishing a material custom-code change. Source files are maintained in the local documentation repo. -->`r`n<script>`r`n$main`r`n</script>`r`n"
Set-Content -LiteralPath (Join-Path $repo 'webflow-footer-inline-full.html') -Value $payload -Encoding UTF8
```

Codex Web may have a different checkout path. If so, use the repo root for `$repo`.

## Verification Contract

Always verify:

- `node --check m45-site.js`
- `git diff --check`
- Production HTML has no GitHub loader after Webflow publish.
- Production HTML has exactly one custom behaviour payload.
- Desktop and mobile Research PDF behavior:
  - Desktop opens the modal reader.
  - Mobile opens the native PDF directly.
  - Featured `The M45 Way` does not open `.ri-pdf-reader` on mobile.
- Navigation appears consistently across:
  - `/`
  - `/our-investment-philosophy`
  - `/what-we-do`
  - `/our-leadership`
  - `/newsroom`
  - `/research-insights`

## Important Do Nots

- Do not reintroduce the old GitHub Pages loader unless the owner explicitly changes the hosting model.
- Do not paste the full payload into Webflow Head Code.
- Do not trust Webflow Design mode alone for Research & Insights; use Preview with custom code enabled and production.
- Do not store client secrets, private client documents, access tokens, or client-specific data in Webflow.
- Do not build sensitive client portal logic inside Webflow custom code.
