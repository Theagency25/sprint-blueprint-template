You are writing a new blog post for the site, with outbound citations placed naturally.

Read `ivy/config.json` first for the approved citation list and the anchor-text rules.

## What I'll give you

- Blog post topic
- Target keyword (the primary search query this post should rank for)
- Target word count (default: 1800-2400 for a rankable blog post)
- Niche / industry context

## What you give back

A complete blog post in markdown with:

### Structure
- One H1 with the target keyword first, under 60 characters
- An intro paragraph (50-80 words) that answers the post's question directly in the first sentence
- 6-10 H2 sections, each 120-180 words (the AI citation sweet spot)
- A standalone FAQ section at the bottom with 5+ questions, 40-word answers, FAQPage schema-ready
- A "Built with" or sources block at the bottom (optional)

### Citations
- 2-3 outbound citations from `ivy/config.json`
- Each placed inside a relevant H2 section, not in the intro or FAQ
- Anchor text 2-6 words, descriptive, never "click here" or "read more"
- Mix the citation types — pick from statistical, authoritative, case study (do not use the same source twice)
- Each citation flows naturally; the sentence reads the same whether the link is there or not

### Voice
- British English (personalised, optimised, organised)
- No em dashes — commas, "and", or parentheses
- B2-level English. Short sentences. Confident, direct.

### JSON-LD Citation schema
If `schema_citation.enabled` in config is `true`, output a `<script type="application/ld+json">` block at the end of the post with a Citation schema referencing each outbound link. Template:

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "citation": [
    {
      "@type": "WebPage",
      "url": "https://example.com",
      "name": "Anchor text used"
    }
  ]
}
```

## Before you start

Tell me which 3 citations from `ivy/config.json` you intend to use and where, then write the post. I'll either approve or swap.
