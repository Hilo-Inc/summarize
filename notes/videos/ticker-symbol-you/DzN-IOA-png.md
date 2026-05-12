---
title: "I Was Wrong. This Is a Historic Buying Opportunity."
channel: "Ticker Symbol: YOU"
channel_url: https://www.youtube.com/@TickerSymbolYOU
source: https://www.youtube.com/watch?v=DzN-IOA-png
videoId: DzN-IOA-png
date: 2026-05-12
topic: AI data center CPUs, AMD/Intel/ARM, Buffett cash position, SubQ
---

## I Was Wrong. This Is a Historic Buying Opportunity.

Alex argues the market's "extreme greed" reading is masking a quiet rotation: Berkshire is at record cash, and the next leg of AI spend is shifting from GPUs alone to the **CPUs** that orchestrate agentic workloads. He publicly walks back his earlier dismissal of AMD and Intel, then makes the case that **ARM's new in-house AGI CPU** is the most disruptive entrant of the three.

### The setup: greed on top, fear at the top

- CNN Fear & Greed Index has sat near **extreme greed for 3 weeks** — longest stretch this year.
- Big Tech announced **>$700B in AI infrastructure capex** for the year, up **77% YoY** despite supply chain stalls.
- Berkshire Hathaway is holding **~$400B cash (32% of portfolio)** — an all-time record, larger than its cash share before the dot-com bust, GFC, or pandemic.

> "Be fearful when others are greedy and greedy when others are fearful." — Warren Buffett

The thesis: when Buffett and other institutions redeploy that cash, the question is *where* it goes. Alex says: into the AI compute stack — specifically CPUs.

### The mistake: agentic AI needs ~3× more CPUs than he thought

Old assumption was that AI data centers run roughly **1 CPU per 8 GPUs**. Agentic workloads (tool calls, sub-agents, ballooning context) run on CPUs, not GPUs, and Jensen quoted **400,000 CPU cores per 12,000 GPUs at scale at GTC 2026** — sounds like 33:1.

When you do the rack math vs. chip math, the picture changes:

| Unit | Ratio (GPU : CPU) for 12,000 Reuben GPUs |
|---|---|
| Racks (Nvidia Vera) | **9 : 1** (167 GPU racks vs. 18 CPU racks) |
| Chips (Nvidia Vera) | **2.6 : 1** (12,000 GPUs vs. 4,600 CPUs) |

> Investors price racks, but chips are what actually get sold. Counting by chips, AI data centers need **~3× more CPUs than I had been telling people.** Apology in full — I should have covered AMD and Intel more aggressively.

### AMD: huge wins, huge dilution

- Q revenue **$10.3B (+38% YoY)**; data center **$5.8B (+57% YoY)**, mostly CPUs.
- **Meta committed to 6 GW** of AMD Instinct GPUs, including 1 GW of fully custom MI450s — roughly the size of all non-hyperscaler AI compute on Earth.
- Cost of the deal: AMD issued **Meta a warrant for ~10% of the company at $0.01/share**, vesting if AMD hits **$600** (~$1T cap). Stock already at **~$450** (75% of the way there).
- **OpenAI has the same warrant.** At $600, **20% dilution kicks in simultaneously**, dragging effective per-share value to ~$480 — only **$30 above today's price**.

> Lisa Su: data center CPU TAM will **nearly triple by 2030** (~35% CAGR, ~3× the S&P 500).

### Intel: the foundry finally has customers

For years Intel needed an anchor foundry customer. In April it landed **three back-to-back**:

1. **Terafab** — $25B Austin fab with **Tesla, SpaceX, xAI**, on Intel's most advanced node.
2. **Google** — multi-year deal for custom internal-cloud chips.
3. **Apple** (per Bloomberg) — early talks with Intel and Samsung for US manufacturing to de-risk TSMC/Taiwan exposure. Apple last used Intel silicon in Macs from 2006–2020.

- Q revenue **$13.6B (+7% YoY)**; EPS **$0.29 vs. $0.13** YoY.
- Stock jumped **+24% the next day** — best single day **since the dot-com era**.

> "Two years ago I called Intel a value trap. Today they're the only American-owned and -operated factory that can build some of the world's most advanced chips."

### ARM: the arms dealer picked a side

After 35 years of selling blueprints to everyone, ARM launched **its first own-branded chip — the AGI CPU**.

| Metric | Nvidia Vera CPU | ARM AGI CPU |
|---|---|---|
| Cores per chip | 88 | **136** |
| Chips per rack | 256 | 60 |
| Cores per rack | ~22,500 | ~8,200 |
| Chips needed for 12,000 Reuben GPUs | 4,600 | **3,000** |
| CPU : GPU chip ratio | 1 : 2.6 | **1 : 4** |

- ~**40% fewer CPUs** needed vs. Vera for the same workload.
- **~2× perf/watt** vs. Intel and AMD.
- ARM claims **~$10B in construction savings per GW** of compute.
- Applied to Meta's 6 GW build: **~$60B in savings** if Meta had used ARM instead of AMD — roughly the value of the warrant AMD handed Meta to win the deal. **Meta is ARM's flagship AGI CPU customer.**
- Demand **doubled in the first 6 weeks** of orders.
- ARM's CFO guides **>$1B AGI CPU revenue in year one** and **$15B annual chip revenue by 2031** (vs. <$5B total revenue today — a ~4× over five years).
- Data-center royalty revenue **>2× YoY** at **~95% gross margins**.
- Stock dropped 10% post-earnings on **supply constraints, not demand** — they can't build fast enough.

> "ARM didn't just enter the CPU battleground. They dropped a tactical nuke on it."

### Wildcard: SubQ 1M (unverified)

Miami startup **Sub Quadratic** announced **SubQ 1M preview**:

- Research version: **12M token context window** (~12× frontier).
- Shippable version: 1M tokens, but claimed **>300× cheaper to run** ("$2,500 of Claude work for the price of a coffee").
- **$29M seed at a $500M valuation.**
- **No peer-reviewed paper, no public model, no reproducible benchmarks** — treat with suspicion.

How to read it: if Anthropic, OpenAI, or Google publish responses on subquadratic attention, the claim is being taken seriously; if crickets, it's smoke. Either way, the **DeepSeek precedent** applies — when AI compute gets cheaper, demand expands rather than contracts (Jevons paradox), and **every CPU in the stack gets more valuable**, not less.

### Bottom line

- The greed reading is real but the smart-money setup looks like 2009 or 2020: institutions building cash, waiting to deploy.
- The under-covered trade is **AI-data-center CPUs**: AMD (with eyes open about the 20% Meta + OpenAI warrant dilution at $600), Intel (foundry finally has anchor customers), and especially **ARM** (perf/watt and chip-count math materially beat Vera; supply, not demand, is the bottleneck).

### Sponsor (clearly marked)

> Sponsored segment for **Delete Me** (data-broker removal service) — 20% off with code "symbol20" at joindeleteme.com. Not part of the investment thesis.
