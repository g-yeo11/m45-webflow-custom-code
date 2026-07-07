# Research & Insights Guide

The `Research & Insights` page is the most custom-coded page on the site.

Path:

```text
https://www.m45capital.com/research-insights
```

## Current Document Categories

Current filters:

- `All`
- `Whitepapers`
- `Value-Chain`
- `Company`
- `Others`

## Current Document Inventory

### The M45 Way

Category:

- `Whitepapers`

Month:

- June 2026

Role:

- Featured document

PDF:

```text
https://cdn.prod.website-files.com/67343f335cb71da254f99401/6a47340002795540f3ec82d7_2026%2006%20-%20The%20M45%20Way%2C%20responsible%20for%20the%20whole%20(M45%20Fundamental%20Research).pdf
```

Short card copy:

```text
Responsible for the whole. Our investment philosophy for long-term capital.
```

Featured teaser:

```text
A short note on how we think about investing. It comes out of thirty years across asset classes, strategies and markets, through good runs and bad ones, managing money for institutions and for families, often alongside some of the best investors in their part of the world. One lesson kept coming back. Left to itself, a portfolio drifts into a collection: a bit of this, a bit of that, and one risk quietly running everything underneath. We'd rather build it on purpose. Here's the thinking.
```

Share route:

```text
https://www.m45capital.com/the-m45-way
```

### Global Luxury

Category:

- `Value-Chain`

Month:

- May 2026

PDF:

```text
https://cdn.prod.website-files.com/67343f335cb71da254f99401/6a475dfd5a4e97910bd49371_2026%2005%20-%20Global%20Luxury%2C%20the%20business%20of%20saying%20no%20(M45%20Fundamental%20Research).pdf
```

Short card copy:

```text
The business of saying no. A value-chain lens on scarcity, pricing power and discipline across global luxury.
```

Share route:

```text
https://www.m45capital.com/global-luxury
```

### AI Foundation Models

Category:

- `Value-Chain`

Month:

- April 2026

PDF:

```text
https://cdn.prod.website-files.com/67343f335cb71da254f99401/6a475dfdf2edbbeda162a23f_2026%2004%20-%20AI%20Foundation%20Models%2C%20where%20physics%20does%20the%20pricing%20(M45%20Fundamental%20Research).pdf
```

Short card copy:

```text
Where physics does the pricing. A value-chain view of compute, infrastructure and model economics.
```

Share route:

```text
https://www.m45capital.com/ai-foundation-models
```

## Adding A New Paper

1. Upload the PDF to Webflow assets.
2. Copy the Webflow CDN URL.
3. Add the document to the `RESEARCH_DOCS` array in `m45-site.js`.
4. If it needs a clean share route, add the route to:
   - `PAPER_REDIRECTS`
   - the `pagePath` field in the relevant `RESEARCH_DOCS` item
5. Run the JavaScript syntax check.
6. Commit and push.
7. Regenerate `webflow-footer-inline-full.html`, paste it into Webflow Footer Code, and publish.
8. Publish Webflow.
9. Test desktop and mobile.
10. Add a changelog entry.

## Featured Paper

The featured paper is currently `The M45 Way`.

To change the featured paper:

- Move the desired paper to the first item in `RESEARCH_DOCS`, or update all `RESEARCH_DOCS[0]` assumptions in `m45-site.js`.
- Update `FEATURE_TEASER`.
- Update the paper PDF URL, title, month, category, summary, slug, and page path.
- Test both desktop and mobile.

## Webflow Designer Vs Preview

The Research page has old static fallback markup inside Webflow Designer, using classes such as:

- `research-main-native`
- `research-feature-native`
- `research-feature-art`
- `research-feature-copy`
- `research-controls-native`
- `research-grid-native`

The live and previewed page is normalized by the canonical renderer in `m45-site.js`.

Important:

- Webflow pure Design mode may still show the static fallback before custom code runs.
- Webflow Preview mode with `Enable custom code?` switched on should show the actual page state.
- The canonical renderer detects the public `/research-insights` path and the Webflow Designer page id `6a45c8c48cc62e907de14ae2`.
- If Designer Preview does not match production, first check whether `Enable custom code?` is on.
- If pure Design mode must visually match without preview, rebuild the native Webflow elements manually to mirror `RESEARCH_DOCS`.

## PDF Viewing Behaviour

Desktop:

- PDF links open in a modal reader.
- The user can close the modal and remain on the page.
- The user can also select `Open PDF`.

Mobile:

- PDF links open the native PDF file directly.
- This is intentional because native mobile PDF viewing supports sharper rendering and pinch zoom.

## Sharing Behaviour

Each PDF card has a `Share` action.

Desktop:

- Opens a small share popover.
- Offers:
  - Copy link
  - LinkedIn
  - WhatsApp

Mobile:

- Uses the native share sheet when available.
- Falls back to the share popover.

Important social preview note:

- Social platforms scrape metadata from the URL being shared.
- JavaScript-created page changes are often ignored by social crawlers.
- For paper-specific LinkedIn and WhatsApp previews, real Webflow CMS detail pages are the best long-term solution. See `docs/WHITEPAPER_SHARING_PAGES.md`.
