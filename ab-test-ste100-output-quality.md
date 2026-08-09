# A/B test: "always use ASD-STE100" vs. output quality

Prompted by a viral tip: save a memory instruction telling Claude to always
write in ASD-STE100 (Simplified Technical English) to stop replies from
getting long-winded. This tests what else that instruction changes.

Full write-up with side-by-side responses and scoring:
**https://claude.ai/code/artifact/20e232f8-44c3-4bc9-80a9-33ab76cdd5e3**

## Method

ASD-STE100 is a controlled-language standard written for aircraft
maintenance manuals: short flat sentences, a restricted approved
vocabulary, active voice only, and — by design — no idiom, no ambiguity,
and minimal hedging.

Six prompts were each generated twice: once as Claude would normally
answer (**A**), once rewritten under strict ASD-STE100 rules (**B**).
Five prompts span open-ended, judgment-heavy asks (emotional support, a
humor request, an architecture recommendation, a contested-topic summary,
a debugging explanation). One is a genuine step-by-step procedure — the
register ASD-STE100 was actually built for — included as a control.

Scored 1–5 on five dimensions: accuracy/completeness, nuance/hedging
preserved, tone appropriateness, task success (did it do the actual job
asked), and practical usefulness. Same model rated both conditions in a
single pass — this is a fast qualitative probe, not a blinded or
statistically powered study.

## Results

| Dimension | A · Normal | B · STE100 | Δ |
|---|---:|---:|---:|
| Accuracy / completeness | 4.83 | 3.83 | −21% |
| Nuance / hedging preserved | 4.67 | 2.00 | −57% |
| Tone appropriateness | 4.50 | 2.17 | −52% |
| Task success | 5.00 | 3.00 | −40% |
| Practical usefulness | 4.83 | 3.00 | −38% |
| **Overall** | **4.77** | **2.80** | **−41%** |

## Findings

1. **Nuance and tone take the biggest hit.** Every hedge word the standard
   forbids ("might," "tends to," "arguably," "some critics say") is doing
   real work — signaling uncertainty or holding a contested claim as
   contested. Removing it changes what the sentence claims, not just its
   voice.
2. **The damage concentrates in exactly the tasks people use a chat
   assistant for.** Support, humor, judgment calls, and fair treatment of
   a contested topic are the bulk of conversational use — and the cases
   where the instruction actively works against the request. A Twitter
   bio asked to be funny fails outright: humor needs the ambiguity and
   exaggeration the standard explicitly bans.
3. **Code and hard facts survive; the framing around them doesn't.** A
   bug fix came out byte-for-byte identical across conditions. What
   eroded was the edge-case explanation — concrete example strings
   (`"(1,234.56)"`, `"12 items at 3.50"`) that make a failure mode
   recognizable disappeared in favor of abstract labels.
4. **On its actual home turf, it costs nothing.** For a linear,
   safety-relevant procedure (factory-resetting a router), ASD-STE100 is
   close to free — literally the register aircraft maintenance manuals
   were written in. The instruction isn't wrong in general; it's wrong
   applied globally instead of contextually.

## Bottom line

The tweet's stated problem — Claude's replies running long — is real, but
a blanket "always write in ASD-STE100" instruction is a blunt fix that
also strips hedging, warmth, humor, and the connective reasoning that
makes advice trustworthy rather than just terse. A narrower instruction
gets the length win without most of the quality loss, e.g. "default to
concise, plain sentences" without the controlled-vocabulary/no-hedging
rules, or scoping it explicitly to step-by-step instructions.
