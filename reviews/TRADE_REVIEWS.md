# TRADE_REVIEWS.md — Per-Trade Post-Mortems

> **Every** trade is reviewed — wins, losses, and breakevens. Do not learn only
> from losers. Post-trade reasoning is kept separate from the frozen pre-trade
> snapshot to prevent hindsight bias.

Each trade is classified:
- **GOOD DECISION + WIN** — evidence the process may work (don't overweight one).
- **GOOD DECISION + LOSS** — normal trading loss; do not auto-change strategy.
- **BAD DECISION + WIN** — dangerous; log the luck, do NOT reinforce.
- **BAD DECISION + LOSS** — investigate what failed.

---

## Review Template

```
### Trade <ID> — <ticker> <date>
Snapshot ref (frozen, pre-outcome): design/TRADE_SCHEMA.md snapshot #<ID>
Result: <pnl, R>
Classification: GOOD/BAD DECISION + WIN/LOSS
Loss class (if loss): STRATEGY / EXECUTION / RISK / SYSTEM / BEHAVIORAL / REGIME

For losses — investigate (not "price went down"):
- What assumption was wrong?
- Was the setup valid? regime right? entry late? liquidity/spread OK?
- Was the stop appropriate? sizing correct? did news change?
- Normal variance or avoidable? rule violation? seen before?

For winners — do not assume good just because profitable:
- Setup valid? rules followed? risk appropriate?
- Did it work for the expected reason, or luck?
- Would repeating this behavior be rational?

Counterfactuals (no hindsight bias):
- What if no trade? entry at plan? stop unchanged? target taken? rejected?

Actions:
- Observation to log (memory/LESSONS.md)?
- Mistake to log (memory/MISTAKES.md)?
- Any change needs owner approval?
```

---

## Reviews

### Trade T-2026-0001 — F 2026-09-16  [OPEN — interim review]
Snapshot (frozen, pre-outcome): data/snapshots/T-2026-0001.json
Entry: 1 share @ $13.4699 (limit $13.50; favorable fill). Stop $13.33 (order
  6aaab306). Target ~$13.75. Planned risk ≈ $0.14 (~0.70% of the $20 account).
Result: CLOSED — exit $13.3622 (2026-09-16 15:32Z). P&L −$0.11 (~−0.77R).
  Closed manually (owner pivot to practice mode) before the $13.33 stop triggered.
Classification: **BAD DECISION + LOSS.** "Bad decision" refers to PROCESS, not
  the tiny loss: the entry had no edge (F flat on a green day, no ORB, taken on
  owner override). The loss is unsurprising — a no-edge entry has ~neutral
  expectancy minus spread/slippage. Per rule 20 this is expected variance, NOT
  evidence the strategy is broken; per rule 19 a win would not have validated it.
  Do not update strategy confidence from this trade.
What went right: risk stayed tiny and controlled (−$0.11 on a $20 account),
  invalidation defined first, protective stop attached immediately, full pipeline
  (reconcile→review→place→fill→stop→exit→journal) proven on real money.
Lesson (memory/LESSONS.md candidate): trading on command without a setup costs
  money even when small; the value here was pipeline validation, not P&L.
Process notes:
- Rule-2 tension acknowledged (traded without an edge) — justified only by
  explicit owner override on fully-at-risk micro capital; logged transparently.
- Risk control HELD: invalidation defined first, sized from risk, mandatory
  broker-held protective stop attached immediately after fill.
- Pipeline validated end-to-end: reconcile → review → place → fill → stop →
  journal. This is the real value of the trade.
Actions at exit: classify GOOD/BAD × WIN/LOSS, record slippage/MFE/MAE, update
  memory. No strategy change from this single owner-directed trade.

### PAPER batch 2026-09-17 (P-2026-0001..0004) — RS-momentum longs, sim $20k
First high-volume paper batch (4 RS-momentum longs opened 1:47pm ET, sim $40 risk each).
- CHPT: WIN, target hit +2.0R (+$79.64 sim) — clean momentum continuation to 10.08.
- CLF: LOSS -0.27R (-$10.65) — faded off its base.
- MARA: LOSS -0.56R (-$22.20) — rolled over midday.
- RIVN: LOSS -0.12R (-$4.97) — near-scratch.
Batch result: **+$41.82 sim (+1.05R), win rate 25%.** Classic momentum profile — one
2R winner outweighs several small losers. All GOOD-DECISION (valid RS entries); the
losses are normal variance, not process errors. Early sample (n=4) — no rule change;
keep accumulating. Observation to watch: entries taken after a name is already
extended intraday fade more (CLF/MARA were mid-afternoon, already up 6-7%).

### PAPER 2026-09-18 (P-2026-0005..0007) — RS-momentum longs, sim $20k
3 trades: MARA +2R (+$80, target 12.98), RIOT +2R (+$79.80, target 23.30),
SOFI -1R (-$39.90, stopped, never traded above entry). Net +$119.90 sim (+3R),
2 wins / 1 loss. Crypto-miners (MARA/RIOT) were the day's leaders and both hit
2:1; SOFI (bank/fintech, weaker RS) failed — consistent with "trade the
strongest RS names." Running paper sample n=7: 3 wins (all +2R) / 4 losers
(mostly small), net positive — the momentum profile (few 2R winners carry many
small losers) is showing. Still a small sample; no rule promoted yet.
Note: MARA's paper win is the same setup whose REAL entry missed this AM — the
read was right; execution (passive limit) was the gap (see O002).

### PAPER 2026-09-21 (P-2026-0008..0010) — RS-momentum longs, sim $20k
3 longs opened 11:14 ET (15:14Z) into a strong risk-on tape (SPY +1.1%, QQQ +2.1%).
Managed on the 12:12 ET intraday pass with fresh 5-min bars:
- **RIOT** (entry 25.01, stop 24.65): **STOPPED −1R (−$39.96).** Held for ~35 min,
  then rolled over on rising volume (15:50Z bar low 24.575), tagged the stop, kept
  fading to 24.43. Clean invalidation — the leader lost its bid and I was out at the
  planned level. No process error; the setup simply failed.
- **AAL** (entry 13.35, stop 13.28): **STOPPED −1R (−$39.97).** Never extended
  (MFE only +0.03), ground straight down to the 13.27 low at 15:50Z, then bounced
  back to 13.36 *right after* the stop. Textbook tight-stop whipsaw — the $0.07 stop
  gave the trade almost no room. Observation to watch: a stop this tight (~0.5% of
  price) on a $13 name sits inside normal noise; the entry needed either a wider stop
  (worse R) or a tighter entry trigger. Flagging as a candidate lesson, not yet a rule.
- **RIVN** (entry 15.47, stop 15.33, target 15.75): **still OPEN**, 15.535 (+0.46R
  unrealized). Only name that held its bid; ranged 15.42–15.58, neither stop nor
  target hit. Carrying into the next pass.

Batch so far: 2 stopped (−2R, −$79.93 sim), 1 open (green). All three were valid
RS-momentum entries; the two failures are normal variance in a choppy-underneath tape
(index green but individual names round-tripping their opens). Consistent with the
running read that only the *genuine* leaders that hold new highs pay — the two that
faded had already given back their opening pushes. Running paper sample now n=9 closed:
3 wins (all +2R) / 6 losers, net still positive on the momentum profile. No rule
promoted; sample still small.

### PAPER 2026-09-21 1:12 ET pass — 2 new longs (P-2026-0011..0012)
Tape strengthened into early afternoon (SPY +1.4%, QQQ +2.4%, semis-led). Scanned
the wider universe for RS leaders making/holding new intraday highs on volume:
- **PASSed AMD (+8.8%)** — day's biggest RS name but it already made its move
  (ripped to 616 by 11am) and has faded/chopped lower for 2 hrs. Entering now =
  chasing an extended, rolling name (O002). Discipline over FOMO.
- **PASSed SMCI (+5.5%)** — chopping mid-range below its 41.48 HOD; no fresh
  breakout to hold. No edge entering the middle of a range.
- **TOOK AAL (P-2026-0011)** — the clean one: after the AM tight-stop whipsaw
  (P-2026-0010) it *reclaimed* and built a higher-low staircase to a new HOD 13.44
  on rising volume. Re-entered at 13.42 with a **wider** stop (13.35, under the whole
  base) — deliberately applying the whipsaw lesson: don't put the stop inside the
  noise. Risk $0.07/sh, target 13.56 (2:1), 571 sh.
- **TOOK NCLH (P-2026-0012)** — clean higher-high staircase to HOD 14.59, holding
  near highs. Entry 14.55, stop 14.44 (under base), target 14.77 (2:1), 363 sh.
  Lighter volume than AAL — flagged.
RIVN (P-2026-0009) left OPEN — drifting sideways (15.46–15.58), no target/stop hit,
momentum cooling but thesis not invalidated. 3 paper positions now open (RIVN/AAL/NCLH).

### PAPER 2026-09-21 2:14 ET pass — NCLH stopped, HOOD breakout added
Manage:
- **AAL (P-2026-0011) WORKING** — after entry it dipped to 13.38 (held the wider
  13.35 stop — a dip that the *earlier* tight stop lesson explicitly anticipated),
  then pushed to 13.50. Green, MFE ~1.14R, target 13.56 not yet hit. Left OPEN.
  The wider-stop decision is being validated in real time.
- **NCLH (P-2026-0012) STOPPED −1R (−$39.93)** — faded immediately off entry, gave
  essentially zero upside (MFE ~0), pierced the 14.44 stop at 17:30Z, THEN bounced
  back to 14.48. The thinner-volume pick failed while the high-volume pick (AAL) is
  working — same pattern seen all week: **the genuine high-volume leader pays; the
  marginal/thin one whipsaws.** I flagged NCLH's lighter volume at entry; this
  reinforces adding a volume filter before promotion to a rule.
- **RIVN (P-2026-0009)** still OPEN, dead flat at entry (15.47); momentum gone but
  no stop/target hit.
New:
- **HOOD (P-2026-0013)** — the day's cleanest *fresh* setup: RS leader +4.3% that
  based 124–125 for 90 min then broke to a new HOD 125.26 on ~3x volume right at
  the pass. Deliberately contrasted with AMD (+8.8% but extended-from-open and
  fading — PASSed again) and SMCI (mid-range chop): only took the one that was
  actually breaking out *now* on volume. Entry 125.05 (through the HOD), stop 124.10
  (under base), target 126.95 (2:1), 42 sh. Note: late-day entry (~1h45 to close) —
  accepting less runway because the breakout quality is high; will see if late
  volume-breakouts behave differently from midday ones (data point for the journal).
Open now: RIVN, AAL, HOOD.
