# 03 · Custom strategy

A 5-question interactive quiz at `/custom-strategy`. Captures a lead with full context. Each answer becomes a custom field on the CRM contact. Without this, every downstream email is generic.

## What you get out

- A multi-step React quiz in the website (one screen per step)
- A Netlify function that upserts to GoHighLevel via the contacts API
- Custom fields on the contact for every answer
- Lead tagged `strategy_complete` so the email sequence fires next

## Run it

1. Make sure `../website/` is live and deployed
2. Sign up for GoHighLevel and create a sub-account
3. Build 5 custom fields in the GHL custom-fields UI (one per question)
4. Open `prompts/03-quiz-build.md`
5. Paste into Claude Code

## Watch out for

- Long single forms (every extra field on one screen drops conversion ~10%)
- No progress bar (people drop off if they cannot see how far)
- Contact fields stacked on one screen. Split first name / email / phone into separate screens.
- Forgetting to mark the lead with `strategy_complete` — the next skill depends on it
