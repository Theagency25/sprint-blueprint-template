# /ivy

Outbound citation governance. Three modes.

## Mode 1 — Write a new blog post with citations woven in

Open `ivy/prompts/07-ivy-write.md`. Pastes the post topic and Claude drafts it with 2-3 citations from `ivy/config.json` placed naturally.

## Mode 2 — Insert citations into an existing draft

Open `ivy/prompts/08-ivy-insert.md`. Pastes an existing draft and Claude suggests where to add citations.

## Mode 3 — Audit every published page

Open `ivy/prompts/09-ivy-audit.md`. Walks `website/src/` and flags any page with fewer than 2 outbound citations or "click here" anchor text.

## Reference

- Skill: `ivy/SKILL.md`
- Config: `ivy/config.json` (the approved citation list)
- Templates: `ivy/templates/` (footer credit block, schema)

## Why this exists

Princeton + Georgia Tech 2025 GEO research:
- Source citation: +30% AI search visibility
- Statistical integration with named sources: +30-40%
- Quotation addition with attribution: +40%

This is one of the highest-ROI things you can do for AI-search ranking.
