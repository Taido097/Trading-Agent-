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

## 2026-09-17 (RE-CHECK, 10:06 ET) — PASS for the day, no trade
Flat ($19.90). Regime still risk-on (SPY +0.85%).
  - RIVN: pushed to 15.875 but NEVER broke OR high 15.93, reversed to ~15.5,
    volume dried up; now 15.74 — failed breakout. PASS.
  - F: false break — wicked to 13.83 (above OR high 13.80) but closed back below
    and faded to 13.745 on weak volume. PASS.
Decision: PASS for the day. Neither confirmed a hold above its OR high; both
  faded. Correct outcome — we watched, the breakouts failed, no chase. Logged to
  REJECTED_TRADES. Trades taken: 0 | Rejected today: 6 | Realized P&L: $0.00.
  Discipline note: this is the ORB filter working — most opening-range pushes
  fail, and not-trading the failures is where the edge is preserved.

## 2026-09-17 (AFTERNOON, ~3:06 ET) — paper batch closed; real PASS
Owner asked to "trade the $20" ~1:50pm; I lined up CLF (RS +7%, at highs). A ~70min
tool/MCP outage delayed execution; on fresh data CLF had FADED off its base
(13.10->12.955) and it was ~54min to close. No clean setup → **real PASS** (would be
a no-edge late entry). Real account still flat $19.90.
Paper (high-volume learning): first batch of 4 RS-momentum longs closed —
  CHPT +2R WIN (+$79.64 sim); CLF -0.27R, MARA -0.56R, RIVN -0.12R.
  Net +$41.82 sim (+1.05R), 25% win rate — one 2R winner carried it.
Note: too late in the day to open a fresh paper batch responsibly; next paper
  passes resume tomorrow via the hourly engine.

## 2026-09-18 (PRE-MARKET, 9:16 ET) — wide screen
Mode: MICRO-LIVE PRACTICE real $20 (setup-gated) + high-volume PAPER.
Reconciliation: Agentic ••••4713 — $19.90, 0 positions, 0 orders — matches OK.
Regime (pre-market): ~flat. SPY 760.46 (-0.03%), QQQ 718.17 (+0.17%). Muted vs
  yesterday's risk-on; lower odds of a clean breakout.
Wide screen (24 names, keep affordable <= ~$19 + liquid + tight spread, rank RS):
  - MARA ~$11.91 (+2.3%) tight spread — primary RS leader
  - RIG +0.9%, BTG +0.7% (both low-priced), RIVN +0.4%, SOFI +0.3%, AAL flat
  - Dropped >$19: KGC, HL(~19.2), RIOT, CCL, KEY, RF, SIRI, AMCR
  - Skipped: CLF/VALE/NCLH (red), CHPT (wide pre-market spread, thin)
Plan: at 9:47 measure opening ranges on the top names (MARA primary); take the
  first valid breakout clearing the gate, else PASS. Flat regime = be selective.
  No trade in this prep step.

## 2026-09-18 (DECISION, 9:48–9:51 ET) — valid ORB (MARA) but entry MISSED; PASS
Flat $19.90. Regime dead flat (SPY ~0.0%).
MARA: **first genuine ORB** — OR high 12.34; broke and held above (12.40) on heavy
  volume (1.78M opening bar); RS leader +6.5%. Cleared the gate.
Execution: placed BUY 1 @ limit 12.36; MARA dipped to 12.33 (retest) then ripped
  to 12.46->12.48 in ~90s — the limit did NOT fill. Cancelled it (confirmed
  cancelled, 0 shares). Chose NOT to chase at 12.48: entry +$0.12 higher pushes
  R:R below 2:1 and repeats the O001 anticipation/chase error. PASS, stayed flat.
Others (RIVN/SOFI/AAL/RIG): no valid breakout (RIVN red, others inside range).
Outcome: 0 trades, 1 missed-fill logged. Process was correct: identified +
  attempted the right setup at the right price; didn't chase when it ran.
Lesson (LESSONS candidate): on fast momentum names a passive limit at the level
  often misses; consider a marketable-limit slightly through the level to catch
  the break, OR accept the miss — but never chase after it extends.

## 2026-09-18 (EOD wrap, ~3:12 ET)
Real $20: 0 trades, flat $19.90. MARA ORB was valid but the entry missed (no
  chase); midday re-check found no clean entry. Correct, disciplined no-trade day.
Paper: 3 trades — MARA +2R, RIOT +2R, SOFI -1R = net +3R (+$119.90 sim). Book
  flat into the close; no late-day entries (little runway). 
Cumulative paper: n=7, 3 wins (all +2R) / 4 small losers, ~+$161.7 sim.
Takeaway: strongest-RS names (crypto-miners) worked; weakest (SOFI) failed —
  supports a "trade only the top RS names" filter as the sample grows.

## 2026-09-21 (PRE-MARKET, 9:16 ET) — wide screen
Reconciliation: Agentic ••••4713 — $19.90, 0 positions, 0 orders — matches OK.
Regime (pre-market): risk-ON gap up. SPY 766.36 (+0.61%), QQQ 727.98 (+0.9%).
  Supportive for long breakouts.
Wide screen (affordable <= ~$19, liquid, tight spread, rank RS):
  - MARA ~$13.84 (+4.5%) tight — primary RS leader (crypto, consistent winner)
  - NCLH ~$14.47 (+2.5%), SOFI ~$17.37 (+2.4%), CLF ~$12.80 (+2.4%), AAL ~$13.25 (+2.2%)
  - Dropped >$19: RIOT ($24.90, +4.8%). Skipped: CHPT (wide spread), SNAP/BTG/RIG (low-priced/weak)
Plan: at 9:47, measure opening ranges; take the FIRST valid breakout on the real
  $20, entering THROUGH the level (O002 fix) with a protective stop, >=2:1. Per
  owner, act on the first clean setup. Else PASS. No trade in this prep step.

## 2026-09-21 (DECISION, 9:48 ET) — PASS (gap-and-fade open)
Flat $19.90. Regime green (SPY +0.7%) but ALL watchlist names gapped up then
FADED in the first 15 min:
  - MARA OR 13.51-13.97, now 13.72 (bar-1 spike to 13.97 then faded) — no break
  - SOFI OR 17.081-17.52, now 17.02 — below OR low
  - NCLH OR 14.23-14.42, now 14.22 — below OR low
  - AAL OR 13.165-13.315, now 13.17 — at OR low
  - CLF now 12.37 (-1%) — red
Decision: PASS. No name broke ABOVE its OR high; all selling off from the open
  (index up, stocks fading = the inverse of a long breakout). Buying any = buying
  a fader. Consistent with owner's "take the good ones, pass the junk." Logged to
  REJECTED_TRADES. Real $20 stays flat. Paper engine covers learning volume later.

---

## 2026-09-22 — Pre-market prep (9:16 ET)

**Reconciliation:** Agentic ••••4713 FLAT — $19.95 cash, 0 positions, 0 open orders.
Matches internal state. Yesterday's AAL round-trip (T-2026-0003) fully settled: buy
6ab176aa filled, stop 6ab176b9 cancelled, sell 6ab18b45 filled. No naked orders.
Lifetime real P&L: −$0.11 (F) +$0.05 (AAL) = −$0.06.

**Regime (pre-market ~13:16Z):** SPY ~774.55 vs 773.50 prior = +0.14%; QQQ ~741.0 vs
741.47 = −0.06%. FLATTISH / mixed — clear step down from 9/21's strong risk-on
(SPY +1.6%). Implication: fewer clean trending setups likely; be MORE selective on
momentum entries today, especially after the open fades. Prefer names with genuine
stock-specific catalysts/RS over beta.

**Event risk:** No major scheduled macro print known for today (no FOMC/CPI/PPI/jobs
flagged). Caveat: not independently verified via a news feed this pass — the 9:47
decision routine should sanity-check headlines before any real entry.

**Wide screen — pre-market RS (last_non_reg vs 9/21 close), affordable ≤ ~$19:**
| Rank | Ticker | Pre-mkt | vs close | Note |
|------|--------|---------|----------|------|
| 1 | SOFI | 17.77 | +4.7% | strongest; liquid; fintech |
| 2 | NCLH | 14.71 | +3.3% | cruise; whipsawed in paper 9/21 (thin) |
| 3 | AAL  | 14.00 | +3.2% | yesterday's real winner, gapping up again |
| 4 | RIVN | 15.54 | +1.2% | EV; ranged all day 9/21 |
| 5 | F    | 13.30 | +1.0% | weak leader |
| — | CLF 12.16 (+0.7%), VALE 14.05 (−0.7%), MARA 13.16 (−0.9%), RIOT 23.86 (−1.3%, unaffordable) | | | miners cooling |

**Unaffordable (skip for real, paper OK):** CCL 23.02, RIOT 23.86, RF 28.5, SIRI 27.4, KEY 20.9.
**Too cheap for a whole-share stop (stop < spread):** GRAB 3.04, NIO 3.68, LCID 4.32, RIG 5.38.

**Top few for the 9:47 decision routine:** SOFI, NCLH, AAL — assess each on ACTUAL
opening-range data (break & hold above OR high on volume) before any real entry.
Pre-market gaps must confirm after the open; do not trade the gap itself. If the
flat tape produces no clean ORB that clears §9 + the gate, PASS — a zero-real-trade
day is fine. High-volume PAPER engine runs 7 passes 10am–4pm ET for learning volume.
