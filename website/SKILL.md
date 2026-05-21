# website — Skill definition

## Purpose

Ship the AI-search-optimised website on auto-deploy. Reads from `brain/output/`, outputs a live site that ranks inside 30 days.

## When to use

- After `brain/` is complete
- For any new pages added later
- When schema or robots.txt needs updating

## Input

- Everything in `brain/output/`
- `intake.json` for domain, social links, logo
- This skill's `config.json`

## Output

- Astro project in `website/src/`
- Deployed to Netlify, auto-deploys on every commit
- All required pages, schema, robots.txt, llms.txt, sitemap

## Tools

- Claude Code (for in-repo work)
- GitHub (source of truth, auto-deploy trigger)
- Netlify (hosting + functions)
- Microsoft Clarity (heatmaps, free)
- Google Search Console (query data)
- Google Analytics 4 (conversion tracking)
- Bing Webmaster Tools (ChatGPT Search source — do not skip)

## Pages (minimum)

| Page | Purpose |
|---|---|
| `/` | Homepage |
| `/about` | Founder story, credibility |
| `/services` | All services overview |
| `/services/[slug]` | One page per service |
| `/results` | Testimonials, case studies |
| `/contact` | Booking, location, form |
| `/faq` | Standalone FAQ in addition to per-page |
| `/blog` + 3 starter posts | Topical authority |
| `/custom-strategy` | The quiz (next skill) |
| `/privacy`, `/terms` | Required by Google |

## Audit before complete

- [ ] `pnpm build` exits 0
- [ ] Every page renders desktop + mobile
- [ ] No placeholder text (`UPDATE:`, `Lorem ipsum`)
- [ ] FAQ with FAQPage schema on every page
- [ ] Organization schema with `sameAs` for every social profile
- [ ] `public/robots.txt` allowing 200+ AI crawlers
- [ ] `public/llms.txt` naming priority pages
- [ ] Sitemap submitted to Google Search Console **and** Bing Webmaster Tools
- [ ] Microsoft Clarity + GA4 firing
- [ ] Lighthouse 90+ on all categories
