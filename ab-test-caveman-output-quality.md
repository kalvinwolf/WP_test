# A/B test #2: Caveman brevity skill vs. output quality

Follow-up to `ab-test-ste100-output-quality.md`, testing
[juliusbrussee/caveman](https://github.com/juliusbrussee/caveman) — a
brevity skill built for AI coding agents — on the same 6 prompts.

Full write-up with side-by-side responses and scoring:
**https://claude.ai/code/artifact/fffcb725-654a-4461-9df9-6992e5af746a**

## What caveman actually does (from `skills/caveman/SKILL.md`)

- **Drops:** articles (a/an/the), filler (just/really/basically),
  pleasantries, hedging, causal arrows, invented abbreviations.
- **Keeps exact:** negation words (not/never/no/except), numbers, units,
  technical terms, code blocks, quoted errors.
- **Reverts to normal prose for:** security warnings, irreversible-action
  confirmations, multi-step sequences where compression risks misreading
  order.

Its own README claims (self-reported, not independently verified): 65%
token reduction on chat-style output, 8.5% on full agentic coding runs,
"100% accuracy retained."

## Results — three-way comparison

| Dimension | A · Normal | B · ASD-STE100 | C · Caveman |
|---|---:|---:|---:|
| Accuracy / completeness | 4.83 | 3.83 | 4.67 |
| Nuance / hedging preserved | 4.67 | 2.00 | 3.83 |
| Tone appropriateness | 4.50 | 2.17 | 4.00 |
| Task success | 5.00 | 3.00 | 4.83 |
| Practical usefulness | 4.83 | 3.00 | 4.67 |
| **Overall** | **4.77** | **2.80** | **4.40** |

Caveman loses ~8% overall vs. normal output. ASD-STE100 lost ~41%.

## Findings

1. **Caveman is a materially better-designed brevity approach.** It
   compresses filler, articles, and pleasantries instead of restricting
   vocabulary and grammar wholesale, so most content survives — including
   humor and structured reasoning that ASD-STE100 destroyed outright.
2. **Its one real weak spot is the same one ASD-STE100 had, just
   smaller.** Its rules explicitly list "hedging" as something to drop.
   On the one task that depends on hedged, both-sides framing (a "fairly
   represent the debate" summary), that costs real nuance — 3.6/5 average
   there vs. 4.8/5 normal, though still much better than ASD-STE100's
   2.2/5 on the same prompt.
3. **The built-in exceptions matter.** Reverting to normal prose for
   security warnings, irreversible actions, and order-sensitive
   sequences is exactly the scoping a blanket "always write like X"
   instruction lacks — compress by default, escalate when it's risky.
4. **Caution on the marketing numbers.** The 65% / 8.5% / "100% accuracy"
   figures are self-reported in the project's own README. This test used
   a different, more adversarial task set (emotional support, contested
   debates, humor) than typical coding-agent output, where compression is
   inherently riskier — so these results aren't a reproduction of those
   claims, just a stress test on harder terrain.
