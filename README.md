# 7-Day Leads Sprint Blueprint

The exact 5-step system to get a business ranking on Google + AI search, converting visitors, and bringing in leads inside 30 days. Build it in seven days with Claude.

This is a GitHub Template. Click **Use this template** at the top of the repo to fork your own copy.

Full blueprint and explainer: **https://theagency.io/sprint**

## The seven modules

| # | Module | Folder | Job |
|---|---|---|---|
| 01 | Brain | [`brain/`](./brain/) | Knowledge base every other module reads from |
| 02 | Website | [`website/`](./website/) | Ship the AI-search-optimised site on auto-deploy |
| 03 | Custom strategy | [`custom-strategy/`](./custom-strategy/) | Capture leads with a 5-question multi-step quiz |
| 04 | Email retargeting | [`email-retargeting/`](./email-retargeting/) | Send 10 personalised emails per lead |
| 05 | Ads | [`ads/`](./ads/) | Drive paid traffic if organic is not there yet |
| + | Agents | [`agents/`](./agents/) | 24/7 qualify on social, chat, inbox |
| + | Ivy | [`ivy/`](./ivy/) | Manage outbound citations (real AI-search ranking signal) |

## How each folder works

Every skill folder ships with the same shape:

- `SKILL.md` — what it does, when to use it, inputs and outputs
- `README.md` — quick-start for a human
- `config.json` — every tenant-specific value (URLs, brand colours, tier prices)
- `prompts/` — one file per Claude prompt this skill uses

Never hardwire values into prompts. Read from `config.json` so the same skill works for any business.

## The order to run them in

| Day | Module |
|---|---|
| 1 | Brain. Twelve docs in `brain/output/`. Nothing else. |
| 2-3 | Website. Astro + Tailwind on Netlify, auto-deploy from GitHub. robots.txt + llms.txt + schema + FAQ. |
| 4-5 | Custom strategy. React quiz + Netlify function + CRM upsert. |
| 5-6 | Email retargeting. 10-email generation in the function, CRM workflow. |
| 7 | Ads (if you need traffic) or Agents. |

Each module reads from the previous. Skip the order and you redo work.

## Stack assumed

- **GitHub** for source
- **Netlify** for hosting + auto-deploy on every push
- **Astro + Tailwind + pnpm** (React for interactive components only)
- **GoHighLevel** for CRM
- **Claude** (claude.ai for chat, Claude Code for in-repo work)
- **Microsoft Clarity, Google Search Console, GA4** for tracking

Swap any of these. The prompts read from `config.json`, not from hardwired tool names.

## Getting started

1. Click **Use this template** at the top of this repo
2. Open the new copy in Claude Code (or your preferred editor)
3. Fill out `intake.template.json` and rename to `intake.json`
4. Start with `brain/` — paste `brain/prompts/01-brain-build.md` into Claude
5. Move to `website/` once `brain/output/` has all 12 documents

## License

MIT. Use freely.
