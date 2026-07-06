# Visual Style & Animation Guide

This guide describes the visual and interaction standards future editors should preserve when changing the M45 Capital Partners Webflow site.

Use `What We Do` as the primary reference page for spacing, typography, nav behaviour, hero height, first-load animation, tab animation, contact-panel animation, and footer styling.

Reference URL:

```text
https://www.m45capital.com/what-we-do
```

## Overall Visual Language

The site should feel:

- Quiet
- Institutional
- Editorial
- Precise
- Spacious
- Premium without looking decorative

Avoid:

- Heavy gradients
- Decorative blobs or orbs
- Rounded card-heavy SaaS layouts
- Marketing-style hero sections
- Overly large new typography that does not match existing pages
- New colours that pull the site away from the navy, off-white, grey, and muted blue system

## Core Colour System

Approximate current palette:

- Near-black navy hero background: `#111218` to `#13141b`
- Deep blue panel: `#292f40`
- Off-white page background: `#f7f7f5` or close Webflow equivalent
- Footer grey: light warm grey used on existing pages
- Text dark navy: `#292f40`
- Muted body grey: grey used across existing paragraph text
- Accent muted blue: used subtly in inactive mobile nav states

When adding new UI:

- Prefer existing Webflow classes first.
- If CSS is needed, sample from existing page colours.
- Do not introduce a new dominant colour family.

## Typography

The site uses a serif display voice for headings and a restrained sans-serif for metadata/body support.

Current observed conventions:

- Heading/display: `Ovo`
- Body/metadata/support: `Zen Kaku Gothic Antique`
- Desktop nav typography should match the canonical nav script:
  - `font-size: 18.375px`
  - `line-height: 25.375px`
  - `font-weight: 400`
  - `letter-spacing: 0`
- Metadata labels use wide letter spacing and uppercase.

Rules:

- Do not scale font sizes with viewport width.
- Keep letter spacing normal for main headings and nav.
- Use uppercase tracking only for labels, categories, metadata, and small eyebrow text.
- Match display text to its container size.

## Global Navigation

Expected desktop order:

1. `Our Investment Philosophy`
2. `What We Do`
3. `Our Leadership`
4. `Newsroom`
5. `Research & Insights`
6. `Get In Touch`

Expected behaviour:

- Current page has a fine underline.
- Hovering a nav item shows a fine underline.
- Nav labels sit on one line on desktop.
- `Research & Insights` should appear exactly once.
- Font size and baseline should be consistent across pages.

Important:

- If a nav item looks different on one page, check whether that page uses a custom header structure.
- The canonical nav block in `m45-site.js` normalizes this across pages.

## Hero Sections

`What We Do` is the reference for dark hero height and text placement.

Expected dark hero behaviour:

- Large dark field with generous top space.
- Text sits low in the hero, not near the top.
- Bottom of hero aligns consistently before the next section begins.
- New pages should preserve this rhythm unless the page intentionally uses a different template.

For `Research & Insights`:

- The dark hero should feel aligned with `What We Do`.
- The `Research Library / Research & Insights / description` text block should sit in the same visual zone as the `What We Do` hero headline.
- Page-load animation should match the general feel of the rest of the site.

## Page Load Animation

Expected:

- Content should appear with a restrained fade or subtle movement.
- Animation should not feel delayed or empty.
- No section should show as blank until the user moves the mouse.

Known issue previously fixed:

- On `What We Do`, `Wealth Management` content previously stayed empty until a mouse movement triggered the fade. Any future tab or filter changes should trigger their own reveal automatically.

## First Scroll / Reveal Animation

Expected:

- As the page begins scrolling, content should reveal smoothly and at similar timing across pages.
- Research cards, featured panels, and footer should not pop in with a different style from other pages.

When rebuilding a page:

- Compare with `What We Do` at the same viewport width.
- Check both first page load and first scroll.
- Check whether the user needs to interact before animation starts; they should not.

## Tabs, Filters, And Accordions

`What We Do` reference:

- Tab labels are full-width horizontal controls on desktop.
- On mobile, Investment/Wealth controls should remain visible between the hero and content.
- Content fade should start immediately after click/tap.

`Research & Insights` reference:

- Filters should use the same restrained visual system:
  - Thin borders
  - Uppercase tracked labels
  - Dark active state
  - Quiet transition
- Cards should hide/show without abrupt page jumping where possible.

## Mobile Menu

Expected:

- Hamburger open/close animation should match across all pages.
- Menu panel style should match the existing pages, especially `What We Do`.
- Mobile arrows should stay at the top of each nav item, not below the label.
- Inactive/active nav states should be visually consistent.
- `Research & Insights` should appear exactly once.

Known custom-code support:

- `m45-site.js` includes a mobile menu arrow normalization block.

## Get In Touch Interaction

Expected desktop behaviour:

- Hover shows the same arrow animation as on `What We Do`.
- Clicking opens the same right-side contact panel.
- The side panel width, background, typography, and map area should match across pages.
- `Locate Us` should point to the official Google Maps URL.

Expected mobile behaviour:

- Contact details appear in the mobile menu in the same style as other pages.
- Address and email are legible and not cramped.

## Footer

Use `What We Do` as the reference.

Expected:

- Same grey background height.
- Same typography, colour, and spacing.
- Same placement of:
  - `M45 Capital Partners`
  - Address
  - Copyright
  - MAS disclaimer
- No extra dark blue band above the footer unless intentionally part of the page design.

If a new page footer looks different:

- Compare container height.
- Compare top padding and bottom padding.
- Compare legal disclaimer line wrapping.
- Compare text colour and font size.

## Research & Insights Visual Contract

Research & Insights should look like a native M45 page, not a separate microsite.

Preserve:

- Dark hero height and text position aligned to `What We Do`.
- Header/nav typography aligned to the rest of the site.
- Featured panel with deep blue right side.
- Featured teaser in the left side panel.
- Document filter controls with restrained borders.
- Document cards with quiet editorial spacing.
- Footer matching `What We Do`.

Avoid:

- Oversized hero title.
- Extra dark bands near the footer.
- Footer height or disclaimer wrapping that differs from other pages.
- Nav labels wrapping to multiple lines on desktop.
- Generic web-app style cards or buttons.

## PDF Modal Visual Contract

Desktop:

- Modal should feel like a refined overlay, not a separate app.
- Background blur/dimming should keep page context visible.
- Modal should be tall enough to read comfortably.
- Header should include:
  - Paper title
  - `Open PDF`
  - Close button

Mobile:

- PDF should open natively, not in a small embedded frame.
- Reason: native PDF gives sharper rendering and pinch zoom.

## Whitepaper Share UI

Expected:

- `Share` should be understated and sit near `View PDF`.
- Desktop share popover should be clean and compact.
- LinkedIn and WhatsApp actions may use compact icons.
- Share URLs should point to paper-specific landing pages once those exist.

See:

- `docs/WHITEPAPER_SHARING_PAGES.md`

## Visual QA Method

Whenever a visual change is made:

1. Open the changed page and `What We Do` side by side.
2. Compare:
   - Header logo size
   - Nav font size
   - Nav spacing
   - Current underline
   - Hero height
   - Hero text baseline
   - First section spacing
   - Footer height
   - Footer text wrapping
3. Test desktop width around `1440px`.
4. Test laptop width around `1280px`.
5. Test tablet/mobile widths around `767px`, `479px`, and a real phone if available.
6. Check interactions:
   - Page load
   - First scroll
   - Hover nav
   - Open mobile menu
   - Click tabs/filters
   - Open Get In Touch
   - Open and close PDF modal
   - Share a paper

## When In Doubt

If a page does not match:

1. Treat `What We Do` as the reference.
2. Match structure before tweaking numbers.
3. Prefer Webflow-native classes and interactions.
4. Use small custom CSS only when Webflow's structure differs.
5. Document the final decision in `CHANGELOG.md`.

