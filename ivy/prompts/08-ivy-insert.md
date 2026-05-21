You are adding outbound citations to an existing blog post or page.

Read `ivy/config.json` first for the approved citation list and the anchor-text rules.

## Input

I will paste the existing draft below. It may be plain markdown, an Astro file, or HTML.

## What you do

1. Read the post end-to-end
2. Count any existing outbound citations (`<a href="https://...">`)
3. Identify the 2-3 best places to add a citation from `ivy/config.json`. "Best" means:
   - The surrounding sentence makes a claim that the citation supports
   - The citation type matches the claim (statistical claim → statistical source, theory claim → authoritative source, case study claim → case study source)
   - The post does not already cite the same source elsewhere
4. For each placement, output:
   - Line number / paragraph location
   - The source URL from `ivy/config.json`
   - The exact anchor text to use (2-6 words, descriptive)
   - A rewritten version of the sentence with the citation embedded (preserve the original meaning, just add the link)
5. If the post already has 3+ citations and they all comply with `ivy/config.json` rules, say so and stop.

## Rules

- Never force a citation. If the post genuinely does not need one in a section, do not add one there.
- Never use "click here", "this site", "read more", or "here" as anchor text.
- Never link to the same source more than twice in one post.
- Mix citation types across the post (statistical, authoritative, case study).

## Output format

```
## Citation insertion plan

### Citation 1
- Location: paragraph 3, sentence 2
- Source: https://example.com
- Anchor: "industry overview"
- Rewritten sentence: "[full new sentence with the citation]"

### Citation 2
- ...

## After-insertion checks
- [ ] Total outbound citations: 3
- [ ] Mix of types: statistical (1) + authoritative (1) + case study (1)
- [ ] No source used more than twice
- [ ] No "click here" anchors
```
