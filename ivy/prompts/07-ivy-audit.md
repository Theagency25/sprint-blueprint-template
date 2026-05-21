You are managing outbound citation governance for the website. Read `ivy/citations.json` and `ivy/config.json` first.

## Mode 1 — suggest placements for a new post

For the blog post / page I paste below:

1. Read the content
2. Identify 2-3 natural places where an outbound citation would strengthen the argument
3. For each, suggest:
   - Which citation source from `ivy/citations.json` fits
   - The exact anchor text (descriptive, not "click here")
   - Where to place it (paragraph reference)
4. Output as a markdown list with line numbers and rewrite suggestions

## Mode 2 — audit every published page

Walk `website/src/pages/` and `website/src/content/blog/`. For every published page:

1. Count outbound citations (any `<a href="https://...">` to an external domain)
2. Flag any page with fewer than `minimum_citations_per_post` from `ivy/config.json`
3. Flag any page with more than `maximum_citations_per_post` (link dilution)
4. Flag any page using "click here" or non-descriptive anchor text
5. Suggest what to add or fix

## Rules

- Two to three citations is the sweet spot for a blog post
- Mix the citation types from `ivy/citations.json` — never link to the same source three times in one post
- Anchor text should describe what the reader gets at the destination
- Never force a citation. If the content does not need one, do not add one.

## Output

Print a clear "Citation Audit Report" with:

- Pages compliant ✓
- Pages flagged ⚠ with specific fixes
- Suggested additions for any post still being drafted
