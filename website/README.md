# 02 · Website

Ship the AI-search-optimised site on auto-deploy from GitHub to Netlify. Built right, this ranks inside 30 days.

## Stack

- **GitHub** — source of truth, every commit triggers a build
- **Netlify** — auto-deploy on push, free SSL, edge functions
- **Astro + Tailwind + pnpm** — fast static site, React only where you need interactivity

## What you get out

A live site at your domain with:

- All required pages (homepage, about, services overview + one per service, results, contact, FAQ, blog, privacy, terms)
- `robots.txt` allowing 200+ AI crawlers
- `llms.txt` naming priority pages for AI engines
- JSON-LD schema on every page (Organization, FAQPage, LocalBusiness)
- 120-180 word sections between H2s (the AI citation sweet spot)
- 40-word FAQ answers
- Microsoft Clarity + Search Console + GA4 wired

## Run it

1. Make sure `../brain/output/` is complete first
2. Open `prompts/02-website-build.md`
3. Paste into Claude Code with this repo open
4. Claude reads `brain/output/` and builds every page

## Watch out for

- Stock photos, template defaults, "sound familiar?" copy. Strip all of it.
- Sections shorter than 120 words. AI engines need the density to cite.
- Missing schema. Every page needs at least Organization + WebPage.
- Forgetting to submit the sitemap to **Bing Webmaster Tools**. ChatGPT Search pulls from Bing, not Google.
