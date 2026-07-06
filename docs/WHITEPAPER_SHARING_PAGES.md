# Whitepaper Sharing Pages Guide

This guide explains the recommended long-term setup for sharing M45 Capital Partners whitepapers cleanly on LinkedIn, WhatsApp, email, and direct messages.

## Goal

Each whitepaper should have its own public page with:

- A clean URL
- Its own page title
- Its own meta description
- Its own Open Graph preview image
- A clear `View PDF` action
- A share action that points to the page, not directly to the PDF

This lets LinkedIn, WhatsApp, iMessage, Slack, and other platforms show the correct paper title and preview when the link is pasted.

## Why This Matters

Social platforms usually do not execute JavaScript when building link previews. They scrape the raw HTML at the shared URL.

That means a JavaScript route such as:

```text
https://www.m45capital.com/research-insights?paper=global-luxury
```

may still preview as:

```text
Research & Insights | M45 Capital Partners
```

instead of:

```text
Global Luxury | M45 Capital Partners
```

The reliable fix is to create a real Webflow page or CMS detail page for each paper.

## Recommended URL Structure

Use short, stable URLs:

```text
https://www.m45capital.com/research/the-m45-way
https://www.m45capital.com/research/global-luxury
https://www.m45capital.com/research/ai-foundation-models
```

Alternative shorter URLs are acceptable:

```text
https://www.m45capital.com/the-m45-way
https://www.m45capital.com/global-luxury
https://www.m45capital.com/ai-foundation-models
```

Pick one convention and keep it consistent.

## Recommended Webflow CMS Collection

Create a CMS collection called:

```text
Research Papers
```

Recommended fields:

- `Name`
- `Slug`
- `Short Title`
- `Category`
- `Month`
- `Year`
- `Short Description`
- `Featured Teaser`
- `PDF File`
- `Open Graph Image`
- `LinkedIn Share Text`
- `WhatsApp Share Text`
- `Featured`
- `Published`

Optional fields:

- `Author`
- `Series`
- `Reading Time`
- `Hero Eyebrow`
- `SEO Title`
- `SEO Description`

## CMS Detail Page Requirements

Each research paper detail page should include:

- Global M45 header
- Paper title
- Category and date
- Short teaser copy
- `View PDF` button
- `Share` button
- Link back to `Research & Insights`
- Footer matching the rest of the site

The page does not need to duplicate the full PDF content. It can be an elegant landing page whose purpose is to introduce and share the paper.

## SEO And Open Graph Settings

For each CMS detail page, set:

Page title:

```text
{Paper Title} | M45 Capital Partners
```

Meta description:

```text
{Short Description}
```

Open Graph title:

```text
{Paper Title} | M45 Research & Insights
```

Open Graph description:

```text
{Short Description}
```

Open Graph image:

```text
Use the paper-specific preview image.
```

Important:

- Use a proper image, not a PDF file, for the social preview.
- Recommended Open Graph image size: `1200 x 630`.
- Keep text large and minimal because social cards are small.

## Current Papers To Create

### The M45 Way

Recommended URL:

```text
/research/the-m45-way
```

Title:

```text
The M45 Way
```

Category:

```text
Whitepapers
```

Date:

```text
June 2026
```

Description:

```text
Responsible for the whole. Our investment philosophy for long-term capital.
```

PDF:

```text
https://cdn.prod.website-files.com/67343f335cb71da254f99401/6a47340002795540f3ec82d7_2026%2006%20-%20The%20M45%20Way%2C%20responsible%20for%20the%20whole%20(M45%20Fundamental%20Research).pdf
```

### Global Luxury

Recommended URL:

```text
/research/global-luxury
```

Title:

```text
Global Luxury
```

Category:

```text
Value-Chain
```

Date:

```text
May 2026
```

Description:

```text
The business of saying no. A value-chain lens on scarcity, pricing power and discipline across global luxury.
```

PDF:

```text
https://cdn.prod.website-files.com/67343f335cb71da254f99401/6a475dfd5a4e97910bd49371_2026%2005%20-%20Global%20Luxury%2C%20the%20business%20of%20saying%20no%20(M45%20Fundamental%20Research).pdf
```

### AI Foundation Models

Recommended URL:

```text
/research/ai-foundation-models
```

Title:

```text
AI Foundation Models
```

Category:

```text
Value-Chain
```

Date:

```text
April 2026
```

Description:

```text
Where physics does the pricing. A value-chain view of compute, infrastructure and model economics.
```

PDF:

```text
https://cdn.prod.website-files.com/67343f335cb71da254f99401/6a475dfdf2edbbeda162a23f_2026%2004%20-%20AI%20Foundation%20Models%2C%20where%20physics%20does%20the%20pricing%20(M45%20Fundamental%20Research).pdf
```

## Share Button Behaviour

On the Research & Insights listing page:

- `View PDF` should keep the current behaviour:
  - Desktop: opens modal reader
  - Mobile: opens native PDF directly
- `Share` should share the paper's public landing page, not the PDF URL.

On the paper detail page:

- `View PDF` opens the PDF.
- `Share` shares the current detail page URL.

Recommended share destinations:

- Copy link
- LinkedIn
- WhatsApp

## Migration From Current JavaScript Routes

The current script has JavaScript routes:

```text
/the-m45-way
/global-luxury
/ai-foundation-models
```

These routes redirect into:

```text
/research-insights?paper=...
```

Once real Webflow pages exist:

1. Update the share URL map in `m45-site.js` to point to the real pages.
2. Stop redirecting the real page URLs.
3. Keep legacy redirects only if old shared links already exist.
4. Test LinkedIn and WhatsApp previews.

## Verification Checklist

For each paper page:

- Page loads publicly while logged out.
- URL is clean and stable.
- Page title is paper-specific.
- Meta description is paper-specific.
- Open Graph title is paper-specific.
- Open Graph description is paper-specific.
- Open Graph image is paper-specific.
- LinkedIn share shows the paper title.
- WhatsApp share shows the paper title.
- `View PDF` works on desktop.
- `View PDF` works on mobile.
- `Share` uses the paper page URL.
- Back link returns to `Research & Insights`.

## Social Preview Testing

After publishing:

- Paste the page URL into WhatsApp and confirm the preview.
- Use LinkedIn's post composer and confirm the preview.
- If LinkedIn shows old metadata, wait and test again. Social platforms cache previews.

If previews still show the generic Research & Insights title:

- Confirm the URL being shared is the real paper page.
- Confirm Webflow page settings use paper-specific metadata.
- Confirm the page was published.
- Confirm the Open Graph image is reachable publicly.
- Avoid relying on JavaScript to update metadata.

