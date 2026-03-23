# Suman Coding Tutor – Website Maintenance Guide

## Project Overview

Static HTML/CSS/JS tutoring website for Suman (Senior Software Engineer & Coding Tutor, Melbourne).
No build tools, no frameworks, no server required — plain files hosted as a static site.

---

## File Structure

```
suman-coding-tutor/
├── index.html          # Home page
├── about.html          # About page
├── services.html       # Services & pricing page
├── contact.html        # Contact / booking form page
├── thanks.html         # Form submission thank-you page
├── footer.html         # Shared footer partial (loaded via JS)
├── style.css           # All site styles
├── main.js             # Shared JS (hamburger menu, active nav, footer loader)
└── readme.md           # This file
```

---

## How the Shared Footer Works

The footer is defined once in `footer.html` and injected into every page by `main.js`.

To **update the footer** (links, contact info, copyright year):
1. Edit `footer.html` only — changes apply to all pages automatically.
2. Do **not** manually edit footer HTML inside individual `.html` files.

> Note: The fetch-based footer loader in `main.js` requires a local server (e.g. VS Code Live Server) to work during development. Opening HTML files directly via `file://` will block the fetch due to CORS. For production, it works normally once deployed.

---

## Common Maintenance Tasks

### Update Navigation Links
- Desktop nav: edit the `<nav>` section inside each `.html` file (or create a shared nav partial similar to the footer).
- Mobile nav: the `.mobile-nav` block inside each `.html` file.

### Update Contact Details
- Edit `footer.html` — email, WhatsApp link, and Superprof profile link are all there.
- Also check `contact.html` if there is a contact section with duplicated details.

### Update Pricing / Services
- Edit `services.html` — all pricing cards and package details are in that file.

### Update the Copyright Year
- Edit the `<p>` tag inside `.footer-bottom` in `footer.html`.

### Add a New Page
1. Create a new `.html` file by copying an existing page (e.g. `about.html`) as a template.
2. Keep the `<head>`, `<nav>`, mobile nav, and footer placeholder consistent.
3. Link to it from the nav in all existing pages.

---

## Styles

All styles are in `style.css`. Key CSS custom properties (design tokens) are defined at the top of the file under `:root`:

- `--navy`, `--navy-mid` — background colours
- `--blue` — accent colour
- `--white`, `--grey` — text colours
- `--max-width` — max content width
- `--font-main`, `--font-code` — font families

To change the colour scheme or spacing, update the `:root` variables — no need to hunt through the file.

---

## JavaScript

`main.js` handles:
- **Hamburger menu** — mobile nav toggle
- **Active nav link** — highlights the current page link in the nav
- **Footer loader** — fetches and injects `footer.html` into `#footer-placeholder`

No external JS libraries or dependencies.

---

## Deployment

This is a static site — deploy by uploading all files to any static hosting provider.
Ensure `footer.html` is uploaded alongside the HTML files (it is fetched at runtime).

---

## SEO / Meta

- Each page has its own `<title>` and `<meta name="description">` — update these if page content changes.
- A `sitemap.xml` should be present at the root of the deployed domain.
- Google Search Console verification meta tag is in `index.html`.

---

## Things to Avoid

- Do not hardcode phone numbers, emails, or profile URLs in multiple places — keep them in `footer.html` and `contact.html` only.
- Do not add inline `<style>` blocks to individual pages unless page-specific — put shared styles in `style.css`.
- Do not commit sensitive keys, tokens, or credentials to this repository.
