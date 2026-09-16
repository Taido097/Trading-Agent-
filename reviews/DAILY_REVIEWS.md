# DAILY_REVIEWS.md — End-of-Day Process Log

> Runs after every session, whether or not trades were taken. Zero trades is a
> valid, reportable outcome.

Template:
```
## YYYY-MM-DD
Mode: <trading mode / drawdown mode / SAFE MODE?>
Market regime read:
Reconciliation: broker vs internal match? discrepancies?
Trades taken: <count>  |  Rejected: <count>
Realized P&L: $  |  R:
Rule violations: <none / list>
Errors observed:
Observations to log:
Risk status: daily loss used %, weekly DD used %, consecutive losses
Owner items:
```

---

## 2026-09-11
Mode: NOT TRADING (Phase 1 build)
Market regime read: not assessed (regime engine not built)
Reconciliation: n/a (not connected)
Trades taken: 0 | Rejected: 0
Realized P&L: $0.00 | R: 0
Rule violations: none
Errors observed: none
Observations to log: none
Risk status: no capital deployed
Owner items: review architecture; approve risk numbers & first strategy

## 2026-09-16 (PRE-MARKET, 9:16 ET)
Mode: MICRO-LIVE ARMED (real ~$20). Strategy: Opening-Range Breakout (long).
Reconciliation: Agentic ••••4713 — total $20.01, cash $20.01, buying power $20.01,
  0 positions, 0 open orders. Internal journals empty -> matches broker OK.
Regime (pre-market): SPY 759.88 (+0.33% vs 757.39), QQQ 708.25 (+0.53% vs 704.54)
  -> mild risk-ON / positive open bias. Supportive for a long breakout, pending
  confirmation at the open.
Event risk: TO VERIFY at decision time — mid-September can coincide with an FOMC
  meeting; if today/tomorrow is FOMC, reduce/avoid per RISK_RULES §6. No known
  earnings for the watchlist names in this window (confirm at 9:47).
Watchlist screen (need 1 share <= ~$19, liquid, tight spread):
  - F     ~$13.51  spread ~$0.04  OK primary
  - VALE  ~$14.47  spread ~$0.04  OK
  - RIVN  ~$15.62  spread ~$0.05  OK
  - SOFI  ~$17.15  spread ~$0.05  OK
  - NIO   ~$3.60   spread ~$0.01  marginal (too low-priced; stop below risk band)
  - GRAB  ~$2.94   spread ~$0.01  marginal (too low-priced)
  - INTC  ~$100.68 dropped (exceeds $20 buying power; 1 share unaffordable)
Plan: at 9:47 ET, measure each candidate's first-15-min opening range; take the
  first valid long breakout that clears the full pre-trade gate; else PASS. No
  trade taken in this prep step.
