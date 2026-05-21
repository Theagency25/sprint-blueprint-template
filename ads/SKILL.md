# ads — Skill definition

## Purpose

Drive paid traffic to the custom-strategy quiz when organic is not there yet.

## When to use

- After the website and strategy quiz are live and proven (test submission lands a real GHL contact)
- Only if organic SEO + social are not yet sending enough traffic

## Input

- `brain/output/CUSTOMERS.md` (pain points + language)
- `brain/output/BRAND.md` (voice)
- Strategy page URL
- Meta Ads Manager account + Pixel installed

## Output

- 10 visual variants in `ads/creatives/` (HTML, exportable to PNG via Puppeteer or screenshot)
- 10 copy variants in `ads/copy.md`
- Launch settings + monitoring sheet

## Tools

- Meta Ads Manager (or Google Ads — adapt the prompt)
- HTML / Canva for creatives
- Meta Pixel + GA4 for tracking

## Launch settings (defaults — override in `config.json`)

- Campaign objective: Lead generation
- Daily budget: $30-$50 for the test
- Audience: lookalike of existing customers OR narrow interest-based, never broad
- Optimisation: form completions on `/custom-strategy`

## Kill / scale rules

- Kill any creative after 100 clicks if CPL is more than 2× target
- Scale the winner only when CPL is under target for 7 consecutive days
