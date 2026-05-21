Build an AI agent across 4 channels using n8n with the Claude API.

Read `brain/output/BRAND.md`, `brain/output/FAQ_BANK.md`, `brain/output/PRODUCTS.md`, `brain/output/OPERATIONS.md`, and `agents/config.json` before building anything.

## Channels (one n8n workflow each)

- Instagram DM received (Meta Webhook)
- Facebook DM received (Meta Webhook)
- Website live chat message (your CRM's webhook)
- WhatsApp message (Twilio or Meta WhatsApp Business)

## Per channel, the workflow is

1. Fetch the conversation history from your CRM by contact phone or email (or create the contact if new)
2. Build the system prompt by reading `brain/output/BRAND.md`, `FAQ_BANK.md`, `PRODUCTS.md`
3. Send the latest message + history to the Claude API (model `claude-haiku-4-5` for speed, escalate to `claude-sonnet-4-6` for complex)
4. Save the response and post it back via the channel's API
5. Log the message + response on the CRM contact as a note

## The agent's job

- Qualify (ask 2 to 3 questions if it is not clear what they want)
- Answer common questions from `FAQ_BANK.md`
- Book calls (offer the calendar link from `OPERATIONS.md`)
- Push qualified leads to the strategy quiz (send `/custom-strategy` URL)

## The non-negotiable system-prompt opening

The system prompt MUST start with this block at the very top, before anything else:

```
<banned_formatting>
NEVER use em dashes (—) or en dashes (–). Use commas, "and", or two sentences.
NEVER use markdown (no **, no ##, no bullet points, no numbered lists).
NEVER use emojis.
NEVER say "sorry", "I apologise", or "apologies".
Max 140 characters per message. Max 2 sentences. Write like a real person texting.
</banned_formatting>
```

Without this, the agent uses markdown and emojis everywhere and sounds like a chatbot. With it, it sounds human.

## Test before going live

Send 8+ real-feeling test messages across edge cases:

- Vague question ("hey")
- Spam (irrelevant link)
- Refund request
- "Are you a bot?"
- Long detailed enquiry
- Confused (gibberish)
- Wrong language
- Multiple questions in one message

For each, confirm: no em dashes, no markdown, no emojis, no "sorry", under 140 chars, two sentences max. Qualified-lead messages must end with the strategy quiz URL.
