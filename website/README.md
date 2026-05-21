# Website

A high-level checklist of what your website needs to rank for both Google and AI search engines.

This folder is **instructions, not a build kit**. It tells you what good looks like and the minimum bar to clear. The actual build methodology is part of how we run a Sprint with our clients.

## What good looks like

### Hosting + deploy
- Source in GitHub, hosted on Netlify, auto-deploy on every commit
- SSL on by default (Netlify includes it free)

### Pages (minimum)
- Homepage, About, Services (overview + one per service), Results / Testimonials
- Contact, FAQ (standalone), Blog with 3+ starter posts
- Privacy and Terms (required by Google)
- A lead-capture page (see [`custom-strategy/`](../custom-strategy/))

### Every page must have
- One H1, primary keyword first, under 60 characters
- 120-180 word sections between H2s (the AI citation sweet spot)
- An FAQ section with 5+ questions and ~40-word answers
- JSON-LD schema in the head (at minimum Organization + WebPage; FAQPage on every FAQ)
- A primary CTA above the fold and repeated every 2-3 sections

### Three files most builders miss
- `public/robots.txt` allowing 200+ AI crawlers. A working template lives in [`templates/robots.txt`](./templates/robots.txt) — copy it as-is, change the sitemap URL.
- `public/llms.txt` naming your priority pages so AI engines know what to cite
- `public/sitemap.xml` — and submit it to **both Google Search Console and Bing Webmaster Tools**. ChatGPT Search pulls from Bing, not Google. This is the single biggest miss most agencies make.

### Tracking
- Microsoft Clarity (free heatmaps + session recordings)
- Google Search Console (query data)
- Google Analytics 4 (conversion tracking)

### Citations
Every blog post and key page should include 2-3 outbound citations. This is one of the strongest AI search ranking signals. See [`../ivy/`](../ivy/) — the only full skill in this repo — for how to manage them.

## Stack we recommend

Astro + Tailwind + pnpm. Any modern static site generator works (Next.js, SvelteKit, Eleventy). Pick what your team already knows.

## Want it built for you?

We ship a full Sprint build in seven days. **https://theagency.io/sprint**
