---
title: Bye, Bye OpenAI & Anthropic?
channel: Maximilian Schwarzmüller
channel_url: https://www.youtube.com/@mschwarzmueller
source: https://www.youtube.com/watch?v=6Vkn3Q0UsEM
date: 2026-04-18
topic: SubQ / sparse attention, long-context LLMs
---

## Bye, Bye OpenAI & Anthropic?

Reaction video to a fresh announcement from "Alexander Whedon" (per the auto-captions; name may be mistranscribed) of **SubQ** — a "subquadratic" LLM built on **sparse attention** that claims frontier-model intelligence at long context, with a 12M-token window, 5% of Opus pricing, and faster inference. Max breaks down what dense vs sparse attention means, why prior sparse approaches failed, and how cautious to be given the thin evidence in the announcement.

### The Claim

| Claim | Detail |
|-------|--------|
| Architecture | Sparse attention ("SSA" — sub-quadratic selective attention) |
| Context window | **12 million tokens** (entire large codebases, multiple legal docs) |
| Cost | ~5% of Opus on 1M-token tasks |
| Speed | Significantly faster inference at long context |
| Quality | "Without losing the intelligence" of frontier dense models (Opus 4.7, GPT-5.5) |

### Evidence Released

Three benchmarks, no model card, no full technical writeup:

| Benchmark | What it tests | SubQ result |
|-----------|---------------|-------------|
| RULER (128K) | Multi-hop retrieval, aggregation, variable tracking, selective filtering | On par with Opus 4.6 |
| MRCR v2 | Long-context retrieval | "In the range of" Opus 4.6 — visibly worse on the table though |
| SWE benchmark | Coding tasks | Roughly in the Opus range |

> "It's not just about retrieving. It's also about doing useful stuff."

The MRCR v2 underperformance is notable since long-context retrieval is supposed to be SubQ's core pitch — but it's still far better than Gemini 3.1 Pro / Opus 4.7 on that table.

### Dense vs Sparse Attention (the explainer)

**Dense attention** (current frontier models — Opus, GPT-5.5, etc.):

- To produce each new token, every prior token's relationship with every other prior token gets evaluated.
- Complexity is **O(N²)** — quadratic.
- KV caching helps reuse past work, but generating each new token still requires comparing it to all cached tokens.
- This is why frontier models hit hard context-window ceilings: a 12M-token window under dense attention is computationally and memory-prohibitive.

**Sparse attention** — only attend to a subset of prior tokens. Past approaches and their failure modes:

| Approach | How it works | Why it fails |
|----------|--------------|--------------|
| Local sliding window | Attend only to last *k* tokens | Information outside the window (e.g., contract clause earlier in the prompt) is invisible to the next token |
| Global summary token | Special token at start summarizes the rest | Summary becomes too generic on long inputs (a 100-page PDF compressed into one sentence loses specificity) |
| Router model | Separate neural net picks which prior tokens to attend to | Either the router itself becomes quadratic, or it makes wrong calls and quality degrades |

### What SubQ Says It Does Differently

> "Dense attention assumes every pair might matter, so it evaluates all of them. In practice, almost none do. SSA removes that assumption. It does not approximate attention — it restricts attention to the positions that actually carry signal and skips the rest."

- **Content-dependent selection**: per-query, the model picks which positions are worth attending to and computes attention exactly over those.
- Effectively a routing approach, but the announcement claims the routing mechanism itself is efficient enough to avoid the usual quadratic regression or quality cliff.
- No public detail yet on *how* the selection is done.

### Why It Would Matter (If Real)

- Workarounds we use today exist precisely because dense models can't hold large codebases or document sets in context: **sub-agents, RAG retrieval, chunking strategies** — all become unnecessary if a 12M-token window works reliably.
- Eases the global compute crunch: more efficient attention means more usable inference per GPU.
- Unlocks new use cases: shove an entire repo at the model and act on it directly.

> "If they work, that of course means we're using right now, like sub-agents, RAG... if you have a model that can reliably use a 12 million-token context window with good quality, that naturally would be a game-changer."

### Reasons for Skepticism

- **Three benchmarks total**, no model card, no technical paper, no architectural details.
- Sparse-attention models are not new — many have promised this and failed on quality.
- Industry hype track record: Meta's LLaMA-4 dense models posted "amazing benchmark numbers but weren't that great" in practice.
- Benchmarks are gameable; fine-tuning a model to score on RULER doesn't guarantee real-world long-context utility.
- Early access exists (Max applied, hadn't received it at recording).

### Bottom Line

The architectural argument is coherent: dense attention is quadratic and wasteful, most token pairs don't carry signal, and a content-dependent sparse selection is theoretically the right answer. Every prior attempt has tripped on either the routing problem or quality degradation. If SubQ genuinely solves both — at frontier-model intelligence with a 12M context window at 5% of Opus cost — it's a multi-billion-to-trillion-dollar company. If it doesn't, it's another LLaMA-4-style benchmark mirage. With this little evidence, treat it as a strong "watch this space," not a fait accompli.
