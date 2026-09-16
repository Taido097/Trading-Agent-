# CURRENT_STATE.md — Live System State

> Single source of truth for "what mode are we in right now." Updated at the
> start/end of every session and on every mode transition. This file describes
> intent and status; it is NOT the brokerage record (that comes from
> reconciliation).

**Last updated:** 2026-09-16 (first live trade CLOSED −$0.11; back to PRACTICE)

---

## Operating Status

| Field                     | Value                                             |
| ------------------------- | ------------------------------------------------- |
| Development phase         | **MICRO-LIVE PRACTICE** on the real $20 (owner: "Practice on the $20") |
| Trading mode              | **MICRO-LIVE, setup-gated** — real trades, tiny size, learn from each; PASS when no valid setup |
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
| Trades today               | 1 closed (T-2026-0001, F long) + 4 rejected |
| Realized P&L today         | -$0.11 (~-0.77R) |
| Consecutive losses         | 1     |
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
| Today                     | 1 closed trade (F −$0.11) + 4 rejected; flat, no resting orders |
| Notes                     | Account is limited_margin; per RISK_RULES we operate cash-only, no margin/leverage, until owner approves otherwise |
