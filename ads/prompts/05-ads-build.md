Build a Meta Ads lead-magnet campaign driving traffic to `/custom-strategy`.

Read `brain/output/CUSTOMERS.md` and `brain/output/BRAND.md` before writing a single line.

## Generate 10 visual variants

Static HTML files (1080×1080 and 1080×1350 each). Save under `ads/creatives/`. Each targets a different hook:

1. **Pain** — the cost of doing nothing
2. **Outcome** — the result they want
3. **Social proof** — a real testimonial from `brain/output/RESULTS.md`
4. **Contrast** — before / after
5. **Curiosity** — a question
6. **Authority** — founder credentials from `brain/output/ABOUT.md`
7. **Stat-led** — a specific number from `brain/output/LOCKED_TRUTHS.md`
8. **List** — "3 ways to fix X"
9. **Demo** — screenshot of the strategy quiz
10. **Free thing** — the lead magnet itself

## Generate 10 copy variants

Save as `ads/copy.md`. Each has primary text + headline (under 40 chars) + description (under 30 chars):

- **Direct** — "Get more leads in 30 days"
- **Problem-aware** — "If you are losing leads to slow follow-up..."
- **Solution-aware** — "Stop building DIY funnels..."
- **Curious** — "The 5 question quiz that..."
- **Specific** — "How [niche] businesses get to [outcome] in [timeframe]"
- **Authority** — "After [N] AI builds, here is what works in 2026"
- **Empathic** — "Running a [niche] business is harder than it should be"
- **Calculated** — "If your average client is worth £[X], every missed lead costs you £[Y]"
- **Bold** — "Most [niche] websites will be dead in 18 months"
- **Soft** — "A free [niche] strategy, no calls, no fluff"

## Launch settings (from `ads/config.json`)

- Campaign objective: Lead generation
- Daily budget: $30-$50 to start
- Audience: lookalike of existing customers OR narrow interest-based, never broad
- Optimisation: form completions on `/custom-strategy`
- Pixel: Meta Pixel on every page, GHL contact source field captures `utm_source`

## Kill / scale rules

- Kill any creative after 100 clicks if CPL is more than 2× your target
- Scale the winner only when CPL is under target for 7 consecutive days

British English. No em dashes.
