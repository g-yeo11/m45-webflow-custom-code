# Codex Web Handoff

Use this guide to continue M45 Webflow work from Codex Web or from another machine.

## What Can Move To Codex Web

The reliable portable unit is the GitHub repository:

```text
https://github.com/g-yeo11/m45-webflow-custom-code
```

Codex Web can work from that repo, read `AGENTS.md`, edit files, regenerate the footer payload, and create commits or pull requests.

The live desktop browser session and Webflow login state do not move automatically. Webflow publishing still needs a logged-in Webflow session.

## Recommended Codex Web Startup Prompt

Paste this into a new Codex Web task after selecting the GitHub repo:

```text
We are editing the M45 Capital Partners Webflow site.

Repository:
https://github.com/g-yeo11/m45-webflow-custom-code

Before making changes, read AGENTS.md, README.md, CHANGELOG.md, docs/AI_AGENT_HANDOFF.md, docs/CODEX_WEBFLOW_OPERATIONS.md, docs/WEBFLOW_EDITING_RUNBOOK.md, and docs/QA_CHECKLIST.md.

Live website:
https://www.m45capital.com

Webflow custom-code page:
https://webflow.com/dashboard/sites/m45capital/custom-code

Important operating model:
- Edit m45-site.js as the source.
- Regenerate webflow-footer-inline-full.html after script changes.
- Webflow Head Code must be empty or contain only: <!-- M45 custom behaviour lives in Footer code. -->
- Webflow Footer Code must contain the full webflow-footer-inline-full.html payload.
- Do not reintroduce the old GitHub Pages loader.
- Use What We Do as the visual and animation reference page.
- Verify production with cache-busting URLs after publishing.

If you cannot access Webflow from Codex Web, make the repo changes and tell me exactly what to paste/publish in Webflow.
```

## Recommended Workflow From Another Machine

1. Open Codex Web.
2. Connect/select the GitHub repo `g-yeo11/m45-webflow-custom-code`.
3. Use the startup prompt above.
4. Let Codex Web make repo changes and produce a commit or PR.
5. Review the generated `webflow-footer-inline-full.html`.
6. From a logged-in Webflow session, paste the payload into global Footer Code.
7. Save and publish staging and production.
8. Verify production with the QA checklist.

## What Codex Web Should Not Do

- Do not assume it can publish Webflow unless a logged-in browser session is explicitly available.
- Do not ask for or store Webflow passwords in repo files.
- Do not put private client data, access tokens, or secrets in Webflow custom code.
- Do not use direct PDF URLs for social sharing pages when unique Open Graph previews are required; use real Webflow/CMS paper pages.

## When Desktop Codex Is Still Better

Use desktop Codex or a human Webflow session when the task requires:

- Visual Webflow Designer edits.
- CMS entry updates through Webflow UI.
- Pasting and publishing global custom code.
- Comparing browser screenshots side by side.
- Checking mobile menu interactions on the actual published site.

## Handoff Checklist

Before handing off to another Codex task:

- Commit and push the latest repo changes.
- Add a `CHANGELOG.md` entry.
- State whether Webflow was published.
- State the production URL and cache-busting verification URL.
- State any known visual or behavior gaps.
