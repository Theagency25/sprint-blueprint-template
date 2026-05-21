# + · Ivy — outbound citation governance

Every blog post and key page needs 2-3 outbound citations to high-authority sources. This is one of the strongest AI search ranking signals: pages that cite verified sources get cited more than orphan pages.

Ivy manages this — a curated list of outbound citations, where they fit in your content, and an audit that flags pages missing them.

## What it produces

- A `ivy/citations.json` of approved citation sources (with anchor text + context)
- Suggested citation placements for every new blog post you write
- A weekly audit listing any published page with fewer than 2 outbound citations

## Run it

1. Open `ivy/config.json` — review the default citation list, add your own, remove any that do not match your niche
2. Open `prompts/07-ivy-audit.md` and run on every new blog post
3. Run the audit weekly to catch any drift

## Why this matters

The Princeton/Georgia Tech 2025 GEO research found:

- Source citation: +30% AI visibility
- Statistical integration with named sources: +30-40% AI visibility
- Quotation addition with attribution: +40% AI visibility

Pages that cite credibly are cited credibly. The compounding starts there.

## Customise

Edit `ivy/citations.json` to match your niche. The defaults are general-purpose. For a fitness site, swap in fitness journals. For a legal site, swap in case-law references. Two to three citations per blog post is the sweet spot.
