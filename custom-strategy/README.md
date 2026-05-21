# Custom strategy

A short interactive quiz on your site that turns a visitor into a qualified lead with full context.

This folder is **instructions, not a build kit**. It outlines what to build at a high level. The exact question design, function code, and CRM integration is the work we do with Sprint clients.

## What you are building

A multi-step quiz at `/custom-strategy` (or `/start`, whatever you prefer).

- Five short questions tuned to your niche — biggest challenge, current volume, what they have tried, value, revenue
- Three split contact steps (one field per screen): first name, then email, then phone
- A loading animation between submit and thank-you so the wait feels intentional
- A real thank-you screen with clear next-step expectations

## Why it's the primary CTA

Without these answers, every downstream email is generic. With them, your follow-up sequence can quote the prospect back to themselves in their own language. Generic sequences are dying. Personalised ones based on real answers convert.

## The non-negotiables

- Multi-step, never a single long form (each extra field on one screen drops conversion ~10%)
- Progress bar visible from step 1
- Mobile-first (most leads are on a phone)
- Every answer captured as a custom field on the contact record, not as a free-text note
- Each lead auto-tagged so the next workflow (the email sequence) fires cleanly
- A clean handoff to whatever email tool you use next (see [`../email-retargeting/`](../email-retargeting/))

## What to build it with

Whatever stack you already have. A React component inside a static page works well. The form's `onSubmit` should POST to a small serverless function that talks to your CRM.

## Want it built for you?

We design and build this quiz for every Sprint client. **https://theagency.io/sprint**
