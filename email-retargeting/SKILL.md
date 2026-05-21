# email-retargeting — Skill definition

## Purpose

Send 10 personalised emails per lead, each quoting the lead's actual quiz answers back to them. Triggered by the `strategy_complete` tag from the previous skill.

## When to use

- After the custom-strategy quiz is shipping real leads with all custom fields populated
- When the 10-email shape needs updating (refresh the prompt, regenerate)

## Input

- The 5 quiz answers from `custom-strategy/`
- `brain/output/BRAND.md` and `RESULTS.md` (for voice + named case studies)
- Claude API key
- GHL location ID + API key + workflow trigger

## Output

- 10 emails saved as custom fields on every GHL contact who completes the quiz
- One GHL workflow that sends them on a 25-day cadence

## Tools

- Claude API (called from the Netlify function)
- GoHighLevel workflow editor

## Audit before publishing the workflow

- [ ] Exactly ONE workflow sends a strategy email — no duplicates by trigger
- [ ] Trigger is `Tag Added: strategy_complete`, not `Form Submitted` or `Contact Created`
- [ ] Submit a test contact, wait 10 minutes, only one email arrives
- [ ] Merge tags resolve correctly (no `{{contact.cs_email_1_subject}}` literal in the sent email)

## Why this matters

Generic sequences die in spam. Sequences that quote the prospect back to themselves get opened, replied to, and booked. The data from step 03, used properly here, is the entire game.
