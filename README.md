# M45 Capital Partners Webflow Custom Code

This repository is the source of truth for custom behaviour and technical documentation for the M45 Capital Partners Webflow site.

The production site is still hosted by Webflow. Webflow loads the custom JavaScript from GitHub Pages so that the Webflow custom-code fields stay small, readable, and below Webflow's character limit.

## Live Integration

Production site:

- [m45capital.com](https://www.m45capital.com/)
- [Research & Insights](https://www.m45capital.com/research-insights)

Hosted script:

- [m45-site.js](https://g-yeo11.github.io/m45-webflow-custom-code/m45-site.js)

Webflow footer loader:

```html
<script src="https://g-yeo11.github.io/m45-webflow-custom-code/m45-site.js?v=YYYYMMDDHHMM"></script>
```

When `m45-site.js` changes, commit and push to `main`, then update the `v=` query string in Webflow and publish if browsers need to pick up the change immediately.

## Documentation

- [Changelog](CHANGELOG.md)
- [Site Architecture](docs/SITE_ARCHITECTURE.md)
- [Custom Code Reference](docs/CUSTOM_CODE_REFERENCE.md)
- [Research & Insights Guide](docs/RESEARCH_INSIGHTS.md)
- [Whitepaper Sharing Pages Guide](docs/WHITEPAPER_SHARING_PAGES.md)
- [Webflow Editing Runbook](docs/WEBFLOW_EDITING_RUNBOOK.md)
- [QA Checklist](docs/QA_CHECKLIST.md)
- [AI Agent Handoff Notes](docs/AI_AGENT_HANDOFF.md)

## Current Webflow Custom Code Contract

The Webflow global custom-code fields should remain minimal:

Head code:

```html
<!-- M45 custom behaviour is loaded from the footer via GitHub Pages: https://g-yeo11.github.io/m45-webflow-custom-code/m45-site.js -->
```

Footer code:

```html
<script src="https://g-yeo11.github.io/m45-webflow-custom-code/m45-site.js?v=YYYYMMDDHHMM"></script>
```

Do not paste the full custom script back into Webflow unless GitHub Pages is unavailable and the tradeoff is intentional.

## Standard Update Flow

1. Edit `m45-site.js` or the documentation in this repo.
2. Run a JavaScript syntax check.
3. Commit and push to `main`.
4. If `m45-site.js` changed, bump the Webflow loader query string.
5. Publish Webflow to staging and production.
6. Run the desktop and mobile QA checklist.
7. Add a dated entry to [CHANGELOG.md](CHANGELOG.md).
