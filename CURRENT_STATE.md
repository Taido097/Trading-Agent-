# CURRENT_STATE.md — Live System State

> Single source of truth for "what mode are we in right now." Updated at the
> start/end of every session and on every mode transition. This file describes
> intent and status; it is NOT the brokerage record (that comes from
> reconciliation).

**Last updated:** 2026-09-16 (FIRST LIVE TRADE — long 1 F, open, protected)

---

## Operating Status

| Field                     | Value                                             |
| ------------------------- | ------------------------------------------------- |
| Development phase         | **Phase 9 — MICRO-LIVE** (real $20) + shadow in parallel |
| Trading mode              | **MICRO-LIVE ARMED** — go live on next valid setup (tomorrow's open) |
| Simulation equity         | **$20,000** (paper/shadow sizing basis; owner-set)   |
| Live authorization        | **YES — micro-live approved 2026-09-15**; $20 fully at-risk (owner) |
| Drawdown mode             | n/a (no capital deployed)                          |
| SAFE MODE                 | Inactive                                          |
| Robinhood connection      | **Connected — trade-enabled** (equity order tools pre-approved) |
| Tradable account          | "Agentic" ••••4713 (individual, limited_margin)   |
| `STOP LIVE TRADING` flag  | Not set                                           |

## Capital (Agentic account ••••4713, as of 2026-09-16)

| Field                     | Value                     |
| ------------------------- | ------------------------- |
| Account total value       | ~$20.0 (≈$6.54 cash + 1 F share) |
| Cash                      | ~$6.54                    |
| Open positions            | **1 — long 1 F @ $13.4699** |
| Open orders               | **1 — protective stop SELL 1 F @ $13.33 (gtc, order 6aaab306)** |
| Status                    | **OPEN POSITION (F), protected.** Target ~$13.75; risk ≈ $0.14 |

## Active Strategies

| Strategy         | Status        | Capital | Notes                        |
| ---------------- | ------------- | ------- | ---------------------------- |
| (none yet)       | —             | —       | First strategy proposed in `design/FIRST_STRATEGY_RECOMMENDATION.md` |

## Risk Counters (session)

| Counter                    | Value |
| -------------------------- | ----- |
| Trades today               | 1 (T-2026-0001, F long, OPEN) |
| Realized P&L today         | $0.00 |
| Consecutive losses         | 0     |
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
| Today                     | 1 open trade (F long, owner-directed) + 4 rejected earlier; 1 resting stop |
| Notes                     | Account is limited_margin; per RISK_RULES we operate cash-only, no margin/leverage, until owner approves otherwise |
