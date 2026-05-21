# Email retargeting

A personalised email follow-up sequence that quotes the prospect's own answers back to them.

This folder is **instructions, not a build kit**. It explains the shape of the sequence and why it works. The actual generation logic, sequence timing, and CRM workflow integration is the work we do with Sprint clients.

## The shape

Roughly 10 emails over 3-4 weeks, each one referencing the prospect's specific answers from the quiz.

- Day 0: welcome + their personalised summary
- Early emails (day 1-6): address their stated challenges, show what similar businesses achieved, quote their numbers back to them
- Middle emails (day 9-16): soft pitch, case study, objection handling
- Late emails (day 20-25): final value drop, last chance

## Why it works

Generic email sequences are dying. "Hi [first name], hope this finds you well" gets archived in 2 seconds. Sequences that quote the prospect's own answers — their numbers, their language, their pain — get opened, replied to, and booked.

The data from your quiz is the entire game. Used properly here, it's the difference between a 1% reply rate and a 15% one.

## The non-negotiables

- Each email pulls real data from the quiz answers — not placeholders
- Subject lines are short (2-6 words), lowercase, curiosity over salesiness
- One CTA per email — the same CTA across most of the sequence
- Mobile-first body, short paragraphs, one idea each
- **Only ONE workflow may send these emails**. Audit your CRM workflows before publishing or leads will get duplicate emails 2-10 minutes apart.

## What to build it with

- A small AI call to draft the 10 emails per lead using the quiz answers as input
- Your CRM's workflow tool to schedule the sends with merge tags
- A single trigger (e.g. tag added) — not Form Submitted or Contact Created (those fire on too many other things)

## Want it built for you?

We build this for every Sprint client. **https://theagency.io/sprint**
