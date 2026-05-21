Build a multi-step React quiz at `/custom-strategy` that captures a lead with 5 niche-specific questions plus name, email, phone.

Read `brain/output/BRAND.md`, `brain/output/CUSTOMERS.md`, `brain/output/PRODUCTS.md`, and `custom-strategy/config.json` before writing a single line.

## Tech

- React component in an Astro page (`client:only="react"`)
- 5 question steps + 3 contact steps + 1 loading step + 1 thank-you step
- Never a single long form. Every step is one decision.
- Progress bar at the top, 0 to 100% across the steps
- Brand colours from `brain/output/BRAND.md`
- DM Serif Display for headings, Inter for body (or whatever the brand uses)

## The 5 questions (adapt the options to the niche)

1. What is your biggest revenue challenge right now?
2. How many leads do you get per month? (ranges: 0-10, 11-50, 51-200, 200+)
3. How do you currently handle inbound leads? (manual, partial CRM, full CRM, no system)
4. What is the average value of a client to you? (ranges in the niche's currency)
5. What is your current monthly revenue? (ranges)

Then three split contact steps, one field per screen: first name → email → phone.

## On final submit

POST JSON to `/.netlify/functions/process-strategy`:

```json
{
  "formType": "custom_strategy",
  "firstName": "...",
  "email": "...",
  "phone": "...",
  "q1": "...", "q2": "...", "q3": "...", "q4": "...", "q5": "..."
}
```

## Build the Netlify function too

`/.netlify/functions/process-strategy` must:

1. Validate every field. Reject if missing or malformed.
2. Upsert a GoHighLevel contact via `POST https://services.leadconnectorhq.com/contacts/upsert`
   - Headers: `Authorization: Bearer ${GHL_API_KEY}`, `Version: 2021-07-28`
   - Body includes the contact + `customFields` array with keys from `custom-strategy/config.json`
3. Tag the contact `strategy_complete` so the email sequence in step 4 fires
4. Return `{ success: true, message: "..." }`

## Rules

- Use the brand voice from `brain/output/BRAND.md`
- British English. No em dashes.
- Mobile-first. Test on a real phone before declaring done.
- Show a loading animation between step 9 (submit) and the thank-you screen so the wait feels intentional.
