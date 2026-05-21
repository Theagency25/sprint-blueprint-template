# custom-strategy — Skill definition

## Purpose

Capture every visitor as a CRM contact with five quiz answers attached as custom fields. This is the data the next skill (email retargeting) uses to personalise every email.

## When to use

- After the website is live
- When you add new niches or offers (the questions change per niche)

## Input

- `brain/output/BRAND.md`, `CUSTOMERS.md`, `PRODUCTS.md`
- GoHighLevel sub-account with 5 custom fields created
- This skill's `config.json` (GHL location ID, API key, custom field keys)

## Output

- React multi-step quiz at `/custom-strategy`
- Netlify function at `/.netlify/functions/process-strategy`
- GHL contacts with custom fields populated + `strategy_complete` tag

## Tools

- Claude Code
- GoHighLevel (CRM, sub-account)
- Netlify Functions

## The 5 questions (adapt per niche)

1. Biggest revenue challenge right now? (multiple choice)
2. Monthly leads count? (ranges)
3. Current lead handling system? (manual, partial CRM, full CRM, no system)
4. Average client value? (ranges)
5. Current monthly revenue? (ranges)

Then three split contact steps (one field per screen): first name → email → phone.

## Audit before complete

- [ ] 5 question steps + 3 contact steps + 1 loading + 1 thank-you
- [ ] Progress bar visible from step 1
- [ ] Mobile-first (most leads are mobile)
- [ ] Test submission lands as a real GHL contact with all 5 custom fields populated
- [ ] `strategy_complete` tag visible on the contact
- [ ] Thank-you page sets expectations for what happens next
