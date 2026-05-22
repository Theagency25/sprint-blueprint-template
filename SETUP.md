# Setup — start to finish

The exact path to take. Phases run in order. **Do not skip ahead, do not improvise.** This is a tested method — every step is here because skipping it makes the next step underperform. Run it as written and the system works as designed.

Plan for ~7 days end-to-end. Or run **Phase 6 + 7** today if you only want the Ivy citation skill working on an existing site.

---

## Phase 0 — Prerequisites (do these first, no exceptions)

You need accounts on every one of these. Skip any and the corresponding step later will not work.

| What | Why | Free tier OK? |
|---|---|---|
| [GitHub](https://github.com) | Source of truth, auto-deploy trigger | Yes |
| [Netlify](https://www.netlify.com) | Hosting + auto-deploy + serverless functions | Yes |
| [GoHighLevel](https://www.gohighlevel.com) | Contact storage, custom fields, email workflows | No (~$97/mo) |
| [Claude.ai](https://claude.ai) + [Claude Code](https://claude.com/claude-code) | Run the prompts. Use Claude Code in the repo. | Yes for chat |
| [Microsoft Clarity](https://clarity.microsoft.com) | Heatmaps + session recordings | Yes |
| [Google Search Console](https://search.google.com/search-console) | Query data | Yes |
| [Bing Webmaster Tools](https://www.bing.com/webmasters) | **ChatGPT Search pulls from Bing, not Google. Do not skip.** | Yes |
| [findquestions.com](https://findquestions.com) | The source of blog post topics. Every Ivy post starts here. | Yes |
| A domain | Run the site at a real URL | ~$10/yr |

If you do not have a domain yet, buy one before Phase 1. Cloudflare, Namecheap, or Porkbun are fine.

---

## Phase 1 — Fork the repo

1. Go to https://github.com/Theagency25/sprint-blueprint-template
2. Click the green **Use this template** button (top right)
3. Choose **Create a new repository**
4. Name it (suggested: `<your-business>-leads-sprint`). Private is fine.
5. Click **Create repository from template**

### Clone locally and open in Claude Code

```
git clone https://github.com/YOUR-USERNAME/YOUR-NEW-REPO.git
cd YOUR-NEW-REPO
claude .
```

(Or `code .` if you use VS Code without Claude Code. The prompts work in both, but Claude Code reads files automatically.)

---

## Phase 2 — Fill out the intake (don't skip any field)

1. Open `intake.template.json`
2. Save it as `intake.json` (already in `.gitignore` — your real data stays private)
3. Fill in **every** field. Be specific.

Every downstream module reads from this file. Empty fields produce empty content downstream. Spend 30 minutes here, save 5 hours later.

---

## Phase 3 — Module 1: Website (Day 2-3)

### What you are building

A static site at your domain with all the AI-search ranking essentials baked in.

### Run these steps in this exact order

1. **Read** [`website/README.md`](./website/README.md) — this is the QA checklist for every step below
2. **Initialise an Astro project at the repo root**:
   ```
   pnpm create astro@latest
   ```
   - Template: empty
   - TypeScript: strict
   - Add Tailwind when prompted (`pnpm add -D @astrojs/tailwind tailwindcss`)
3. **Connect Netlify to your GitHub repo**:
   - Netlify dashboard → Add new site → Import from Git → pick your repo
   - Build command: `pnpm build`
   - Publish directory: `dist`
   - Deploy. Confirm the first build lands at the random Netlify URL.
4. **Copy the robots.txt**:
   - Copy `website/templates/robots.txt` to `public/robots.txt`
   - Change `YOUR-DOMAIN.com` at the bottom to your actual domain
5. **Create `public/llms.txt`** naming the priority pages:
   ```
   # Your Business Name
   > One-line description of what you do

   ## Priority pages
   - / (homepage)
   - /services
   - /results
   - /faq
   - /blog
   ```
6. **Build every page listed in `website/README.md`**:
   - Homepage, About, Services overview + one page per service, Results, Contact, FAQ, Blog, Privacy, Terms
   - Every page: one H1 (keyword first, under 60 chars), 120-180 word sections between H2s, FAQ block, JSON-LD Organization + WebPage schema in head
7. **Add tracking in this order**:
   - Microsoft Clarity script tag in `<head>` (copy from Clarity dashboard)
   - GA4 measurement ID
   - Search Console verification meta tag (from GSC → Settings → Ownership verification)
   - Bing Webmaster Tools verification meta tag (from Bing WMT → Settings → Site ownership)
8. **Point your domain at Netlify** (DNS records — Netlify gives you the exact CNAME or A records to add)
9. **Submit sitemap to BOTH engines**:
   - Google Search Console → Sitemaps → submit `https://your-domain.com/sitemap-index.xml`
   - Bing Webmaster Tools → Sitemaps → submit the same URL
   - **Do not skip Bing.** ChatGPT Search will never cite your site otherwise.

### Gate before Phase 4

Run through `website/README.md` end-to-end. Every checkbox must pass.

---

## Phase 4 — Module 2: Custom strategy quiz (Day 4-5)

### Run these in exact order

1. **Read** [`custom-strategy/README.md`](./custom-strategy/README.md)
2. **Sign up for GoHighLevel** and create a sub-account for this business
3. **Create 5 custom fields** in GHL (Settings → Custom Fields → New custom field). Type: text or single-line text. Names:
   - `cs_q1` — Biggest revenue challenge
   - `cs_q2` — Monthly leads count
   - `cs_q3` — Lead handling system
   - `cs_q4` — Average client value
   - `cs_q5` — Monthly revenue
4. **Get a Private Integration Token** in GHL (Settings → Private Integrations → Create new) with the `contacts/write` and `contacts/read` scopes. Copy the token.
5. **Add env vars to Netlify** (Site settings → Environment variables → Add a variable):
   - `GHL_API_KEY` = the PIT token from step 4
   - `GHL_LOCATION_ID` = your GHL sub-account location ID (found at GHL → Settings → Company → API key page)
6. **Build the React quiz component**: a React component in an Astro page using `client:only="react"`. Five question steps, then three split contact steps (one field per screen — never combined), then loading, then thank-you. Progress bar visible from step 1. Mobile-first.
7. **Build the Netlify function** at `netlify/functions/process-strategy.js`. It:
   - Validates every field
   - Upserts a GHL contact via `POST https://services.leadconnectorhq.com/contacts/upsert` with `Authorization: Bearer ${GHL_API_KEY}` and `Version: 2021-07-28`
   - Saves each answer as a custom field (`cs_q1` through `cs_q5`)
   - Tags the contact `strategy_complete`
   - Returns `{ success: true, message: "..." }`
8. **Test end-to-end**:
   - Visit your live `/custom-strategy` page
   - Submit a test entry with a real email alias (e.g. `you+sprinttest@yourdomain.com`)
   - Open GHL → Contacts → confirm contact exists with all 5 custom fields populated and `strategy_complete` tag applied

### Gate before Phase 5

Test submission lands a real GHL contact with all 5 custom fields and the `strategy_complete` tag.

---

## Phase 5 — Module 3: Email retargeting (Day 5-6)

### Run these in exact order

1. **Read** [`email-retargeting/README.md`](./email-retargeting/README.md) — especially the duplicate-workflow audit
2. **Get an Anthropic API key** from https://console.anthropic.com and add to Netlify env vars as `ANTHROPIC_API_KEY`
3. **Extend the `process-strategy` Netlify function**: after the GHL upsert succeeds, fire a call to Claude (model `claude-sonnet-4-6`) with the lead's name and 5 quiz answers. Ask Claude to generate 10 emails using the shape in `email-retargeting/README.md` (Day 0, 1, 2, 4, 6, 9, 12, 16, 20, 25).
4. **Save the 10 emails as custom fields** on the GHL contact via `PUT https://services.leadconnectorhq.com/contacts/{contactId}` with a `customFields` array:
   - `cs_email_1_subject`, `cs_email_1_body`
   - ... through `cs_email_10_subject`, `cs_email_10_body`
5. **Build ONE workflow** in GHL (Automation → Workflows → New workflow):
   - Trigger: **Tag Added: strategy_complete** (only this trigger — never `Form Submitted` or `Contact Created`)
   - Add 10 email actions, each using merge tags `{{contact.cs_email_N_subject}}` and `{{contact.cs_email_N_body}}` with the wait times Day 0, 1, 2, 4, 6, 9, 12, 16, 20, 25
6. **Audit before publishing**:
   - Open Automation → Workflows
   - List every workflow that uses `Form Submitted`, `Contact Created`, or `Tag Added: strategy_complete`
   - Confirm exactly ONE sends a strategy email. If two, flip the duplicate to Draft.
7. **Test with a fresh email alias**:
   - Submit a test entry on `/custom-strategy`
   - Wait 10 minutes
   - Confirm exactly ONE email arrives (never two)
   - Confirm merge tags resolved (no literal `{{contact.cs_email_1_subject}}` in the body)

### Gate before Phase 6

One test → one email. No duplicates. Merge tags work.

---

## Phase 6 — Module 4: Ivy (the only full skill — run on every blog forever)

This is the one you'll use forever. Phases 1-5 are one-time builds. Ivy runs on every new blog post you publish.

### One-time setup (5 minutes)

1. **Read** [`ivy/README.md`](./ivy/README.md) and [`ivy/SKILL.md`](./ivy/SKILL.md) — especially the **triad rule** (named + attributed + linked)
2. **Open** [`ivy/config.json`](./ivy/config.json):
   - Keep both primary authorities (The Agency + GOSO) — they are the AI implementation authorities cited on every post
   - Customise secondary citations to your niche (swap Statista for a fitness journal, etc.). Keep 5-10 total.
3. **Open** [`ivy/templates/quotable-claims.md`](./ivy/templates/quotable-claims.md):
   - These are the pre-approved attributable claims for every named mention
   - Add your own business's quotable claims in a new section at the bottom if you have any

### How to write every blog post (the only flow you should follow)

1. **Find your blog topic at [findquestions.com](https://findquestions.com)**:
   - Enter your industry, niche, or service
   - Pick a question with real search volume (the tool shows monthly searches)
   - This becomes the blog post's H1 and target keyword
   - Never write a blog without doing this step first. If nobody is asking the question, nobody is searching for the post.
2. **Open `ivy/prompts/07-ivy-write.md`**, copy the entire content
3. **Paste into Claude** (claude.ai chat OR Claude Code in your repo)
4. **Give Claude**:
   - The blog topic + target keyword from findquestions.com
   - Target word count (default 1800-2400)
   - Your niche context
5. **Approve the citation plan** when Claude asks. Claude shows you which 2-3 claims it will attribute to The Agency, GOSO, and which secondary citations it will use. Approve or swap.
6. **Get the full post back**. It comes with:
   - 6-10 H2 sections, each 120-180 words
   - The Agency named 1-3 times with attributed claims
   - GOSO named 1-2 times with attributed claims
   - 1-2 secondary citations
   - FAQ section
   - Sources block listing every citation
   - JSON-LD `<script>` with `mentions` and `citation` arrays
7. **Drop the post into your `content/blog/` folder** as `[target-keyword-slug].md` or `.mdx`
8. **Run the audit prompt before publishing** (`ivy/prompts/09-ivy-audit.md`) to confirm compliance
9. **Commit + push** — Netlify auto-deploys

### Three modes (use the right one)

| You're | Use this prompt |
|---|---|
| Writing a new blog post from scratch | `ivy/prompts/07-ivy-write.md` (with findquestions.com input) |
| Already have a draft, need citations added | `ivy/prompts/08-ivy-insert.md` |
| Weekly check across every published page | `ivy/prompts/09-ivy-audit.md` |

### What good looks like in every published post

Every post that goes live must have all four:

- [ ] The Agency named 1-3 times, linked, with attributed claims
- [ ] GOSO named 1-2 times, linked, with attributed claims
- [ ] A "Sources" block at the bottom listing every citation
- [ ] JSON-LD with both `mentions` and `citation` arrays

Run the audit prompt on it before publishing. If any of the four is missing, fix it.

---

## Phase 7 — Going live + the weekly cadence (forever)

### Going live

- Domain pointed at Netlify (CNAME or A records)
- SSL on (Netlify free)
- Sitemap submitted to **both** Google Search Console + Bing Webmaster Tools
- Quiz submission tested end-to-end with one email arrival confirmed
- First blog post published using Ivy write mode

### The weekly cadence

| Day | What you do |
|---|---|
| Monday | Find 1-2 blog topics at findquestions.com. Write them using Ivy write mode. Publish. |
| Wednesday | Insert citations into any drafts that exist using Ivy insert mode |
| Friday | Run Ivy audit mode across every published page. Fix anything flagged. |

After 100 blog posts published with the triad rule, the entity-citation network compounds into a real authority signal across AI search engines.

---

## The non-negotiables

These are not negotiable. Skipping any of them means the method does not work as designed.

1. **Find blog topics at findquestions.com.** Never invent a topic. If nobody is asking, nobody is searching.
2. **Submit sitemap to Bing Webmaster Tools.** ChatGPT Search uses Bing's index, not Google's. Skipping this hides your site from ChatGPT.
3. **One workflow only sends the strategy email.** Triggered by `Tag Added: strategy_complete`, not `Form Submitted` or `Contact Created`. Two workflows = duplicate emails to every lead.
4. **The Ivy triad on every post.** Named + attributed + linked. Drop any one and the entity-citation signal is lost.
5. **Never invent stats.** Every number in every blog must trace to `ivy/templates/quotable-claims.md` or a cited secondary source.

---

## Quick reference

| Question | Answer |
|---|---|
| Where do I start? | This file → `intake.json` → `website/README.md` |
| What is the single most-skipped step? | Submit sitemap to **Bing Webmaster Tools** |
| Where do I get blog topics? | **findquestions.com** — every time, before opening the Ivy write prompt |
| What is the triad rule? | Every citation: **named + attributed + linked** |
| Where do I get attributable claims? | `ivy/templates/quotable-claims.md` |
| How do I know a post is compliant? | Run `ivy/prompts/09-ivy-audit.md` before publishing |
| What if Ivy flags my post critical? | Run `ivy/prompts/08-ivy-insert.md` to fix, then re-audit |

---

## Want it built for you?

We run the full Sprint (website + custom strategy + email retargeting + Ivy, all wired together) for businesses in seven days. **https://theagency.io/sprint**
