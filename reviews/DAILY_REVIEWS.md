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

## 2026-09-16 (DECISION, 9:48 ET) — PASS, no trade
Mode: MICRO-LIVE ARMED. Reconciliation re-checked: $20.01, 0 positions/orders — OK.
Regime: SPY +0.31%, QQQ +0.67% (green). But ALL candidates red and below their
  opening-range highs — relative weakness, the inverse of a long-breakout setup.
Opening ranges (9:30–9:45 ET) vs price at 9:48:
  - F    OR 13.440–13.565  now 13.48  -> inside range, no breakout
  - VALE OR 14.420–14.480  now 14.44  -> inside range, tiny (~$0.06), no breakout
  - RIVN OR 15.180–15.729  now 15.33  -> breaking DOWN on rising volume (bearish)
  - SOFI OR 16.810–17.160  now 16.94  -> below OR high, choppy/red
Decision: **PASS on all four.** No valid Opening-Range Breakout long existed.
  Devil's advocate confirmed: buying a red, underperforming name with no upside
  break is chasing/hoping, not an edge. Authorized != obligated.
Trades taken: 0 | Rejected: 4 (logged to data/REJECTED_TRADES.csv)
Realized P&L: $0.00 | R: 0 | Rule violations: none | Errors: none
Risk status: daily loss 0%, weekly DD 0%, consecutive losses 0. Capital intact.
Note: never verified whether today is FOMC; moot since we PASSed regardless.

## 2026-09-17 (PRE-MARKET, 9:16 ET)
Mode: MICRO-LIVE PRACTICE on real $20, setup-gated (recurring routine).
Reconciliation: Agentic ••••4713 — $19.90 cash, 0 positions, 0 OPEN orders
  (yesterday's F buy+sell+cancelled-stop all closed). Matches internal -> OK.
Regime (pre-market): strong risk-ON gap up. SPY 763.6 (+1.3% vs 754.05 close),
  QQQ 716.5 (+1.7%). Supportive for a long breakout.
Event risk: TO VERIFY at decision — sharp gap suggests a catalyst; mid-Sept can
  be FOMC (decision ~2pm ET). ORB is a morning intraday trade so likely fine,
  but stay flat into any 2pm decision.
Watchlist (1 share <= ~$19, liquid, gapping with tape):
  - SOFI ~$17.28 (+2.6%) spread ~$0.04
  - RIVN ~$15.51 (+1.8%) spread ~$0.01
  - VALE ~$14.28 (+1.1%) spread ~$0.02
  - AAL  ~$13.06 (+2.8%) spread ~$0.01  (recovered from yesterday's fade)
  - F    ~$13.59 (+1.8%) spread ~$0.10 wide pre-market (should tighten at open)
Plan: at 9:47 ET, measure each opening range; take the first valid long breakout
  clearing the full gate; else PASS. No trade in this prep step.

## 2026-09-17 (DECISION, 9:48 ET) — WATCH, no entry yet
Flat confirmed ($19.90). Regime risk-on (SPY +0.94%).
Opening ranges (9:30–9:45) vs price at 9:48:
  - RIVN OR 15.47–15.93, now 15.78 (+3.6%) — strongest, volume surging, but
    consolidating BELOW the OR high; breakout NOT confirmed.
  - F    OR 13.59–13.80, now 13.785 (+3.3%) — at OR high but volume declining
    (weak breakout quality).
  - AAL/VALE/SOFI — below OR high / inside range / red. No.
Decision: WATCH RIVN (primary) + F. No entry — neither has broken and HELD above
  its OR high. Entering now = anticipating the break (the O001 mistake). Will
  re-check ~10:05 ET: enter only on a confirmed hold above OR high on volume,
  else PASS for the day.
