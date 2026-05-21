# agents — Skill definition

## Purpose

24/7 AI agent across social DMs, live chat, and inbox. Qualifies, answers, books calls, pushes qualified leads to the strategy quiz.

## When to use

- After the strategy quiz is live (the agent's main CTA is sending leads there)
- When social/DM volume is high enough that responses are slipping

## Input

- `brain/output/BRAND.md`, `FAQ_BANK.md`, `PRODUCTS.md`, `OPERATIONS.md`
- API access: Meta (IG + FB), Twilio (WhatsApp), Anthropic, GHL
- Calendar link (from `brain/output/OPERATIONS.md`)

## Output

- 4 n8n workflows, one per channel
- Every conversation logged as a note on the GHL contact

## Tools

- n8n (workflow orchestration)
- Claude API (claude-haiku-4-5 for speed, claude-sonnet-4-6 for complex replies)
- GHL contacts API (history + note logging)

## The non-negotiable

Every system prompt MUST start with this block at the very top:

```
<banned_formatting>
NEVER use em dashes (—) or en dashes (–). Use commas, "and", or two sentences.
NEVER use markdown (no **, no ##, no bullet points, no numbered lists).
NEVER use emojis.
NEVER say "sorry", "I apologise", or "apologies".
Max 140 characters per message. Max 2 sentences. Write like a real person texting.
</banned_formatting>
```

Without it, the agent uses markdown and emojis everywhere and sounds like a chatbot. With it, it sounds human.

## Audit before going live

- [ ] Banned formatting block at the top of the prompt
- [ ] 8+ test conversations with no em dashes, markdown, emojis, "sorry"
- [ ] Replies under 140 chars
- [ ] Qualified leads correctly routed to `/custom-strategy`
- [ ] Every conversation logged on the GHL contact as a note
