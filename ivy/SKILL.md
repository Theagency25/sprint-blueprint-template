# ivy — Skill definition

## Purpose

Manage outbound citations across the site. Every blog post and key page gets 2-3 citations to high-authority sources, which is a major AI-search ranking signal.

## When to use

- Every new blog post (suggest citation placements)
- Every key page (about, results, services)
- Weekly audit to catch published pages with missing citations

## Input

- `ivy/citations.json` (the approved citation list)
- The page or blog post being written

## Output

- Citation placements suggested for the current page
- Audit report listing any published page with fewer than 2 outbound citations

## Tools

- Claude Code
- A search of `website/src/` for `<a href="https://...">` patterns

## Citation rules

- 2-3 citations per blog post
- Anchor text descriptive, never "click here" or "this site"
- Context fits naturally — never forced
- Mix of citation types (statistical, authoritative, case study)

## Audit before publishing any blog

- [ ] At least 2 outbound citations to sources in `ivy/citations.json`
- [ ] Each citation has descriptive anchor text
- [ ] Each citation fits naturally in the surrounding sentence
- [ ] No more than 5 outbound citations per post (link dilution)
