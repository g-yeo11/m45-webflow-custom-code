# M45 Webflow Custom Code

This repository hosts the external JavaScript used by the M45 Capital Partners Webflow site.

Webflow loads `m45-site.js` from GitHub Pages to keep the site custom-code field small and avoid Webflow's character limit. The script contains the current Research & Insights document behavior, PDF reader behavior, share tools, contact-map link patch, mobile menu arrow fix, and canonical nav cleanup.

Production loader pattern:

```html
<script src="https://g-yeo11.github.io/m45-webflow-custom-code/m45-site.js?v=YYYYMMDDHHMM"></script>
```

When updating the script, commit and push to `main`, then update the `v=` query string in Webflow if you need browsers to pick up the new version immediately.
