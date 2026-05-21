# Build order

The order to ship the four modules in. Each one feeds the next.

The detail of HOW to build each (prompts, code, integrations) is what we run for Sprint clients. The bar to clear for each module is below — clear it however you want.

---

## 1. Website

**Folder:** [`website/`](./website/)
**Job:** ship an AI-search-optimised site on auto-deploy from GitHub to Netlify
**Gate before moving on:**
- All required pages live (homepage, about, services, results, contact, FAQ, blog, privacy, terms)
- JSON-LD schema on every page (Organization, WebPage, FAQPage)
- `robots.txt` allowing 200+ AI crawlers (use [`website/templates/robots.txt`](./website/templates/robots.txt) as-is)
- `llms.txt` naming priority pages
- Sitemap submitted to **both** Google Search Console and Bing Webmaster Tools
- Microsoft Clarity, GA4, Search Console wired
- Lighthouse 90+ on every category

---

## 2. Custom strategy

**Folder:** [`custom-strategy/`](./custom-strategy/)
**Job:** lead-capture quiz that turns visitors into qualified contacts with full context
**Gate before moving on:**
- Multi-step quiz live at a clear URL (`/start`, `/custom-strategy`, etc.)
- Progress bar visible, one screen per question/contact field
- Each answer captured as a custom field on the contact record
- Lead auto-tagged so the next workflow (email sequence) fires cleanly
- End-to-end test with a real email creates a tagged contact

---

## 3. Email retargeting

**Folder:** [`email-retargeting/`](./email-retargeting/)
**Job:** personalised follow-up sequence using each lead's actual quiz answers
**Gate before moving on:**
- Sequence drafted with real numbers and quotes from the lead, not placeholders
- ONE workflow in the CRM sends these emails — not multiple
- Test submit, wait 10 minutes, exactly one email arrives
- Merge tags resolve correctly (no `{{contact.x_y_z}}` literal in the sent email)

---

## 4. Ivy — the only full skill in this repo

**Folder:** [`ivy/`](./ivy/)
**Job:** outbound citation governance — a major AI-search ranking signal
**Run it:**
1. Open [`ivy/config.json`](./ivy/config.json), review the default citation list, customise to your niche
2. On every new blog post, use one of the three prompts in [`ivy/prompts/`](./ivy/prompts/) (write / insert / audit)
3. Run the audit weekly to catch drift

Unlike the first three modules, Ivy ships as a working skill — config + 3 prompts + templates. Use it immediately.

---

## Want the whole thing built?

We run the full Sprint (all four modules wired together) in seven days. **https://theagency.io/sprint**
