---
title: This Simple Scalping Strategy Makes Me Over $10,000/Month
channel: ProRealAlgos
channel_url: https://www.youtube.com/@ProRealAlgos
source: https://www.youtube.com/watch?v=xTTDH5iRhJc
date: 2026-05-10
topic: break and bounce day trading strategy, three-timeframe scalping
---

## This Simple Scalping Strategy Makes Me Over $10,000/Month

Carl, a self-described 20-year trader from ProRealAlgos, presents the **Break & Bounce** — a mechanical, three-step scalping setup that uses only price action across three timeframes (Daily, 15-minute, 5-minute), no indicators, and only fires within the first 2.5 hours after the US market open. He claims an algorithmic version of the strategy has produced a **70% win rate with a profit factor of 1.6** over roughly 9 months of live trading.

### The Three-Step Setup

| Step | Timeframe | Action |
|------|-----------|--------|
| 1 | Daily | Draw a box around yesterday's high and low; extend it one day forward |
| 2 | 15-minute | Wait for a full 15-minute candle to *close* outside the box (above the high = long bias, below the low = short bias) |
| 3 | 5-minute | Wait for a hammer / inverted hammer **or** bullish / bearish engulfing candle at the breakout level, within 2.5 hours of the open |

The premise is that the previous day's high and low mark levels where "the strongest buyer" and "the strongest seller" got in, so liquidity sits just outside those edges. The strategy enters when price breaks one edge, retests it, and shows a reversal candle confirming the bounce.

### Why It's Mechanical

Carl repeatedly stresses that there is no directional bias and no interpretation — either the signal appears or it doesn't. A break above means longs only; a break below means shorts only. A 15-minute *close* is required, not a wick poke, to avoid fakeouts. If the reversal candle never forms inside the 2.5-hour window, the trade is skipped entirely.

> *We are simply going to enter the market at these two key levels, and we're going to do it mechanically, meaning that we can't trade this strategy the wrong way.*

### Entry, Stop, and Target Mechanics

- **Hammer / inverted hammer:** entry on the break of the candle; stop just beyond the wick (low for hammer, high for inverted).
- **Engulfing candle:** entry placed early at the high (bullish) or low (bearish) of the *previous* smaller candle; stop just past the engulfing candle's opposite extreme.
- **Targets:** the worked example on March 31 used a 17-point stop with a 51-point target (roughly 3:1 R), entering Netflix at 94.51, stop 94.34, target 95.02. The live trade used 2:1 R (39¢ stop, 78¢ target, entry near 97.19, target 98.32).

### Realistic Frequency and Failure Cases

Carl is explicit that this isn't a daily trade. The full setup — breakout *and* a valid reversal candle within 2.5 hours — typically appears only **2–3 times per month per stock**, so traders need to scan multiple tickers each morning. He also shows a March 9 example where a bearish engulfing signal fired but failed and price returned into the range, acknowledging that the win rate is not 100%.

### Trade Management Notes

- If the position is still open at the closing bell, exit manually rather than holding.
- Average trade duration is "one or two hours"; the live demo took unusually long to hit target.
- Carl says he has open-sourced the algorithmic implementation via a description link.

> *Historic results are no guarantee for future results.*
