# brain — Skill definition

## Purpose

Build the foundational knowledge base for the business. Every other skill in this repo reads from these documents.

## When to use

- At the start of every new build, before touching the website
- Whenever the business positioning, products, or pricing changes
- After major customer research

## Input

- `intake.json` at the repo root
- A short founder interview (10-15 mins)
- The business's current website URL (asset scraping only, not copying copy)

## Output

12 markdown files in `brain/output/`:

| File | Purpose |
|---|---|
| BRAND.md | Voice, tone, words to use, words to avoid |
| LOCKED_TRUTHS.md | Verified stats only, every claim with a source |
| PRODUCTS.md | What is sold, pricing, tier breakdown |
| CUSTOMERS.md | Ideal customer, pain points, the language they use |
| COMPETITORS.md | Top 5 competitors, what they do well, gaps |
| KEYWORDS.md | 15-25 target search queries |
| FAQ_BANK.md | 20 real customer questions, 40-word answers |
| ABOUT.md | Founder story, real credentials |
| RESULTS.md | Real outcomes, testimonials with sources |
| GTM.md | Go-to-market: lead sources, sales process |
| OPERATIONS.md | Team, tools, workflows |
| ROADMAP.md | 30/60/90 day plan |

## Tools

- Claude (claude.ai or Claude Code)
- The founder for verification calls
- Public web for competitor research

## Audit before complete

- [ ] No invented stats. Every number traceable to a source.
- [ ] Brand voice matches how the founder actually speaks.
- [ ] FAQ answers are ~40 words each.
- [ ] Keywords are queries customers search for, not jargon.
- [ ] No `[VERIFY]` flags left unresolved.
