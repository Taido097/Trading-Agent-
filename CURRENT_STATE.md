# CURRENT_STATE.md — Live System State

> Single source of truth for "what mode are we in right now." Updated at the
> start/end of every session and on every mode transition. This file describes
> intent and status; it is NOT the brokerage record (that comes from
> reconciliation).

**Last updated:** 2026-09-28 (16:12 ET EOD — flat & done. RED risk-off day (SPY −0.75%, QQQ −1.07%). REAL: 0 trades, $20.00 preserved (red tape all day; only RS names >$19 unaffordable; MARA morning pop faded). PAPER: 2 RS-in-downtape coils (CCL, SIRI) BOTH stopped −1R = −2R. New lesson: RS-in-downtape needs a STABILIZING tape; in a DETERIORATING one even RS names get dragged down. Classifier had intermittent outages; prep pass skipped, all managed on later passes, nothing at risk.)

---

## Operating Status

| Field                     | Value                                             |
| ------------------------- | ------------------------------------------------- |
| Development phase         | **MICRO-LIVE (real $20) + HIGH-VOLUME PAPER** (owner: "trade as much as possible to learn") |
| Trading mode              | Real $20: **MICRO-LIVE, setup-gated**. Learning volume: **PAPER** (sim $20k, many trades/day, real data, zero risk) via hourly engine |
| Paper engine              | Hourly 14:00–20:00Z (10am–4pm ET, 7 passes) weekdays; now STEP A real-$20 setup check (every pass, all day) + STEP B high-volume paper; logs to data/PAPER_TRADES.csv (kept separate from live) |
| Paper results             | 23 closed: 9 wins / 14 losers (net ~−$16 sim lifetime after 9/28's −$79.92). 9/28 red-tape test: CCL & SIRI RS-in-downtape coils BOTH stopped −1R (both entered near breakout tick, MFE ~0). LESSON: RS-in-downtape longs need a STABILIZING backdrop (flat/basing SPY) — in a DETERIORATING red tape (−0.5%→−0.8%) even RS names get dragged down; the long-side edge disappears. Winners (CLF +2R, NCLH +2R) were all flat/recovering tapes. Regime gate for the real $20 fully vindicated: both "best" setups lost, real $20 untouched. |
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
| Account total value       | ~$20.00 (all cash)        |
| Cash                      | ~$20.00                   |
| Open positions            | 0 (flat)                  |
| Open orders               | 0 (both CLF stops cancelled cleanly) |
| Status                    | **FLAT.** T-2026-0004 CLF closed +$0.05 (+0.30R), 2nd edge-based real WIN. Lifetime real P&L: F −$0.11, AAL +$0.05, CLF +$0.05 = **−$0.01** (basically flat). 2 real wins in a row. |

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
