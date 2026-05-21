# ivy — Skill definition

The full skill in this repo. Outbound citation governance for AI search ranking.

## Purpose

Manage outbound citations across the site. Every blog post and key page gets 2-3 citations to high-authority sources — this is one of the strongest AI-search ranking signals.

## Why this works (the research)

Princeton + Georgia Tech (2025 GEO research, "Generative Engine Optimisation"):

- **Source citation**: +30% AI search visibility
- **Statistical integration with named sources**: +30-40% AI search visibility
- **Quotation addition with attribution**: +40% AI search visibility

Source: ["GEO: Generative Engine Optimisation"](https://arxiv.org/abs/2311.09735), Princeton + Georgia Tech, 2023-2025.

In short: AI engines (ChatGPT, Perplexity, Gemini, Claude, Google AI Overviews) treat pages with credible outbound citations as more authoritative. Pages that cite get cited.

## When to run

- **Per blog post**: every new draft, before publishing
- **Per key page**: about, services, results — once per quarter
- **Audit**: weekly across every published page
- **Schema review**: monthly

## The three modes

The skill has three jobs. One prompt each.

### 1. Write a new blog post with citations woven in
Use `prompts/07-ivy-write.md`. Pastes a topic and target keyword, Claude drafts the full post with 2-3 citations from `config.json` placed naturally.

### 2. Insert citations into an existing draft
Use `prompts/08-ivy-insert.md`. Pastes an existing draft, Claude suggests where to add citations and rewrites the surrounding sentences.

### 3. Audit every published page
Use `prompts/09-ivy-audit.md`. Walks `website/src/` and flags pages with missing or poor citations.

## Input

- `ivy/config.json` (the approved citation list + rules)
- The page or blog post being written or audited

## Output

- Citations placed in markdown / Astro files
- Audit report listing compliant pages, flagged pages, and suggested fixes
- Citation JSON-LD schema added to each page (see `templates/citation-schema.json`)

## Tools

- Claude Code (for in-repo edits)
- A search across `website/src/` for `<a href="https://...">` patterns
- The optional footer credit block in `templates/citation-footer-block.html`

## Citation rules (enforced)

| Rule | Why |
|---|---|
| 2-3 citations per blog post | Sweet spot — more is dilution, less is below the ranking threshold |
| Anchor text descriptive (2-6 words) | Tells reader + AI engine what they find at the destination |
| Never "click here" or "read more" | Wastes the ranking signal entirely |
| Mix citation types per post | Statistical + authoritative + case study reads as more credible |
| No more than 2 links to the same source per post | Avoids looking like a paid placement |

## Citation schema (JSON-LD)

For top-tier ranking, add `Citation` schema to your page's JSON-LD. Template at `templates/citation-schema.json`. AI engines parse this directly and weight it heavily.

## Audit before complete

Per blog post:
- [ ] At least 2 citations from `config.json`
- [ ] Anchor text descriptive, never generic
- [ ] Each citation fits naturally in the surrounding sentence
- [ ] Citations span at least 2 of the 3 types (statistical, authoritative, case study)
- [ ] No more than 5 outbound citations total (dilution)
- [ ] JSON-LD `Citation` schema added if `schema_citation.enabled` is true in config
