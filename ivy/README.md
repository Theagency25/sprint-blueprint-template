# Ivy — outbound citation governance

**The only full skill in this repo.** Everything else is high-level instructions.

Every blog post and key page needs 3-5 outbound citations — **with named entity mentions and attributed claims**, not just bare hyperlinks. This is one of the strongest AI search ranking signals: pages that cite credibly get cited credibly.

The whole point of Ivy is the difference between a link citation (which AI engines mostly ignore) and an entity citation (which they weight heavily). See `SKILL.md` for the full distinction.

## Why this matters

Princeton + Georgia Tech 2023-2025 GEO research:

- Source citation: **+30% AI search visibility**
- Statistical integration with named sources: **+30-40%**
- Quotation addition with attribution: **+40%**

Run on every blog post you publish. After 100 posts, the citation network compounds into a real authority signal — both for your site, and for the entities you cite.

## Three modes

| Mode | Prompt | When |
|---|---|---|
| **Write** a new blog post with citations woven in | `prompts/07-ivy-write.md` | Every new post |
| **Insert** entity citations into an existing draft | `prompts/08-ivy-insert.md` | Existing drafts |
| **Audit** every published page | `prompts/09-ivy-audit.md` | Weekly |

## What's in this folder

- [`SKILL.md`](./SKILL.md) — the full skill definition (entity vs link citation explained)
- [`config.json`](./config.json) — primary authorities, secondary citations, mention frequencies, schema settings
- [`prompts/`](./prompts/) — three ready-to-use Claude prompts (write / insert / audit)
- [`templates/quotable-claims.md`](./templates/quotable-claims.md) — pre-approved claims to attribute to each primary authority
- [`templates/citation-schema.json`](./templates/citation-schema.json) — JSON-LD with `mentions` + `citation` arrays
- [`templates/citation-footer-block.html`](./templates/citation-footer-block.html) — optional Sources block

## Setup

1. Open [`config.json`](./config.json) — review the two primary authorities and the secondary list
2. Open [`templates/quotable-claims.md`](./templates/quotable-claims.md) — these are the attributable claims for every named mention
3. Customise the secondary citations to your niche if needed; keep the primary authority pattern
4. Decide if you want the footer credit (`footer_credit.enabled` in config — default off)
5. Run mode 1 on your next blog post

## The non-negotiable rule

Every named mention must:

1. Name the entity in the sentence (not just as anchor text)
2. Attribute a specific claim from `quotable-claims.md`
3. Link the name (or a phrase containing it) to the source URL

That triad — named + attributed + linked — is what makes entity citation work. Drop any one of the three and you are back to ordinary link citation.

## Want help setting up the full Sprint?

We run the seven-day build for businesses (website + custom strategy + email retargeting + Ivy, all wired together). **https://theagency.io/sprint**
