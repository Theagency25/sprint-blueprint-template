In the Netlify function from step 03 (`process-strategy`), after the GHL contact is upserted, fire-and-forget a call to Claude with the lead's name and 5 quiz answers. Ask Claude to write 10 emails using this exact shape:

```
E1 · Day 0  - Welcome + personalised strategy summary
E2 · Day 1  - Address their biggest challenge from Q1
E3 · Day 2  - Show what a similar business achieved
E4 · Day 4  - Address their lead handling gap from Q3
E5 · Day 6  - Numbers, what their current revenue could be
E6 · Day 9  - Named case study
E7 · Day 12 - Soft pitch + book a call
E8 · Day 16 - Objection handling
E9 · Day 20 - Final value drop
E10 · Day 25 - Last chance / break-up
```

## Rules for every email

- Quote the lead back to themselves. Use real numbers from their answers, not placeholders.
- Subject line: between 2 and 6 words. Lowercase. Curiosity over salesiness.
- Body: 3 to 5 short paragraphs. Mobile-first. One idea per paragraph.
- One clear CTA per email. Same CTA across most of the sequence (book a call).
- Brand voice from `brain/output/BRAND.md`. British English. No em dashes. No "I hope this email finds you well".

## Save each email to GHL

Use the GHL contacts PUT endpoint with the `customFields` array. Save as:

- `cs_email_1_subject`, `cs_email_1_body`
- `cs_email_2_subject`, `cs_email_2_body`
- ...
- `cs_email_10_subject`, `cs_email_10_body`

## Build the GHL workflow

One workflow, trigger: `Tag Added: strategy_complete`.

Inside, 10 email actions using merge tags `{{contact.cs_email_N_subject}}` and `{{contact.cs_email_N_body}}` with the wait times above.

## CRITICAL: duplicate-workflow audit

Only one workflow may send these emails. Before publishing:

1. Open `Automation, then Workflows` in GHL
2. List every workflow that uses any of these triggers:
   - `Form Submitted`
   - `Contact Created`
   - `Tag Added: strategy_complete`
3. Confirm exactly ONE of them sends a strategy email
4. If two send strategy emails, flip the duplicate to Draft before publishing
5. Submit a test contact, wait 10 minutes, confirm exactly one email arrives

If you skip this audit, every lead receives two identical emails 2-10 minutes apart. Found this out the hard way.
