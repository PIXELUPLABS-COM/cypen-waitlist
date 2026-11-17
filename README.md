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
4. **Share image URL.** The social share card (`cypen-assets/og-image.png`, 1200×630, from Figma `591:3351`) is linked with a relative path in the `og:image` and `twitter:image` tags in `index.html`. Change both to the full URL on the live domain, or link previews on Slack, LinkedIn, X and WhatsApp won't show the image.

## Layout

- **1180px and wider:** the Figma desktop layout on a 1440px stage, scaled to the window.
- **640–1179px (tablet):** a stacked layout.
- **Under 640px (phone):** the stacked layout with a single-column form and alerts.

In the stacked layout the Problem section keeps its background: the faint pattern texture across the whole section and the green, orange and pink tiles in its top corners. The Solution illustration is drawn stronger there than in the desktop design (brighter window, code and chart), because it is shown smaller.

The hero always fills the first screen (100vh). On desktop the pattern scales up to cover the taller hero and the sections below move down to match; `fit()` in `index.html` sets this on load and resize.

## Motion

- **Nav:** the links scramble in like the headline, one after another on load, and again whenever one is hovered. The PIXELUPLABS link in the footer does the same when it first scrolls into view and on hover.
- **Hero:** the headline scrambles in. The pattern below it is a static image.
- **Section labels:** the eyebrow labels crawl in and their text decodes.
- **Problem:** scrolljacked on desktop. When the section reaches the top of the window the page holds there, and scrolling brings the three cards in one at a time (left, right, bottom). After the third card the page scrolls on. It plays once. On tablet and phone there is no hold; each card appears as it scrolls into view.
- **Solution:**
  - The Data Exfiltration and Phishing alerts travel down from Problem into Solution as you scroll, and gain a severity row as they land.
  - The dashboard drifts and zooms slowly, with a slight parallax on mouse move.
- **Footer:** static. The orange pattern on the right doesn't animate.

The alert travel is desktop only. Everything is off for visitors with reduced motion turned on.

## Files

| Path | What it is |
| --- | --- |
| `index.html` | The page: markup, CSS and JS in one file |
| `cypen-assets/*.webp, *.png, *.jpg` | Pattern artwork and textures exported from Figma. The paper textures have Figma's linear-burn blend baked in. |
| `cypen-assets/made-heart.svg`, `pixelup-mark.svg` | The heart and the PixelUp mark in the footer's "Made with … by PIXELUPLABS" credit |
| `cypen-assets/og-image.png` | Social share card (1200×630) |
| `cypen-assets/dash/*.svg` | The Solution dashboard's layers from Figma. The window is built in HTML from these so it stays see-through, as in the design. |
| `cypen-assets/*.svg` | Icons, logo mark and the Cypen wordmark |
| `cypen-assets/fonts/` | Design fonts (see the licensing note above) |
