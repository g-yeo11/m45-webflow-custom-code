# M45 Capital Partners Webflow Custom Code

This repository is the source of truth for custom behaviour and technical documentation for the M45 Capital Partners Webflow site.

The production site is hosted and published by Webflow. The live custom behaviour should live directly in Webflow global Footer Code, copied from `webflow-footer-inline-full.html`. This repo remains the version-controlled working copy, documentation home, and changelog.

## Live Integration

Production site:

- [m45capital.com](https://www.m45capital.com/)
- [Research & Insights](https://www.m45capital.com/research-insights)

Webflow custom-code page:

- [Custom code settings](https://webflow.com/dashboard/sites/m45capital/custom-code)

Canonical source files:

- `m45-site.js`: main site behaviour.
- `webflow-footer-inline-full.html`: the exact one-script payload to paste into Webflow Footer Code.

## Documentation

- [Changelog](CHANGELOG.md)
- [Site Architecture](docs/SITE_ARCHITECTURE.md)
- [Custom Code Reference](docs/CUSTOM_CODE_REFERENCE.md)
- [Visual Style & Animation Guide](docs/VISUAL_STYLE_AND_ANIMATIONS.md)
- [Research & Insights Guide](docs/RESEARCH_INSIGHTS.md)
- [Whitepaper Sharing Pages Guide](docs/WHITEPAPER_SHARING_PAGES.md)
- [Webflow Editing Runbook](docs/WEBFLOW_EDITING_RUNBOOK.md)
- [Codex Webflow Operations Guide](docs/CODEX_WEBFLOW_OPERATIONS.md)
- [QA Checklist](docs/QA_CHECKLIST.md)
- [AI Agent Handoff Notes](docs/AI_AGENT_HANDOFF.md)

## Current Webflow Custom Code Contract

Head Code:

```html
<!-- empty -->
```

Footer Code:

```html
<!-- paste the full contents of webflow-footer-inline-full.html -->
```

The footer payload is generated from `m45-site.js` and should contain one `<script>` tag. The final Research & Insights featured-card recovery lives inside `m45-site.js`, so Webflow only has to preserve one inline script.

## Standard Update Flow

1. Edit `m45-site.js` or the documentation in this repo.
2. Regenerate `webflow-footer-inline-full.html`.
3. Run JavaScript syntax checks on `m45-site.js`.
4. Paste `webflow-footer-inline-full.html` into Webflow global Footer Code.
5. Clear Webflow Head Code.
6. Save and publish Webflow to staging and production.
7. Run the desktop and mobile QA checklist.
8. Add a dated entry to [CHANGELOG.md](CHANGELOG.md).
9. Commit and push this repo.

For Codex-assisted edits, read [Codex Webflow Operations Guide](docs/CODEX_WEBFLOW_OPERATIONS.md) before touching Webflow. It documents the Webflow navigation workflow, save/publish sequence, verification checks, and common failure modes learned from prior edits.
