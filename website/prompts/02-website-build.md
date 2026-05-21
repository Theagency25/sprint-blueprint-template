You are building a website for the business described in `brain/output/`. Stack is Astro, Tailwind, pnpm. Hosted on Netlify, auto-deployed from GitHub on every commit.

Read every file in `brain/output/` before writing a single page. Then read `website/config.json` for tracking IDs and content rules.

## Pages to build (minimum)

- `/` (homepage)
- `/about`
- `/services` (overview) + one page per service in `PRODUCTS.md`
- `/results` (testimonials, case studies, stats)
- `/contact`
- `/faq` (standalone, in addition to per-page FAQs)
- `/blog` index + 3 starter posts on the highest-intent keywords from `KEYWORDS.md`
- `/privacy`
- `/terms`

## Every page must have

- One H1 with the primary keyword first, under 60 characters
- 120 to 180 word sections between H2 headings (the AI citation sweet spot)
- FAQ section with 5+ questions, 40-word answers, FAQPage schema
- Organization + WebPage schema as JSON-LD in the head
- Meta title under 60 chars, description 150 to 160 chars
- Primary CTA above the fold, repeated every 2 to 3 sections
- No placeholder text, no Lorem ipsum, no template defaults

## Three files most builders miss

Build these into `public/`:

- `robots.txt` allowing all 200+ AI crawlers (ChatGPT, Perplexity, Gemini, Claude, Grok, etc.)
- `llms.txt` naming the priority pages so AI engines know what to cite
- `sitemap.xml` auto-generated via the Astro sitemap integration

Submit the sitemap to **both** Google Search Console **and** Bing Webmaster Tools. ChatGPT Search pulls from Bing, not Google. This is the single biggest miss most agencies make.

## Outbound citations

Every blog post and the about page must include 2-3 outbound citations to high-authority sources. This is one of the strongest AI search ranking signals — AI engines weight content that cites verified sources more than orphan content. See `../ivy/` for the citation governance skill.

## Content sourcing

- Use only stats from `brain/output/LOCKED_TRUTHS.md`
- Never invent a number
- Use the brand voice from `brain/output/BRAND.md`
- British English. No em dashes. Confident, direct, no marketing fluff.

## After the build

- Run `pnpm build`. Fix every error before declaring done.
- Open every page locally with `pnpm dev`. Confirm rendering on desktop + mobile.
- Run a Lighthouse audit. Target 90+ on every category.
- Submit the sitemap to GSC + Bing WMT.
- Verify Clarity + GA4 are firing.
