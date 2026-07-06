# QA Checklist

Run this after any Webflow or custom-code change.

## Desktop Pages

Check these pages:

- `/`
- `/our-investment-philosophy`
- `/what-we-do`
- `/our-leadership`
- `/newsroom`
- `/research-insights`

For each page:

- Header logo appears correctly.
- Desktop nav order is correct.
- `Research & Insights` appears exactly once.
- Current page has an underline.
- Hovering nav labels shows an underline.
- Page-load animation feels consistent with `What We Do`.
- First-scroll reveal timing feels consistent with `What We Do`.
- `Get In Touch` hover animation matches other pages.
- `Get In Touch` opens the side panel.
- Contact panel content and map behaviour work.
- Footer matches the reference page style.

## Mobile Pages

Check at mobile width or on a phone:

- Hamburger appears.
- Hamburger opens with the same animation across pages.
- Menu items appear in correct order.
- Mobile arrows stay at the top of each menu item.
- `Research & Insights` appears exactly once.
- `Get in Touch` and email/address content appear correctly.
- Mobile menu open/close animation matches the other pages.

## What We Do

Desktop:

- `Investment Management` appears before `Wealth Management`.
- `Investment Management` is the default visible tab.
- Switching to `Wealth Management` fades content in automatically.

Mobile:

- Investment/Wealth controls are visible between the hero text and content.
- Tapping either section opens the correct content.
- Text remains readable over image backgrounds.

## Our Leadership

Desktop and mobile:

- Jason appears first.
- Leland appears last.
- Other leaders are ordered alphabetically inside their categories.
- Category separation is subtle and clean.

## Research & Insights

Desktop:

- Hero height and text position match the rest of the site.
- Nav typography matches the rest of the site.
- Featured document shows `The M45 Way`.
- Featured teaser appears in the left panel.
- Filters are:
  - `All`
  - `Whitepapers`
  - `Value-Chain`
  - `Company`
  - `Others`
- Document cards show correct title, category, date, and description.
- `View PDF` opens the modal reader.
- Modal can be closed.
- `Open PDF` opens the PDF directly.
- `Share` opens the share popover.
- Copy, LinkedIn, and WhatsApp actions work.

Mobile:

- Research page animation and layout feel consistent with `What We Do`.
- Featured teaser appears.
- Filters are usable and do not overflow awkwardly.
- `View PDF` opens the native PDF directly.
- Native PDF can be scrolled and pinch-zoomed.
- Share opens native share sheet where supported.

## Automated Nav Check

Use this from the local machine if Playwright is available:

```powershell
$node='C:\Users\gordo\.cache\codex-runtimes\codex-primary-runtime\dependencies\node\bin\node.exe'
$env:NODE_PATH='C:\Users\gordo\.cache\codex-runtimes\codex-primary-runtime\dependencies\node\node_modules;C:\Users\gordo\.cache\codex-runtimes\codex-primary-runtime\dependencies\node\node_modules\.pnpm\node_modules;C:\Users\gordo\.cache\codex-runtimes\codex-primary-runtime\dependencies\node\node_modules'
@'
const { chromium } = require('playwright');
const paths = ['/our-investment-philosophy','/newsroom','/research-insights','/what-we-do','/our-leadership'];
(async () => {
  const browser = await chromium.launch({ headless: true });
  for (const path of paths) {
    const page = await browser.newPage({ viewport: { width: 1440, height: 900 } });
    await page.goto('https://www.m45capital.com' + path + '?nav_verify=' + Date.now(), { waitUntil: 'networkidle', timeout: 45000 });
    await page.waitForTimeout(5000);
    const result = await page.evaluate(() => {
      const sel = document.querySelector('.ri-nav .ri-links') ? '.ri-nav .ri-links' : '.navbar-linkcontainer.w-nav-menu';
      const visible = Array.from(document.querySelectorAll(sel + ' a')).map(a => {
        const r = a.getBoundingClientRect();
        const cs = getComputedStyle(a);
        return { text: a.textContent.replace(/\s+/g, ' ').trim(), x: Math.round(r.x), y: Math.round(r.y), w: Math.round(r.width), fontSize: cs.fontSize, lineHeight: cs.lineHeight, display: cs.display, visibility: cs.visibility };
      }).filter(x => x.display !== 'none' && x.visibility !== 'hidden' && x.w > 0 && x.x >= 0 && x.x < innerWidth && x.y >= 0 && x.y < 180);
      return { visible, researchCount: visible.filter(x => x.text === 'Research & Insights').length };
    });
    console.log(path, JSON.stringify(result, null, 2));
    await page.close();
  }
  await browser.close();
})();
'@ | & $node -
```
