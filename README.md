# Cypen waitlist page

A temporary waitlist landing page for Cypen (continuous attack surface testing). Built by PixelUp from the Figma file "[For Work] Cypen", frame `544:1441` (Temp Landing page).

It's a static page: one `index.html` plus the `cypen-assets/` folder. No build step and no dependencies.

## Run it locally

```bash
python -m http.server 4321
```

Then open http://localhost:4321. Opening `index.html` directly from disk also works, but some browsers block the fonts that way.

## Deploy

Upload `index.html` and the whole `cypen-assets/` folder to any static host (Vercel, Netlify, Cloudflare Pages, S3). Keep the folder structure as it is.

## Before launch

1. **Connect the waitlist form to HubSpot.** In `index.html`, find `const HUBSPOT={portalId:'',formGuid:''};` and fill in the portal ID and form GUID. The form posts the email to HubSpot's public Forms API, so no secret is needed. Until this is set, the form shows a success message but sends nothing. Never put a HubSpot private-app token in this file.
2. **Licence the fonts for web use.** `cypen-assets/fonts/` contains Roobert and Season Sans **trial** builds, plus Paper Mono and PP Mori. Trial fonts aren't licensed for a public website. Buy web licences and swap in the licensed files, keeping the same file names, or update the `@font-face` rules at the top of `index.html`.
3. **Privacy policy.** The Figma design has no privacy policy link. A form that collects emails should normally link to one.

## Layout

- **1180px and wider:** the Figma desktop layout on a 1440px stage, scaled to the window.
- **640–1179px (tablet):** a stacked layout.
- **Under 640px (phone):** the stacked layout with a single-column form and alerts.

## Motion

- **Hero:** the headline scrambles in.
- **Section labels:** the eyebrow labels crawl in and their text decodes.
- **Problem:** the alert cards fade up one after another.
- **Solution:**
  - The Data Exfiltration and Phishing alerts travel down from Problem into Solution as you scroll, and gain a severity row as they land.
  - The dashboard drifts and zooms slowly, with a slight parallax on mouse move.
- **Footer:** the orange swarm grows in from the right.

The alert travel and the swarm growth are desktop only. Everything is off for visitors with reduced motion turned on.

## Files

| Path | What it is |
| --- | --- |
| `index.html` | The page: markup, CSS and JS in one file |
| `cypen-assets/*.webp, *.png, *.jpg` | Pattern artwork and textures exported from Figma. The paper textures have Figma's linear-burn blend baked in. |
| `cypen-assets/*.svg` | Icons, logo mark and the Cypen wordmark |
| `cypen-assets/fonts/` | Design fonts (see the licensing note above) |
