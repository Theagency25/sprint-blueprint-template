# 04 · Email retargeting

Ten emails per lead, each one written using the lead's actual quiz answers. Not "Hi {first_name}". Specifically: "Jim, you said you have $100K a year to spend and your biggest blocker is missed leads...".

## What you get out

- A function call to Claude that generates 10 personalised emails on quiz submit
- Each email saved as `cs_email_N_subject` / `cs_email_N_body` on the GHL contact
- One GHL workflow with 10 email actions using merge tags + the wait times below

## The 10-email shape

| # | Day | Purpose |
|---|---|---|
| E1 | 0 | Welcome + personalised strategy summary |
| E2 | 1 | Address their biggest challenge from Q1 |
| E3 | 2 | What a similar business achieved |
| E4 | 4 | Address their lead-handling gap from Q3 |
| E5 | 6 | Numbers, what their current revenue could be |
| E6 | 9 | Named case study |
| E7 | 12 | Soft pitch + book a call |
| E8 | 16 | Objection handling |
| E9 | 20 | Final value drop |
| E10 | 25 | Last chance / break-up |

## Run it

1. Make sure step 03 is shipping leads with all 5 custom fields populated
2. Add the Claude API call to the `process-strategy` Netlify function
3. Build one GHL workflow with trigger `Tag Added: strategy_complete`
4. Add 10 email actions, each using merge tags `{{contact.cs_email_N_subject}}` / `{{contact.cs_email_N_body}}`

## Watch out for

**Critical**: only one workflow may send these emails. If you also have a `Contact Created` or `Form Submitted` workflow that sends a strategy email, leads will get duplicates. Audit your GHL workflows before publishing.
