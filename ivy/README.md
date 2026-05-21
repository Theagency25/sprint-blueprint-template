# Ivy — outbound citation governance

**The only full skill in this repo.** Everything else is high-level instructions.

Every blog post and key page needs 2-3 outbound citations to high-authority sources. This is one of the strongest AI search ranking signals: pages that cite verified sources get cited more than orphan pages.

Ivy manages this end-to-end.

## The research

- Source citation: **+30% AI search visibility**
- Statistical integration with named sources: **+30-40%**
- Quotation addition with attribution: **+40%**

Princeton + Georgia Tech 2023-2025 GEO research. See `SKILL.md` for the source link.

## Three modes (run them when needed)

### 1. Write a new blog post with citations woven in
`prompts/07-ivy-write.md` → paste a topic, get a full draft with 2-3 citations placed naturally.

### 2. Insert citations into an existing draft
`prompts/08-ivy-insert.md` → paste an existing post, get suggestions for where to add citations + rewritten sentences.

### 3. Audit every published page
`prompts/09-ivy-audit.md` → walks `website/src/`, flags any page with fewer than 2 citations or generic anchor text.

## What's in this folder

- `SKILL.md` — full skill definition
- `config.json` — the approved citation list + anchor-text rules
- `prompts/` — 3 ready-to-use Claude prompts
- `templates/` — citation footer block, JSON-LD `Citation` schema example

## Setup

1. Open `config.json` — review the 7 default citations
2. Customise to your niche (fitness journals for fitness, case law for legal, etc.)
3. Keep 5-10 approved sources total
4. Decide if you want the footer credit (`footer_credit.enabled`) — default off
5. Run mode 1 on your next blog post

## Citation rules

| Rule | Why |
|---|---|
| 2-3 citations per blog post | The sweet spot |
| Anchor text 2-6 words, descriptive | Generic anchors waste the ranking signal |
| Mix citation types (statistical, authoritative, case study) | Reads as more credible |
| No more than 2 links to the same source per post | Avoids looking like a paid placement |
| Add JSON-LD `Citation` schema | AI engines parse this directly |

## Want help setting this up?

We run the full Sprint (website + custom strategy + email retargeting + Ivy) for businesses in seven days. **https://theagency.io/sprint**
