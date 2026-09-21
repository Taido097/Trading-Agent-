# CURRENT_STATE.md — Live System State

> Single source of truth for "what mode are we in right now." Updated at the
> start/end of every session and on every mode transition. This file describes
> intent and status; it is NOT the brokerage record (that comes from
> reconciliation).

**Last updated:** 2026-09-21 (14:14 ET — NCLH stopped −1R; AAL working (green); RIVN flat; added HOOD breakout; real flat $19.90)

---

## Operating Status

| Field                     | Value                                             |
| ------------------------- | ------------------------------------------------- |
| Development phase         | **MICRO-LIVE (real $20) + HIGH-VOLUME PAPER** (owner: "trade as much as possible to learn") |
| Trading mode              | Real $20: **MICRO-LIVE, setup-gated**. Learning volume: **PAPER** (sim $20k, many trades/day, real data, zero risk) via hourly engine |
| Paper engine              | Hourly 15:00–19:00Z (11am–3pm ET) weekdays; manages open paper trades + opens new; logs to data/PAPER_TRADES.csv (kept separate from live) |
| Paper results             | 10 closed: 3 wins (all +2R) / 7 losers, net ~+$41.9 sim. 9/21 OPEN (3): RIVN 15.47 (flat), AAL 13.42 (green, MFE ~1.1R), HOOD 125.05 breakout (stop 124.10). Closed: NCLH −1R (thin-name whipsaw). Pattern: high-vol leaders pay, thin/marginal names whipsaw. |
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
| Account total value       | $19.90                    |
| Cash                      | $19.90                    |
| Open positions            | 0 (flat)                  |
| Open orders               | 0                         |
| Status                    | **FLAT.** First trade closed −$0.11. Practice mode; no live risk. |

## Active Strategies

| Strategy         | Status        | Capital | Notes                        |
| ---------------- | ------------- | ------- | ---------------------------- |
| (none yet)       | —             | —       | First strategy proposed in `design/FIRST_STRATEGY_RECOMMENDATION.md` |

## Risk Counters (session)

| Counter                    | Value |
| -------------------------- | ----- |
| Trades today (9/18)        | 0 taken; MARA valid ORB but limit missed the fill (no chase) |
| Realized P&L today (9/18)  | $0.00 |
| Consecutive losses         | 1 (from 9/16 F trade; no new real trades since) |
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
