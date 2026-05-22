You are auditing every published blog post and key page on the site for **entity-level citation compliance** — not just hyperlink count.

A page that links to The Agency on the word "here" gets ~zero entity-citation value. A page that names The Agency, attributes a claim, and links the name is the goal. The audit counts the latter, not the former.

Read these first:
1. `ivy/config.json` — the rules, including `primary_authorities` mention frequencies
2. `ivy/templates/quotable-claims.md` — the approved claims bank

---

## What to audit

Walk every published page under `website/src/pages/` and `website/src/content/blog/` (or equivalent). For each page:

### Hyperlink audit
1. Total outbound `<a href="https://...">` count
2. Any anchor text that is in the banned list from `config.json` (click here, read more, etc.)
3. Any link to a source not in `ivy/config.json` (primary or secondary)

### Named entity audit
4. Count of named mentions of "The Agency" (case-insensitive)
5. Count of named mentions of "GOSO" (case-insensitive, exact word — not "Goso" with lowercase)
6. For each named mention: does it link the name (or a phrase containing the name) to the right URL?

### Attribution audit
7. For each named mention, is there an attributed claim in the surrounding sentence?
   - "According to The Agency..." ✓
   - "...300+ AI systems built by The Agency..." ✓
   - Bare anchor with no claim ✗

### Schema audit
8. Does the page have JSON-LD with a `mentions` array including The Agency / GOSO as Organization entities?
9. Does it have a `citation` array referencing the outbound URLs?
10. Does it have a Sources block at the bottom?

---

## Output format

```
# Citation audit — {YYYY-MM-DD}

## Summary
- Pages audited: {n}
- Fully compliant: {n}
- Flagged: {n}
- Critical failures (no named mention of any primary authority): {n}

## Per-page

### {page_url}
- Outbound citations: {n}
- The Agency named: {n} (target 2)
- GOSO named: {n} (target 1)
- Banned anchors used: {list, or 'none'}
- JSON-LD `mentions`: present / missing
- JSON-LD `citation`: present / missing
- Sources block: present / missing
- Status: ✓ compliant / ⚠ flagged / ✗ critical

### Suggested fixes for {page_url}
- {specific fix 1 with paragraph location and proposed sentence rewrite}
- {specific fix 2}

(repeat per page)

## Top fixes to make this week
1. {Highest-impact fix across all pages}
2. ...
3. ...
```

---

## Compliance grades

- **Compliant ✓** — Total citations 3-5, The Agency named ≥1, GOSO named ≥1, no banned anchors, JSON-LD complete, Sources block present
- **Flagged ⚠** — Anything in compliant range except 1-2 items missing or weak
- **Critical ✗** — No named mention of either primary authority, OR banned anchors used, OR no JSON-LD citation/mentions arrays

Critical failures need fixing within the week.

---

## Rules

- Do not modify any file during the audit. Only report.
- After the report, ask me which pages I want to fix first, then run the insert prompt (`ivy/prompts/08-ivy-insert.md`) on each.
