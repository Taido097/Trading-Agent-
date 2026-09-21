# CURRENT_STATE.md — Live System State

> Single source of truth for "what mode are we in right now." Updated at the
> start/end of every session and on every mode transition. This file describes
> intent and status; it is NOT the brokerage record (that comes from
> reconciliation).

**Last updated:** 2026-09-21 (15:14 ET — **REAL AAL open ~breakeven** (T-2026-0003), EOD close call pending ~3:52pm; paper book flattened EOD: +0.11R/+0.79R/−0.69R)

---

## Operating Status

| Field                     | Value                                             |
| ------------------------- | ------------------------------------------------- |
| Development phase         | **MICRO-LIVE (real $20) + HIGH-VOLUME PAPER** (owner: "trade as much as possible to learn") |
| Trading mode              | Real $20: **MICRO-LIVE, setup-gated**. Learning volume: **PAPER** (sim $20k, many trades/day, real data, zero risk) via hourly engine |
| Paper engine              | Hourly 15:00–19:00Z (11am–3pm ET) weekdays; manages open paper trades + opens new; logs to data/PAPER_TRADES.csv (kept separate from live) |
| Paper results             | 13 closed: 5 wins / 8 losers, net ~+$4 sim lifetime. 9/21 book flattened EOD: RIVN +0.11R, AAL +0.79R (4c shy of target), HOOD −0.69R (late-day breakout fizzled). Day −2.8R in a choppy-underneath tape. Lesson candidate O003: late-day breakouts lack follow-through. |
| Sizing basis              | Real equity (~$19.90) per RISK_RULES §9; $20,000 is a mental reference only, never sizes a live order |
| Live authorization        | **YES** — micro-live approved; equity order tools pre-approved |
| Options / crypto / margin | **NOT enabled** — options only after separate testing + explicit owner approval (owner: "later we can trade options") |
| Drawdown mode             | n/a (no capital deployed)                          |
| SAFE MODE                 | Inactive                                          |
| Robinhood connection      | **Connected — trade-enabled** (equity order tools pre-approved) |
| Tradable account          | "Agentic" ••••4713 (individual, limited_margin)   |
| `STOP LIVE TRADING` flag  | Not set                                           |

## Capital (Agentic account ••••4713, as of 2026-09-16)

| Field                     | Value                     |
| ------------------------- | ------------------------- |
| Account total value       | ~$19.90 (1 AAL share @ 13.47 + residual cash) |
| Cash                      | ~$6.43 after AAL buy (13.4699 fill)           |
| Open positions            | **1 — long 1 AAL @ 13.4699** (T-2026-0003)    |
| Open orders               | **1 — GTC stop-market sell 1 AAL @ 13.32** (id 6ab176b9) |
| Status                    | **LONG AAL.** First edge-based real trade. Stop 13.32 (risk $0.15), target 13.77 (2:1). Max loss if stopped ≈ $0.15. |

## Active Strategies

| Strategy         | Status        | Capital | Notes                        |
| ---------------- | ------------- | ------- | ---------------------------- |
| (none yet)       | —             | —       | First strategy proposed in `design/FIRST_STRATEGY_RECOMMENDATION.md` |

## Risk Counters (session)

| Counter                    | Value |
| -------------------------- | ----- |
| Trades today (9/21)        | 1 REAL taken — long 1 AAL @ 13.47 (T-2026-0003), OPEN with stop; edge-based breakout |
| Realized P&L today (9/21)  | $0.00 (AAL open) |
| Consecutive losses         | 1 (from 9/16 F trade; AAL is the next real trade, still open) |
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
| Last reconciliation       | 2026-09-16 09:48 ET |
| Internal vs broker match? | **Yes** — $20.01, 0 positions, 0 orders; no live trades |
| Discrepancies open        | 0                  |
| Today (9/17)              | 0 trades, 2 rejected (RIVN/F failed breakouts); flat, no orders |
| Notes                     | Account is limited_margin; per RISK_RULES we operate cash-only, no margin/leverage, until owner approves otherwise |
