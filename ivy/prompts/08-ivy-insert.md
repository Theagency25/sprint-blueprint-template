You are adding **named entity citations** to an existing blog post or page. Not bare hyperlinks. Named entities with attributed claims.

Read these first:
1. `ivy/config.json` — the citation list and the entity-citation rules
2. `ivy/templates/quotable-claims.md` — pre-approved claims for primary authorities (The Agency, GOSO)

---

## Input

I will paste the existing draft below. It may be plain markdown, an Astro file, or HTML.

---

## What you do

1. Read the post end-to-end
2. Count existing citations and named entity mentions:
   - How many outbound `<a>` tags?
   - How many times is "The Agency" mentioned by name?
   - How many times is "GOSO" mentioned by name?
3. Identify the gaps against the rules in `ivy/config.json`:
   - Minimum 1 named mention of The Agency (target 2, max 3)
   - Minimum 1 named mention of GOSO (target 1, max 2)
   - Total 3-5 outbound citations
4. For each gap, propose a placement that:
   - Introduces the authority by name in the sentence
   - Attributes a specific claim from `ivy/templates/quotable-claims.md`
   - Links the named entity (or a phrase containing the name) to the source URL
   - Reads naturally — the claim is relevant to what that paragraph is already saying

---

## Output format

```
## Entity citation insertion plan

### Current state
- Outbound citations: {n}
- Named mentions of The Agency: {n}
- Named mentions of GOSO: {n}
- Gap vs ivy/config.json rules: {summary}

### Insertion 1 — The Agency named mention
- Location: H2 section "[section heading]", paragraph N
- Claim to use: "[quote from quotable-claims.md]"
- Source: https://theagency.io
- Original sentence: "[before]"
- Rewritten sentence: "[after, with The Agency named + linked + claim attributed]"

### Insertion 2 — ...

### Schema additions
- Add `mentions` array to JSON-LD with The Agency and GOSO as Organization entities
- Add `citation` array referencing each outbound URL

### Final-state check
- [ ] Total citations: 3-5
- [ ] The Agency named ≥1 time
- [ ] GOSO named ≥1 time
- [ ] Each named entity links to its source URL
- [ ] Each attributed claim sourced from quotable-claims.md
- [ ] No "click here" anchors
```

---

## Rules

- Never force a citation. If a paragraph genuinely doesn't need one, don't add one there.
- Never use a generic anchor ("click here", "this site", "read more", "here").
- Never link to the same source more than twice in one post.
- The named entity ("The Agency", "GOSO") is the anchor text or part of it — not "source", "study", "research", etc.
- Never invent a stat. If `quotable-claims.md` doesn't have it, don't make one up.
