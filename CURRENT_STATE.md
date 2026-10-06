# CURRENT_STATE.md — Live System State

> Single source of truth for "what mode are we in right now." Updated at the
> start/end of every session and on every mode transition. This file describes
> intent and status; it is NOT the brokerage record (that comes from
> reconciliation).

**Last updated:** 2026-10-06 (Tue, intraday engine pass ~11:13am ET / 15:15Z — **REAL POSITION OPEN: LONG 1 NCLH**. REAL: TOOK T-2026-0008 — the 10:14 #1 watch resolved into the clean trigger I waited for. NCLH faded its open spike to 15.37, built a 45-min HIGHER-LOWS base, coiled 15.50-15.59, then broke to a new HOD 15.635 on expanding vol (161k) at 15:05Z. BOUGHT 1 @ 15.6274 (break-and-hold, not the 9:45 spike = O002/entry-location fix). STOP-FIRST broker-held GTC stop-market @ 15.43 (CONFIRMED; below 15.50 coil floor + 15.44 HL shelf, wider than immediate base per whipsaw lesson), risk $0.20/1.26%. Target 16.03 (2.04:1). Orders buy 6ac51085 / stop 6ac51092. Snapshot frozen. EOD flatten check scheduled 19:50Z (trig_01SqL6n3KsaG3uwsk8cmrqpP) — NEVER overnight. Regime RISK-ON new highs (SPY +0.79%, QQQ +0.86%); nuclear/uranium + cruise leading, metals red. CASH after buy ~$4.02; account value ~$19.65. PAPER: SMR P-0027 STOPPED -1.00R (low wicked exactly to 8.05 stop — honored; lesson: round-number stops get wicked on cheap high-beta names); UEC/OKLO/CCL still OPEN. Lifetime real (pre-NCLH): -$0.35 (2W/4L). Options/crypto/margin OFF.)

> _2026-10-05 EOD (prior):_ DAY DONE, FLAT, $19.65. GREEN day, index new highs (SPY 774.94 +0.69%) but strength in index/mega-caps; affordable universe choppy. REAL 0 trades (correct PASS — gappers faded: VALE +7.4% gap bled, HL/MARA -3%, SOFI base-break failed). PAPER: P-0025 SOFI -0.53R (entry-location test of base-break-at-HOD failed = confirms wait-for-pullback). Lessons: big pre-mkt gap in affordable name = FADE risk; buy the pullback not the breakout-at-HOD.

---

## Operating Status

| Field                     | Value                                             |
| ------------------------- | ------------------------------------------------- |
| Development phase         | **MICRO-LIVE (real $20) + HIGH-VOLUME PAPER** (owner: "trade as much as possible to learn") |
| Trading mode              | Real $20: **MICRO-LIVE, setup-gated**. Learning volume: **PAPER** (sim $20k, many trades/day, real data, zero risk) via hourly engine |
| Paper engine              | Hourly 14:00–20:00Z (10am–4pm ET, 7 passes) weekdays; now STEP A real-$20 setup check (every pass, all day) + STEP B high-volume paper; logs to data/PAPER_TRADES.csv (kept separate from live) |
| Paper results             | 24 closed: 9 wins / 15 losers (net ~−$51 sim lifetime after 9/29's −$34.60). 9/29: RIVN coil-after-breakout-HOLD −0.87R (MFE +0.46R, MAE −0.91R nearly held, EOD flatten). Better-behaved than the prior RIVN spike-chase (P-18, −1R, MFE ~0) — entry location helped — but STILL a loss because SPY was soft/red. REINFORCED LESSON: entry-location is the edge, but REGIME is the ceiling; a good coil entry still loses when the tape won't cooperate. Real-$20 regime gate keeps proving out (RIVN passed real, then lost in paper). |
| Sizing basis              | Real equity (~$19.90) per RISK_RULES §9; $20,000 is a mental reference only, never sizes a live order |
| Live authorization        | **YES** — micro-live approved; equity order tools pre-approved |
| Options / crypto / margin | **NOT enabled** — options only after separate testing + explicit owner approval (owner: "later we can trade options") |
| Drawdown mode             | n/a (no capital deployed)                          |
| SAFE MODE                 | Inactive                                          |
| Robinhood connection      | **Connected — trade-enabled** (equity order tools pre-approved) |
| Tradable account          | "Agentic" ••••4713 (individual, limited_margin)   |
| `STOP LIVE TRADING` flag  | Not set                                           |

## Capital (Agentic account ••••4713, as of 2026-09-30 EOD)

| Field                     | Value                     |
| ------------------------- | ------------------------- |
| Account total value       | $19.65 (all cash)         |
| Cash                      | $19.65                    |
| Open positions            | 0 (flat — VALE stopped out) |
| Open orders               | 0 (stop 6abd19c6 filled/consumed; no naked orders) |
| Status                    | **FLAT.** T-2026-0005 VALE stopped −$0.20 (−0.98R): breakout failed, MFE ~0 (bought breakout tick near HOD). Lifetime real P&L: F −0.11, AAL +0.05, CLF +0.05, VALE −0.20 = **−$0.21**. Real record: 2 wins (AAL/CLF coil+HOD-hold) / 2 losses (F no-edge, VALE breakout-chase). Lesson reinforced: reclaim/pullback entry > breakout-at-HOD, even on a green tape. |

## Active Strategies

| Strategy         | Status        | Capital | Notes                        |
| ---------------- | ------------- | ------- | ---------------------------- |
| (none yet)       | —             | —       | First strategy proposed in `design/FIRST_STRATEGY_RECOMMENDATION.md` |

## Risk Counters (session)

| Counter                    | Value |
| -------------------------- | ----- |
| Trades today (9/21)        | 1 REAL, closed — long 1 AAL @ 13.4699 → 13.5201 (T-2026-0003), +$0.05 (+0.33R), GOOD DECISION + WIN |
| Realized P&L today (9/21)  | +$0.05 (real); paper −2.8R sim (learning) |
| Consecutive losses         | 0 (AAL win broke the streak) |
| Daily loss used            | 0.00% |
| Weekly drawdown used        | 0.00% |

## Outstanding Owner Approvals Needed

- [ ] Approve final risk numbers in `RISK_RULES.md`
- [ ] Approve first strategy for backtesting
- [ ] Approve Robinhood connection method
- [ ] Approve progression from paper → micro-live

## Reconciliation

| Field                     | Value              |
| ------------------------- | ------------------ |
| Last reconciliation       | 2026-09-21 15:53 ET |
| Internal vs broker match? | **Yes** — flat, 0 positions, 0 open orders after AAL round-trip (buy 6ab176aa filled, stop 6ab176b9 cancelled, sell 6ab18b45 filled) |
| Discrepancies open        | 0                  |
| Today (9/21)              | 1 real trade closed (AAL +$0.05); GTC stop cancelled before the closing sell — no naked orders left |
| Notes                     | Account is limited_margin; per RISK_RULES we operate cash-only, no margin/leverage, until owner approves otherwise |
