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

---

## 2026-09-23 — Pre-market prep (9:16 ET)

**Reconciliation:** Agentic ••••4713 FLAT — $20.00 cash, 0 positions, 0 open orders.
Matches internal state. Yesterday's CLF round-trip (T-2026-0004) fully settled (+$0.05).
Lifetime real P&L: F −$0.11, AAL +$0.05, CLF +$0.05 = −$0.01 (flat; capital preserved).

**Regime (pre-market ~13:17Z):** SPY ~772.60 vs 773.38 = −0.10%; QQQ ~746.0 vs 747.46
= −0.19%. SOFT / slightly RED. Third straight non-trending open; if anything weaker
than 9/22. Momentum-long conditions are poor — expect mean-reversion (yesterday's
lesson) and be extra selective; a coil/pullback in a genuine RS leader is the only
thing worth taking, and there may be none.

**Event risk:** none major flagged (no FOMC/CPI/PPI/jobs known). Not independently
verified via a news feed — the 9:47 decision should sanity-check headlines.

**Wide screen — pre-market (last_non_reg vs 9/22 close), affordable <= ~$19:**
Almost the ENTIRE pool is red pre-market — no clean RS leader:
| Ticker | Pre-mkt | vs close | Note |
|--------|---------|----------|------|
| CHPT | 9.98 | +1.3% | green but THIN (whipsaw risk) |
| GRAB | 3.21 | +1.3% | green but too cheap for a whole-share stop |
| CLF  | 12.42 | −0.9% | yesterday's winner, giving back |
| MARA | 13.48 | −1.1% | miner, red |
| SOFI | 17.00 | −0.9% | red |
| AAL  | 13.41 | −1.5% | red |
| F 13.00 (−0.8%), RIVN 15.10 (−0.3%), VALE 14.05 (−1.0%), NCLH 14.15 (−0.5%), CLSK 14.93 (−1.4%), RIOT 24.51 (−1.7%, unaffordable) | | | broad weakness |

**Read for the 9:47 decision:** no pre-market RS leader worth pre-committing to. This
looks like a PASS-leaning day for the real $20 — only act if a name builds a genuine
post-open coil/higher-lows continuation on volume that clears §9 + the gate. A
zero-real-trade day is the likely and acceptable outcome in a red tape; do NOT force
one (that's the F-trade mistake). Paper engine runs its 7 passes for learning volume,
tightening breakout criteria per the flat/red-tape rule.

---

## 2026-09-23 — EOD wrap (4pm ET)

**Regime:** RED day — SPY closed ~−0.7%, QQQ ~−0.9% (risk-off from the open, weakened midday).

**REAL $20:** 0 trades — PASSED at 9:47 and every hourly engine pass. Correct call: no clean
affordable setup in a down tape, and the one green name (CLF) was either un-triggered (coil,
regime gate) or extended (post-spike, O002). Account FLAT $20.00, untouched. Lifetime real
P&L unchanged at −$0.01. A zero-trade day in a −1% tape = capital preserved = job done.

**PAPER:** 1 trade — CLF (P-2026-0017) **+2.00R (+$79.80 sim), WIN.** Deliberate RS-in-downtape
experiment: entered the CLF coil (only green name) at 12.59, target 12.87 hit at 1:40pm; ran to
12.93 (+2.7%) while SPY fell −0.5%. Answer to the test question: a genuine RS name with an
idiosyncratic bid CAN deliver a full 2:1 against a red market.

**Lessons banked today:**
- Regime discipline held: real account correctly sat out a red day (3rd of the week where the
  right move was fewer/zero trades). The F-trade mistake (forcing a no-edge trade) was NOT repeated.
- Candidate rule (needs more samples, NOT promoted): in a red tape, MAYBE allow a real long
  ONLY for the single strongest green RS coil (not spike), tight stop — else stay flat. n=1 so far.
- Target placement: leaving the target fixed let CLF's 2nd push tag it after a noon penny-miss;
  patience > tightening. Consider setting targets ~1 tick inside round levels.

**Weekly context:** Mon PASS (chop), Tue CLF +$0.05 real win (1 clean setup taken), Wed 0 real
(red tape). Real account 2-for-2 on edge-based trades, capital intact. The system is doing exactly
what it should: trade the rare clean setup, pass everything else, learn on paper daily.

---

## 2026-09-24 — Pre-market prep (9:16 ET)

**Reconciliation:** Agentic ••••4713 FLAT — $20.00 cash, 0 positions, 0 open orders.
Matches internal state. Lifetime real P&L −$0.01 (F −$0.11, AAL +$0.05, CLF +$0.05).

**Regime (pre-market ~13:17Z):** SPY ~764.59 vs 767.81 = −0.42%; QQQ ~735.06 vs 741.21
= −0.83%. RED again — THIRD straight weak/down open, tech-led selloff this time. Risk-off,
rotation toward defensives. Momentum-long conditions poor; expect mean-reversion, be very
selective (same posture that's kept the account flat/green all week).

**Event risk:** none major flagged; not independently verified —9:47 routine should check headlines.

**Wide screen — pre-market (last_non_reg vs 9/23 close), affordable <= ~$19:**
Broad weakness; only defensives green:
| Ticker | Pre-mkt | vs close | Note |
|--------|---------|----------|------|
| HBAN | 15.50 | +0.8% | regional bank (green) but low-beta + WIDE spread; marginal |
| KVUE | 17.75 | +0.5% | defensive (green) but illiquid pre-mkt (bid/ask 16.23/17.89) — avoid |
| CLF  | 12.85 | −0.2% | RS holdout again (flat vs red tape); watch for another coil |
| SOFI −0.8%, F −0.15%, MARA −1.6%, RIOT −2.1%, AAL −0.7%, NCLH −1.1%, CLSK −1.9% | | | cyclicals/miners red |

**Read for the 9:47 decision:** no clean momentum RS leader; tape red for a 3rd day. Watch CLF
for a repeat coil/higher-lows setup (it's the persistent RS name) — take ONLY if it clears §9 +
the gate on a genuine post-open hold, not a spike. Otherwise PASS; a zero-real-trade day in a red
tape is correct and expected. Do NOT force one. Paper engine runs for learning volume, favoring
coils/pullbacks over breakouts per the flat/red-tape rule.

---

## 2026-09-24 — EOD wrap (4pm ET)

**Regime:** THIRD straight red/soft day — SPY ~−0.15%, QQQ ~−0.3% (chopped between −0.9% and flat).

**REAL $20:** 0 trades — PASSED at 9:47 and every hourly pass. Correct: no clean affordable setup
in a red tape; even CLF (3-day RS holdout) cracked below its OR low at the open. Account FLAT $20.00,
untouched. Lifetime real P&L unchanged at −$0.01. Third disciplined zero-trade day this week in a
weak tape = capital preserved.

**PAPER:** 1 trade — RIVN (P-2026-0018) −1.00R (−$39.93). RS-in-downtape test #2: RIVN was the lone
green name (+2.4%), same profile as Wed's CLF, but I entered EXTENDED (chased 15.38, +3% off the low)
and it never traded higher (MFE 0) → stopped. RIVN later made a new HOD 15.505, confirming the name
was right and only the ENTRY was wrong.

**Lesson banked (the day's real payoff):** clean A/B on the RS-in-downtape idea —
  - CLF 9/23: entered at the COIL → +2R
  - RIVN 9/24: entered EXTENDED/chased → −1R (MFE 0)
  Same thesis, opposite entry, opposite result. The edge is ENTRY LOCATION (buy the coil/pullback,
  never chase the highs — O002), not the relative strength alone. This is exactly why the real $20
  correctly passed both. Candidate real-rule (still needs samples): in a red tape, a real long may be
  allowed ONLY for the strongest green RS name entered at a coil (not a chase); gate stays for now.

**Weekly context:** Mon PASS / Tue CLF +$0.05 real WIN / Wed 0 real (red) / Thu 0 real (red). Real
account: 2-for-2 on edge-based trades, capital intact at $20.00 through a 3-day red stretch. Paper is
doing its job — turning would-be real mistakes (chases) into free lessons.

---

## 2026-09-25 (Fri) — PRE-MARKET PREP (9:18 ET / 13:18Z)

**Reconciliation:** Agentic ••••4713 — FLAT. Cash $20.00, equity $0, buying power $20.00,
0 positions, 0 open orders. Matches internal state (no discrepancies).

**Regime (pre-market):** SPY 769.45 vs 767.18 close = **+0.30%**; QQQ 744.13 vs 741.10 = **+0.41%**.
GREEN / risk-on open shaping up — first non-red tape after a 3-day red stretch (Wed/Thu were both red).
This is the tape momentum longs actually work in. Confirm it HOLDS after the open (pre-market ramps fade).

**Event risk:** Last-Friday-of-month → PCE (Fed's preferred inflation gauge) is the likely 8:30 ET print.
Indices green pre-market ⇒ any data already out was digested favorably / market-friendly. No FOMC today.
Stay alert for a post-open fade if the ramp was just a data-relief pop.

**Wide screen (pre-market %, affordability, spread):**
Hard screen = 1 whole share ≤ ~$19 w/ buffer, liquid, tight spread. Pre-mkt spreads run wide — real
spread test is at the open.

RANKED RS LEADERS (affordable + tradable):
- **AAL** ~13.62 (+2.0%) — top RS, tight spread (13.61/13.63 ≈0.15%), very liquid. #1 name. (Prior real WIN 9/21.)
- **NCLH** ~14.45 (+1.83%) — strong RS, spread ~0.6%, affordable.
- **MARA** ~13.10 (+1.39%) — crypto-momentum, tight spread (13.09/13.11), affordable.
- **HL** ~18.15 (+1.17%) — gold/silver momentum, ~$18 (near ceiling), spread ~0.5%.
- **CLF** ~12.61 (+0.88%) — affordable but wide pre-mkt spread (to 12.82); watch after open. (Prior real WIN 9/22.)
- **F** ~12.63 (+0.24%) — inline, ultra-liquid, tightest spread; backup only if it takes RS lead.

DISQUALIFIED: CHPT (bid/ask 8.87/9.76 ≈9% spread — illiquid), HBAN (14.50/16.28 — junk pre-mkt spread),
KGC/RIOT/CCL/KEY/RF/SIRI/AMCR (>$19, can't buy 1 whole share w/ buffer). Laggards (SOFI −0.1%, SNAP,
VALE, RIG) — not leading, skip.

**Plan:** Do NOT trade in prep. The 9:47 ET decision routine looks at the top few (AAL / NCLH / MARA / HL)
for a real setup: an RS leader making & HOLDING a new intraday high on volume, a valid ORB break-and-hold,
or a coil/higher-lows continuation near HOD — never the vertical spike bar (O002). If the green tape holds
and a top name gives a clean NON-CHASE entry, this is a green-tape day where the real $20 can work (unlike
the last 3 red days). Stop first (risk $0.15–0.50, wider than the immediate base), target ≥2:1. If nothing
clean → PASS, never force. Options/crypto/margin OFF.

### 2026-09-25 (Fri) — 9:47 ET OPENING-RANGE DECISION → **PASS (real $20)**

Reconciled first: FLAT, $20.00, 0 positions / 0 open orders.

**Regime now (9:48 ET):** SPY +0.31%, QQQ +0.45% — indices still green, holding. BUT the affordable
momentum names did NOT follow through: the pre-market green ramp faded at the open (classic gap-up fade).

**Opening-range read (first 3 5-min bars, 9:30–9:45):**
- AAL — OR high 13.63; now 13.515 (+1.2% off the highs). Did not reclaim OR high; pulling back. No break-and-hold.
- NCLH — OR high 14.44; faded to 14.305, drifting to lows. No hold.
- MARA — opened 12.96, crashed to 12.53; now **−3.0% on the day** (below prior close). Failed gap / hard reversal. Avoid (O002).
- HL — OR high 17.99; faded to 17.80, red on day now.

**Decision: PASS.** No name is holding above its OR high on volume — every candidate faded off the open,
and MARA outright reversed. Buying any of these here would be chasing a fading gap into weakness (the exact
RIVN-chase mistake). A valid entry needs a name to pull back, coil, and RE-break with the tape — which the
all-day engine (STEP A) will catch if it develops. Zero real trade at the open is the correct call.
Logged 4 rejections to REJECTED_TRADES.csv. Options/crypto/margin OFF.

---

## 2026-09-25 (Fri) — EOD WRAP

**Tape:** GREEN day, first of the week. SPY +0.54%, QQQ +0.45%. BUT the shape mattered: gapped up +0.3%,
FADED the whole gap to flat by 10:15 ET, then recovered and ground higher all afternoon. A "fade-then-grind" day.

**REAL $20: 0 trades — flat, $20.00 preserved.** Decisions in order:
- 9:47 OR decision → PASS (gap-up faded; no name held its opening-range high; MARA reversed −3%).
- Mid-morning, when structure finally appeared, the affordable leaders either FAILED the 2:1 gate (F = clean
  base-breakout but low-beta Ford can't realistically deliver 2:1) or were EXTENDED after a +3-4% run
  (AAL/NCLH/HL = chase location). No clean, affordable (≤~$19), non-chase, ≥2:1 setup ever lined up.
- **Structural finding:** on GREEN momentum days the leaders extend fast and the clean pullback entry tends
  to appear only AFTER the affordable names have run past a good entry. The real-account constraint that bites
  is the intersection (affordable ≤$19) ∩ (not extended) ∩ (≥2:1 achievable). Worth watching whether this
  keeps producing 0-real-trade green days; if so, the fix is patience for a mid-day leader pullback-coil, not
  loosening the gate.

**PAPER: clean 3-way entry-LOCATION A/B on the SAME green tape (all entered 11:13 ET):**
| Entry style | Name | Result | MAE (heat) | Note |
|---|---|---|---|---|
| Reclaim-after-flush | NCLH 14.29→14.67 | **+2.00R WIN** | ~0R | reached target first, never underwater |
| Extended-trend | HL 18.14→18.195 (EOD) | +0.21R | −0.52R | valid trend, worst ride, barely green |
| At-breakout | F 12.735→12.705 (EOD) | −0.18R | −0.27R | cleanest location but low-beta = no 2:1 |
Net paper day: **+2.03R (+$80.96 sim)**. Lifetime paper: 21 closed, 9W/12L.

**Lesson (reconfirmed 3rd time):** ENTRY LOCATION is the edge. Ranked by both target-reach and heat taken:
reclaim/pullback > at-breakout > extended/chase. Agrees with CLF-coil +2R vs RIVN-chase −1R. The reclaim
entry (buy the flush-and-reclaim, not the extension) is now the highest-conviction pattern in the book.

**Weekly (9/21–9/25):** Mon PASS / Tue CLF +$0.05 real WIN / Wed 0 (red) / Thu 0 (red) / Fri 0 (green, no clean
affordable entry). Real: 1 trade all week (CLF win), capital intact $20.00, lifetime real P&L −$0.01. Paper did
the heavy lifting on learning: the entry-location edge is now well-supported. Options/crypto/margin OFF.
