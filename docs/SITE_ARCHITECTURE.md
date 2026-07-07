# Site Architecture

This document describes how the M45 Capital Partners Webflow site is structured and where custom behaviour lives.

## Hosting Model

Webflow owns:

- Page structure
- CMS/content editing
- Page publishing
- Base styles and interactions
- Static assets uploaded to Webflow's CDN

This repository owns:

- The JavaScript source file `m45-site.js`
- The final Webflow footer payload `webflow-footer-inline-full.html`
- Documentation for future maintenance
- Change history through Git commits and `CHANGELOG.md`

Production runs the inline payload pasted into the Webflow global Footer Code field:

```text
webflow-footer-inline-full.html
```

Webflow global Head Code should remain empty.

## Main Pages

### Home

Path:

- `/`

Purpose:

- Brand introduction
- About section
- Quick access links
- Footer

Known custom-code responsibilities:

- Global nav cleanup and `Research & Insights` insertion
- Mobile menu arrow normalization

### Our Investment Philosophy

Path:

- `/our-investment-philosophy`

Purpose:

- Investment philosophy page

Known custom-code responsibilities:

- Global nav cleanup and `Research & Insights` insertion
- Mobile menu arrow normalization

### What We Do

Path:

- `/what-we-do`

Purpose:

- Investment Management and Wealth Management content
- Tabbed/accordion style sections

Known custom-code responsibilities:

- Global nav cleanup and `Research & Insights` insertion
- Mobile menu arrow normalization

Important content conventions:

- `Investment Management` should appear before `Wealth Management`.
- `Investment Management` should be the default visible section.
- Mobile should show the same two section controls as desktop.

### Our Leadership

Path:

- `/our-leadership`

Purpose:

- Leadership biographies

Known content conventions:

- Jason appears first as a standalone leader.
- Leland appears at the end as a standalone leader.
- Remaining leaders are grouped visually by broad category:
  - Investments
  - Wealth Management
  - Operations
- People inside each category should be alphabetical unless there is a specific editorial reason otherwise.

### Newsroom

Path:

- `/newsroom`

Purpose:

- Announcements and media coverage

Known custom-code responsibilities:

- Global nav cleanup and `Research & Insights` insertion
- Mobile menu arrow normalization

### Research & Insights

Path:

- `/research-insights`

Purpose:

- Research and whitepaper library
- Featured document
- Category filters
- PDF viewing and sharing

Known custom-code responsibilities:

- Most Research & Insights page behaviour is in `m45-site.js`.
- See `docs/RESEARCH_INSIGHTS.md`.
- Visual and animation parity should follow `docs/VISUAL_STYLE_AND_ANIMATIONS.md`.

## Shared Components

### Global Header

Expected desktop nav order:

1. `Our Investment Philosophy`
2. `What We Do`
3. `Our Leadership`
4. `Newsroom`
5. `Research & Insights`
6. `Get In Touch`

Custom code ensures:

- `Research & Insights` exists on every page.
- Duplicates are removed.
- Nav typography and spacing are normalized.
- Current page underline appears.
- Hover underline appears.

### Mobile Menu

Expected menu order:

1. `Our Investment Philosophy`
2. `What We Do`
3. `Our Leadership`
4. `Newsroom`
5. `Research & Insights`
6. `Get in Touch`
7. `IR@M45CAPITAL.COM`

Custom code ensures:

- Mobile arrows stay at the top of each menu item.
- `Research & Insights` appears exactly once.
- Mobile menu styling is aligned with the rest of the site.

### Get In Touch Panel

Expected behaviour:

- Hovering over `Get In Touch` shows the same arrow animation as other pages.
- Clicking opens the side contact panel.
- `Locate Us` should point to the official Google Maps URL supplied by M45 Capital Partners.

### Footer

Expected content:

- `M45 Capital Partners`
- `Centennial Tower #20-01`
- `3 Temasek Avenue Singapore 039190`
- Copyright line
- MAS licence disclaimer

Expected design:

- Match the footer dimensions, typography, spacing, and colour treatment used on `What We Do`.
