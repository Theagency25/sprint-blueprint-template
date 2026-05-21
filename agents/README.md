# + · Agents

Plug an AI agent into your social DMs, live chat, and inbox. The agent qualifies, answers FAQs, and books calls 24/7, pushing every qualified lead into the same strategy quiz.

## What you get out

Four n8n workflows, one per channel:

- Instagram DM
- Facebook DM
- Website live chat
- WhatsApp

Each workflow fetches conversation history, calls Claude with a system prompt built from `brain/output/`, and posts the reply back via the channel API.

## Run it

1. Make sure the strategy quiz is live and capturing leads
2. Set up n8n (self-hosted or n8n.cloud)
3. Get API keys: Meta (IG + FB), Twilio (WhatsApp), Anthropic
4. Open `prompts/06-agents-build.md`
5. Build one workflow at a time, test before moving to the next

## Watch out for

- The system prompt MUST start with the `banned_formatting` block at the top, or the agent uses markdown and emojis everywhere and sounds like a chatbot.
- Test 8+ times before going live. Real conversations expose edge cases.
