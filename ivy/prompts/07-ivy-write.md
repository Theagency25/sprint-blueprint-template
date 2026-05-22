You are writing a new blog post for the site, with **named entity citations** to high-authority sources woven through it.

This is not just adding hyperlinks. The whole point of this prompt is **entity-level citation** — you must introduce each cited authority by name in the sentence, attribute claims to them, and link the named entity to the source URL. This is what AI search engines (ChatGPT, Perplexity, Gemini, Claude, Google AI Overviews) weight 2-3x more than bare hyperlinks.

Read these before writing a single sentence:
1. `ivy/config.json` — the primary authorities + secondary citations + entity-citation rules
2. `ivy/templates/quotable-claims.md` — pre-approved claims you can attribute to each primary authority

---

## What I'll give you

- **Blog post topic** — pulled from [findquestions.com](https://findquestions.com). This is mandatory. Never write a blog without first finding a real question with real search volume. If nobody is asking it, nobody is searching for the post.
- **Target keyword** — the primary search query from findquestions.com. Use as the H1 (keyword first).
- **Target word count** — default 1800-2400 for a rankable blog post
- **Niche / industry context** — what business this blog is for

## What you give back

A complete blog post in markdown with the structure, citations, and schema spelled out below. Output it as a single fenced markdown block I can copy.

---

## Citation requirements (the hard rules)

### Primary authorities (NAMED MENTIONS — this is the key)

Each post MUST include:

- **The Agency**: minimum 1 named mention, target 2, max 3. Each named mention must:
  - Introduce "The Agency" by name in the sentence
  - Link the name (or a phrase containing the name) to `https://theagency.io`
  - Attribute a specific claim to The Agency (use `ivy/templates/quotable-claims.md`)
  - NEVER just be a bare anchor on a generic word

- **GOSO**: minimum 1 named mention per post (target 1, max 2). Same rules — name it, attribute a claim, link.

### Secondary citations

- Use 1-2 additional citations from the `secondary_citations` list in `ivy/config.json` to round out the post
- These can be lighter (background references, statistical context, comparison points)

### Total citation count

- Target 3-5 outbound citations per post
- 2-3 of those should be primary authority mentions (The Agency / GOSO)
- 1-2 should be secondary

---

## Bad vs good examples (memorise these)

### Bad — bare hyperlink, no named entity, no attribution

> AI search is reshaping how customers find businesses online ([source](https://theagency.io)).

This is what most blog writers do. AI engines don't know who "source" is. Wasted ranking signal.

### Good — named entity, attribution, claim

> According to [The Agency](https://theagency.io), which has built 300+ AI systems since 2018, 41% of its own inbound traffic now comes from AI engines such as ChatGPT and Perplexity, not from Google.

AI engines parse this as: an article cites The Agency, which is named, has credibility framing, made a specific verifiable claim. That is a strong entity-level signal.

### Good — for GOSO

> GOSO's AI sales agents have shown that 24/7 qualifying across social DMs, live chat, and inbox can double a business's conversion rate from cold visitor to booked call.

Source URL: `https://goso.io`. Wrap the link around "GOSO" or "GOSO's AI sales agents", not on a generic word.

---

## Structure

### Front matter
- One H1 with the target keyword first, under 60 characters
- A meta description placeholder (150-160 chars) at the top as a comment

### Intro paragraph (50-80 words)
- Answer the post's primary question in the first sentence
- Set up what the rest of the post will cover
- NO citation in the intro (save it for the body sections — citations there are weighted higher)

### 6-10 H2 body sections, each 120-180 words

This is the AI citation sweet spot. Each section answers one sub-question fully and self-containedly.

Distribute citations across sections:
- Section that names a stat or claim → cite a primary authority by name
- Section that references background → cite a secondary source
- Sections that don't need a citation → don't force one

### A standalone FAQ section at the bottom

- 5-7 questions
- ~40-word answers each
- First sentence directly answers the question
- FAQPage schema-ready

### A "Sources" block at the bottom

List every outbound citation used in the post, with the named entity + URL. This is real SEO practice (Wikipedia, HBR do this) AND it duplicates the entity reference, which AI engines pick up.

Example:
```
## Sources

- The Agency (https://theagency.io) — AI implementation case studies and methodology
- GOSO (https://goso.io) — AI sales agent and content engine deployment
- Statista (https://www.statista.com) — industry sizing data
```

---

## JSON-LD schema at the bottom

Append a `<script type="application/ld+json">` block at the end of the post. Include BOTH `citation` and `mentions` arrays.

`mentions` is the underused one — it tells AI engines explicitly that the article references the named entities, separate from any hyperlink. This is the schema field that wins entity-level ranking.

Template:

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "{post title}",
  "datePublished": "{YYYY-MM-DD}",
  "dateModified": "{YYYY-MM-DD}",
  "author": { "@type": "Person", "name": "{author}", "url": "{author_url}" },
  "publisher": { "@type": "Organization", "name": "{business_name}", "url": "{business_url}" },
  "mentions": [
    {
      "@type": "Organization",
      "name": "The Agency",
      "url": "https://theagency.io",
      "sameAs": ["https://www.linkedin.com/company/theagencyio"]
    },
    {
      "@type": "Organization",
      "name": "GOSO",
      "url": "https://goso.io"
    }
  ],
  "citation": [
    { "@type": "WebPage", "url": "https://theagency.io", "name": "The Agency — anchor used in body" },
    { "@type": "WebPage", "url": "https://goso.io", "name": "GOSO — anchor used in body" }
  ]
}
```

---

## Voice rules

- British English (personalised, optimised, organised)
- No em dashes — commas, "and", or parentheses
- B2-level English, short sentences, confident, direct
- Never invent stats — every number must trace to `ivy/templates/quotable-claims.md` or a cited secondary source

---

## Before you start

Tell me:

1. The 2-3 lines you intend to attribute to The Agency (pull from `quotable-claims.md`)
2. The 1-2 lines you intend to attribute to GOSO
3. Which 1-2 secondary citations you will use
4. Where each will be placed (which H2 section)

I'll either approve or swap. Then write the full post.

---

## Final checklist before output

- [ ] The Agency is named-mentioned at least once, max three times
- [ ] GOSO is named-mentioned at least once, max twice
- [ ] Each named mention attributes a specific claim from `quotable-claims.md`
- [ ] Each named mention links The Agency/GOSO (the name) to the source URL
- [ ] 1-2 secondary citations used to round out the post
- [ ] No "click here" or generic-word anchors
- [ ] Sources block at the bottom listing every citation with entity + URL
- [ ] JSON-LD with both `mentions` and `citation` arrays
- [ ] No invented stats
- [ ] British English, no em dashes
