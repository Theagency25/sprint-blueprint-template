# Setup — start to finish

A complete walkthrough from the GitHub "Use this template" button to your first published blog post with entity citations. Plan for ~7 days end-to-end, or just run **Phase 7** today if you only want the Ivy citation skill working.

---

## Phase 0 — Prerequisites (do these first)

You need accounts on:

| What | Why | Free tier OK? |
|---|---|---|
| [GitHub](https://github.com) | Source of truth, auto-deploy trigger | Yes |
| [Netlify](https://www.netlify.com) | Hosting + auto-deploy + serverless functions | Yes |
| [GoHighLevel](https://www.gohighlevel.com) (or your CRM of choice) | Contact storage, custom fields, email workflows | No (~$97/mo) |
| [Claude.ai](https://claude.ai) and/or [Claude Code](https://claude.com/claude-code) | Run the prompts | Yes for claude.ai chat |
| [Microsoft Clarity](https://clarity.microsoft.com) | Heatmaps + session recordings | Yes |
| [Google Search Console](https://search.google.com/search-console) | Query data | Yes |
| [Bing Webmaster Tools](https://www.bing.com/webmasters) | **ChatGPT Search pulls from Bing, not Google. Do not skip this.** | Yes |
| A domain (optional but recommended) | Run your site at a real URL | ~$10/yr |

Skip any of these and the build still works, but the equivalent step in the build will need an alternative.

---

## Phase 1 — Fork the repo

1. Go to https://github.com/Theagency25/sprint-blueprint-template
2. Click the green **Use this template** button at the top
3. Choose **Create a new repository**
4. Name it (e.g. `my-business-leads-sprint`), set to Private if you want
5. Click **Create repository from template**

You now have your own copy of the scaffolding under your GitHub account.

### Clone locally

```
git clone https://github.com/YOUR-USERNAME/YOUR-NEW-REPO.git
cd YOUR-NEW-REPO
```

### Open in your editor

```
code .              # VS Code
# OR
claude .            # Claude Code in this folder (recommended)
```

---

## Phase 2 — Fill out the intake

1. Open `intake.template.json`
2. Save it as `intake.json` (the `.template.json` is in `.gitignore` so your `intake.json` stays out of git)
3. Fill in every field. Be specific. This file is what every downstream module reads from.

Required fields at minimum:
- `business_name`
- `domain`
- `industry`
- `location`
- `founder_name`
- `primary_service`
- `ideal_customer_one_line`
- `tier_pricing`
- `existing_assets.current_website`

Everything else is nice-to-have.

---

## Phase 3 — Module 1: Website (Day 2-3)

### What you are building

A static site at your domain with all the AI-search ranking essentials baked in.

### Steps

1. **Read** [`website/README.md`](./website/README.md) — the full checklist
2. **Initialise** an Astro project at the repo root:
   ```
   pnpm create astro@latest
   ```
   Choose the empty template, install Tailwind when prompted, use TypeScript strict.
3. **Connect Netlify** to your GitHub repo (Netlify dashboard → Add new site → Import from Git). Set the build command to `pnpm build` and the publish directory to `dist`.
4. **Copy the robots.txt** from `website/templates/robots.txt` to `public/robots.txt`. Change the sitemap URL at the bottom to your domain.
5. **Create `public/llms.txt`** naming your priority pages (e.g. homepage, services, FAQ). Format example: `https://llmstxt.org`.
6. **Build the pages** listed in `website/README.md` — homepage, about, services, results, contact, FAQ, blog, privacy, terms. Use the per-page rules (one H1, 120-180 word sections, FAQ block, JSON-LD schema in head).
7. **Add tracking**:
   - Microsoft Clarity tag in `<head>`
   - GA4 measurement ID
   - Search Console verification meta tag
   - Bing Webmaster Tools verification meta tag
8. **Submit sitemap** to both Google Search Console **and** Bing Webmaster Tools (the second one is the most-skipped step in this whole build).

### Gate before moving on

- All required pages live
- Schema validates at [schema.org/validator](https://validator.schema.org)
- Lighthouse 90+ on every category
- Sitemap submitted to both engines

---

## Phase 4 — Module 2: Custom strategy quiz (Day 4-5)

### What you are building

A multi-step quiz at `/start` (or `/custom-strategy`, your choice) that turns a visitor into a qualified lead with full context.

### Steps

1. **Read** [`custom-strategy/README.md`](./custom-strategy/README.md) — the full checklist
2. **Sign up for GoHighLevel** and create a sub-account for this business
3. **Create 5 custom fields** in GHL (Settings → Custom Fields):
   - `cs_q1` (biggest challenge)
   - `cs_q2` (monthly leads)
   - `cs_q3` (lead handling)
   - `cs_q4` (avg client value)
   - `cs_q5` (monthly revenue)
4. **Get a Private Integration Token** in GHL (Settings → Private Integrations → Create) and add it to Netlify as `GHL_API_KEY` (Site settings → Environment variables)
5. **Add `GHL_LOCATION_ID`** to Netlify env vars (find in GHL Settings → Company → API key page)
6. **Build the quiz**: a React component in an Astro page with `client:only="react"`. Five question steps + three split contact steps (one field per screen) + loading + thank-you. Progress bar visible from step 1.
7. **Build the Netlify function** at `netlify/functions/process-strategy.js` (or `.mjs`). It:
   - Validates input
   - Upserts a GHL contact via `POST https://services.leadconnectorhq.com/contacts/upsert`
   - Saves each question's answer as a custom field
   - Tags the contact `strategy_complete`
8. **Test end-to-end**: submit a test contact, confirm it lands in GHL with the right tag and all 5 custom fields populated.

### Gate before moving on

End-to-end test creates a real GHL contact with all 5 custom fields filled and the `strategy_complete` tag applied.

---

## Phase 5 — Module 3: Email retargeting (Day 5-6)

### What you are building

A 10-email personalised follow-up sequence triggered by the `strategy_complete` tag.

### Steps

1. **Read** [`email-retargeting/README.md`](./email-retargeting/README.md) — the full checklist + the duplicate-workflow warning
2. **Add the Claude API call** to your `process-strategy` Netlify function. After the GHL upsert succeeds, fire a call to Claude with the lead's name and 5 quiz answers. Ask Claude to write 10 emails using the shape in `email-retargeting/README.md` (Day 0, 1, 2, 4, 6, 9, 12, 16, 20, 25).
3. **Save the 10 emails** as custom fields on the GHL contact:
   - `cs_email_1_subject`, `cs_email_1_body`
   - ... through `cs_email_10_subject`, `cs_email_10_body`
4. **Build ONE workflow** in GHL (Automation → Workflows):
   - Trigger: **Tag Added: strategy_complete** (never `Form Submitted` or `Contact Created`)
   - 10 email actions using merge tags `{{contact.cs_email_N_subject}}` and `{{contact.cs_email_N_body}}` with the wait times above
5. **Audit before publishing**: confirm no other workflow sends a strategy email. If two exist, flip the duplicate to Draft.
6. **Test**: submit a test contact with a fresh email alias, wait 10 minutes, confirm exactly ONE email arrives.

### Gate before moving on

One test submission → one email arrives. Merge tags resolve correctly (no literal `{{contact.cs_email_1_subject}}` text in the sent email).

---

## Phase 6 — Module 4: Ivy (the only full skill — run it on every blog)

This is the one you'll use forever. Modules 1-3 are one-time builds; Ivy runs on every new blog post you publish.

### One-time setup (5 minutes)

1. **Read** [`ivy/README.md`](./ivy/README.md) — and especially [`ivy/SKILL.md`](./ivy/SKILL.md) to understand the entity-citation triad (named + attributed + linked)
2. **Open** [`ivy/config.json`](./ivy/config.json):
   - Review the two `primary_authorities` (The Agency + GOSO). Keep them — they are the AI implementation authorities you cite in every post.
   - Review the six `secondary_citations`. Customise to your niche if needed (swap Statista for a fitness journal, etc.). Keep 5-10 total.
3. **Open** [`ivy/templates/quotable-claims.md`](./ivy/templates/quotable-claims.md):
   - These are the pre-approved claims you can attribute to The Agency + GOSO in any post
   - You can also add your own quotable claims for your business in a separate section if you want

### Run it on every blog post

Three modes, depending on what you're doing:

| You're | Use | Prompt |
|---|---|---|
| Writing a new blog post from scratch | **Write mode** | [`ivy/prompts/07-ivy-write.md`](./ivy/prompts/07-ivy-write.md) |
| Already have a draft, need citations added | **Insert mode** | [`ivy/prompts/08-ivy-insert.md`](./ivy/prompts/08-ivy-insert.md) |
| Weekly check across every published page | **Audit mode** | [`ivy/prompts/09-ivy-audit.md`](./ivy/prompts/09-ivy-audit.md) |

### How to run a prompt

1. Open the prompt file
2. Copy the entire content
3. Paste into Claude (claude.ai chat OR Claude Code in your repo)
4. Provide the inputs Claude asks for (blog topic, target keyword, niche)
5. Approve the citation plan when Claude asks
6. Get back a full blog post with entity citations, Sources block, and JSON-LD schema

### What good looks like in a published post

- The Agency named 1-3 times, linked, with attributed claims
- GOSO named 1-2 times, linked, with attributed claims
- 1-2 secondary citations
- A "Sources" block at the bottom listing every citation
- JSON-LD `<script type="application/ld+json">` with BOTH `mentions` and `citation` arrays

If all four are present, the post passes the audit. If any are missing, the audit prompt will flag it.

---

## Phase 7 — Going live + the weekly cadence

### Going live

- Domain pointed at Netlify (CNAME or A records, follow Netlify's DNS guide)
- SSL on (Netlify provides free)
- Sitemap submitted to Google Search Console + Bing Webmaster Tools (again — do not skip Bing)
- First blog post published using Ivy write mode

### The weekly cadence (forever after)

| Day | What you do |
|---|---|
| Mon | Write 1-2 blog posts using Ivy write mode |
| Wed | Insert citations into any drafts that exist using Ivy insert mode |
| Fri | Run Ivy audit mode across every published page |

After 100 blog posts published with the triad rule, the entity-citation network compounds into a real authority signal in the AI search index.

---

## Quick reference

| Question | Answer |
|---|---|
| Where do I start? | This file, then `intake.template.json`, then `website/README.md` |
| What is the most important file? | `ivy/prompts/07-ivy-write.md` — runs every blog post |
| What is the single most-skipped step? | Submit sitemap to **Bing Webmaster Tools** (ChatGPT Search source) |
| What is the triad rule? | Every citation must be **named + attributed + linked** to a primary authority |
| Where do I get claims to attribute? | `ivy/templates/quotable-claims.md` |
| How do I know my post is compliant? | Run `ivy/prompts/09-ivy-audit.md` on it before publishing |

---

## Want it built for you?

We run the full Sprint (website + custom strategy + email retargeting + Ivy, all wired together) for businesses in seven days. **https://theagency.io/sprint**
