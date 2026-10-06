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

### Trade T-2026-0003 — AAL 2026-09-21  [OPEN — interim review]
Snapshot (frozen, pre-outcome): data/snapshots/T-2026-0003.json
**First edge-based REAL trade** (contrast T-2026-0001 F, which was a no-edge
owner-directed entry). Owner asked "still no trade today?" — and this time there
was an actual clean, affordable setup to say yes to, so I took it.
Entry: 1 share @ $13.4699 (limit 13.48, filled at ask). Stop $13.32 (broker-held
  GTC stop-market, id 6ab176b9). Target $13.77. Planned risk $0.15 (~0.75% of the
  ~$19.90 account), reward:risk 2:1.
Why this one cleared the bar (and days of others did not):
- **Relative strength:** +3.9% vs SPY +1.6% — a genuine leader, not a laggard.
- **Real breakout on volume:** based 13.39-13.44 midday, broke a new HOD 13.50 at
  18:00Z on a 1.74M-share 5min bar (2-3x the prior bars), then HELD the breakout
  instead of fading. This is the exact high-volume-leader profile the paper book
  has been rewarding all week (AAL/HOOD working; thin NCLH whipsawing).
- **Affordable + clean stop:** 1 share fits the $20; stop has a real technical
  home under the base.
Process notes:
- Edge defined BEFORE entry; invalidation set first; mandatory broker-held stop
  attached seconds after the fill; 2:1 respected. Options/crypto/margin OFF.
- Stop placed at 13.32 (wider than the immediate base) specifically to avoid
  repeating the P-2026-0010 tight-stop whipsaw — applying the week's own lesson to
  real money.
Honest caveats (logged, not hidden):
- Late-day entry (~2:26 PM ET) — the 2:1 target has limited runway before the
  close; may need to manage/close near EOD rather than let it sit. Data point on
  late vs midday breakouts.
- 1 whole share means the spread/fees are large relative to the edge; the value
  here is proving a real edge + full live pipeline on a defined setup, NOT P&L that
  can fund operations. $20 still cannot pay for itself; that math is unchanged.
Actions at exit: classify GOOD/BAD x WIN/LOSS, record slippage/MFE/MAE/return_r,
  update memory. This is a GOOD DECISION regardless of outcome (valid edge, correct
  process); a win won't validate the strategy on n=1 and a loss won't refute it.

### PAPER 2026-09-21 3:14 ET pass — EOD close of the book (P-2026-0009/0011/0013)
Last intraday pass of the day; flattened all open paper positions to EOD marks
(no new entries — 46 min to close is too little runway for a fresh momentum entry).
- **RIVN +0.11R (+$4.28)** — ranged 15.40–15.58 all day, never triggered stop or
  target. Scratch win; momentum died right after entry but it held above entry.
- **AAL paper +0.79R (+$31.41)** — peaked 13.52, **4 cents shy** of the 13.56
  target, then faded into the afternoon stall. The wider stop (13.35) was validated
  (the post-entry dip to 13.38 held). Two takeaways: (a) the wider-stop fix works;
  (b) a target set even slightly too far can turn a would-be 2R into a partial when
  afternoon momentum fades — consider a partial-profit / trail once MFE > ~1.3R.
- **HOOD −0.69R (−$27.72)** — the late-day (2:14pm) breakout **never followed
  through**: it barely printed a new high then drifted to 124.29 (didn't even hit
  the stop). Clean confirmation of the caveat I logged at entry.
**Lesson candidate (O003):** late-day breakouts (entered after ~1:30–2pm ET) show
weaker follow-through than midday ones — the runway to a 2:1 target is short and
afternoon momentum tends to fade. HOOD (late) failed while AAL (midday trend,
established since ~12pm) captured most of its move. Not yet a rule; watch for
repetition, then consider a "no fresh breakout entries after ~2pm ET" filter.
Day's paper tally (9/21): 6 closes — RIOT −1R, AAL(0010) −1R, NCLH −1R, RIVN
+0.11R, AAL(0011) +0.79R, HOOD −0.69R = net ~−2.8R (−$111.9 sim). Choppy-underneath
tape (indices green but individual names round-tripping) punished momentum entries;
only the midday-trend name (AAL) really worked. Running sample n=13 closed: 5 wins /
8 losers. Small sample; the edge case for "high-volume midday RS leaders" is holding
up better than the broad "any RS leader" read.

### Trade T-2026-0003 — AAL [EOD management plan]
Real AAL at 3:14pm ET = 13.475 vs 13.4699 entry (breakeven); tagged 13.52 then
faded. Thesis was an intraday breakout continuation and it has stalled. Plan: do
NOT hold overnight on a $20 account (gap risk); make the final close/hold call near
the close with fresh data (self check-in ~3:52pm ET). Broker stop 13.32 protects the
downside (max −$0.15) until then. If it re-breaks 13.52 it can run to target; if it
keeps drifting, close flat-to-small rather than carry it overnight.

### Trade T-2026-0003 — AAL 2026-09-21  [CLOSED — final review]
Snapshot (frozen, pre-outcome): data/snapshots/T-2026-0003.json
Result: **CLOSED +$0.05 (+0.33R).** Bought 1 @ 13.4699 (18:25:46Z), sold 1 @
  13.5201 (19:53:41Z), ~7 min before the close. Held ~1h28m. MFE +0.05 (0.33R),
  MAE −0.03 (0.20R). No fees. Entry favorable by ~$0.01 vs limit.
Classification: **GOOD DECISION + WIN.** Process was right and the outcome was
  positive — but per rule 19 a win on n=1 does NOT validate the strategy, and per
  rule 20 I don't raise strategy confidence off one trade. What made it a good
  decision (independent of the $0.05):
  - Real edge, defined first: RS leader breaking a new HOD on heavy volume and
    holding it — the exact high-volume-leader profile the paper book keeps rewarding.
  - Invalidation set before entry; mandatory broker-held stop attached seconds after
    fill; 2:1 target; options/crypto/margin OFF.
  - Stop placed WIDER than the base (13.32), applying the P-2026-0010 whipsaw lesson
    — and it was never threatened (MAE only reached 13.44).
  - Disciplined exit: the setup was an intraday breakout continuation; it stalled
    below target, so I closed into the close rather than carry overnight gap risk on
    a $20 account. Cancelled the resting GTC stop FIRST (freed the share), then sold
    — no naked order left behind.
Contrast with T-2026-0001 (F, BAD DECISION + LOSS): that was a no-edge owner-directed
  entry. This one was owner-*requested* but independently met the setup bar. Same
  owner ask ("trade today"), opposite process quality.
Honest framing (unchanged): +$0.05 is not income — on 1 share the edge is swamped by
  spread/fees at any real scale, and $20 still cannot fund operations. The value of
  T-2026-0003 is that the FULL real pipeline now works on a genuine edge:
  scan → confirm RS+volume breakout → size from risk → enter → attach stop →
  manage → exit flat-to-green → journal. That is the asset, not the nickel.
Lessons/actions: no new MISTAKE (clean process). Reinforces the forming
  "high-volume midday RS leader" edge (LESSONS candidate, still paper-driven; one
  real win is not promotion evidence). Account reconciled flat post-trade.

### PAPER 2026-09-22 10:15 ET pass — 2 miner longs (P-2026-0014/0015)
First high-volume pass of the ramped-up engine. Flat/mild tape (SPY +0.1%, QQQ +0.6%)
but clear stock-specific leadership from crypto-miners.
- **MARA (P-2026-0014)**: entry 13.91, stop 13.60, target 14.53, 129 sh. +4.7% RS
  leader; steady higher-high staircase to a new HOD 13.97 on a 1.2M-share bar (~2x).
- **RIOT (P-2026-0015)**: entry 25.22, stop 24.80, target 26.06, 95 sh. +4.2%; new
  HOD 25.355 on ~2x volume; staircase all morning.
Both are the miner "high-volume leader making new highs" pattern that hit +2R twice
last week — deliberately concentrating paper volume on the pattern with the best
evidence rather than spraying. Noted risk: both entered just after a 14:10 spike bar,
so a slight chase — stops set with room under the 14:00-14:05 base to absorb a normal
pullback (whipsaw lesson).
PASSED (documented): CHPT +6.5% (biggest mover but THIN 14-80k vol + already spiked
and pulling back — thin-name-whipsaw risk); CCL (fading below its open, no new high);
AAL (chopping mid-OR, no breakout). Discipline over count: took the 2 clean leaders,
skipped the 3 that don't fit, even on a "high-volume" mandate.

### PAPER 2026-09-22 11:14 ET pass — both miners stopped; CLF added
Tape went DEAD FLAT (SPY +0.01%, QQQ +0.5%) and morning leaders faded across the board.
- **MARA (P-2026-0014) STOPPED −1R (−$39.99)** and **RIOT (P-2026-0015) STOPPED −1R
  (−$39.90).** Both topped EXACTLY on the 14:10 spike bar I entered on, then faded the
  whole hour to my stops. This is the "slight chase after the spike bar" I explicitly
  flagged at entry — and it cost the full −1R on both. **Reinforces O002 hard: entering
  immediately after a vertical spike bar = buying the local top.** The read (miner
  leadership) was right; the *timing* was the flaw. Classified GOOD DECISION + LOSS,
  loss_class EXECUTION (not strategy — the entry trigger was wrong, not the selection).
  Actionable refinement (candidate rule): on a momentum name, don't enter on the spike
  bar itself — wait for a 1-2 bar pullback/hold or a re-break of the spike high.
- **CLF (P-2026-0016) OPENED** 12.46, stop 12.30, target 12.78, 250 sh. Deliberately a
  DIFFERENT profile: steel name +3.2% grinding HIGHER LOWS on decent volume, coiling
  under its HOD 12.54 — a controlled continuation, not a vertical spike. It was the one
  name still firming while miners/airlines/cruise all faded. Testing whether a
  coil-continuation entry behaves better than a spike-chase in a flat tape.
Pass net so far today: MARA −1R, RIOT −1R (−$79.89 sim). Flat choppy tape is punishing
momentum — a useful regime data point: SPY ~flat = spikes mean-revert. Being more
selective on remaining passes per the standing guidance.

### 2026-09-22 12:14 ET engine pass (STEP A real + STEP B paper)
STEP A (real): CLF (T-2026-0004) OPEN, 12.43 vs 12.50 entry (−$0.07 unrealized); faded
from the coil rather than breaking 12.54, but stop 12.33 NOT hit (low 12.445). Holding
— not invalidated; stop + EOD check manage it. No 2nd real position (one at a time).
STEP B (paper): CLF paper (P-2026-0016) still OPEN (12.43; no stop/target). NO NEW
paper entries — flat/soft tape (SPY −0.02%, QQQ +0.5%) and morning leaders fading hard
(MARA +4.7→+3.4, RIOT +4.2→+2.4, CHPT +6.5→+4.0). Forcing longs into midday chop is
exactly what generated the AM −1R stops; per the flat-tape rule I stood down on new
entries. A disciplined zero-new-entry pass, not a missed one — the setups aren't there.

### 2026-09-22 1:14 ET engine pass (STEP A real + STEP B paper)
STEP A (real): CLF (T-2026-0004) turned UP — broke the coil to a new HOD 12.645, now
12.59, +0.85R MFE. RAISED the stop to breakeven 12.48 (cancelled the 12.33 stop
6ab2a321 -> new stop 6ab2b7cb @ 12.48) per the Asymmetry Rule (autonomy may only
REDUCE risk). Now a FREE trade: max loss ~$0.02, open shot at target 12.84. Holding;
EOD check re-pointed to the new stop id. No 2nd real position.
STEP B (paper): CLF paper (P-2026-0016) also green (12.59; target 12.78 not yet hit) —
the coil-continuation setup is WORKING while today's spike-chases (MARA/RIOT) failed.
That contrast is the day's cleanest lesson: in a flat tape, a controlled higher-lows
coil/pullback near HOD beats chasing a vertical spike. NO new paper entries — the tape
is still flat (SPY -0.03%) and no other clean coil/pullback is presenting; not forcing
midday-chop longs (consistent with the AM stops). CLF is the standout and it's already held.

### 2026-09-22 2:14 ET engine pass
STEP A (real): CLF (T-2026-0004) grinding up — HOD 12.705, now 12.625 (+1.2R MFE),
well above the breakeven stop 12.48. Deliberately NOT tightening the stop into the
12.60 base (that would risk the whipsaw the journal keeps flagging) — breakeven
already makes it free; letting it breathe toward the 12.84 target. EOD check manages.
STEP B (paper): CLF paper (P-2026-0016) green, peaked 12.705 (7.5c shy of 12.78 target),
still OPEN. NO new entries — it's 2:14pm (late-day, O003 caution), tape only mildly
firmer (SPY +0.05%), and the one clean setup today (CLF coil-continuation) is already
held in both books. Honest read: today's tape offered essentially ONE clean setup, not
many — quality gating means low-count days happen, and forcing more into late-day chop
is how the AM losses happened. Discipline over count.

### Trade T-2026-0004 — CLF 2026-09-22  [CLOSED — final review]
Snapshot: data/snapshots/T-2026-0004.json
Result: **CLOSED +$0.05 (+0.30R).** Bought 1 @ 12.50 (15:47Z), sold 1 @ 12.5503
(19:15Z, ~45 min before close). Held ~3.5h. MFE +0.205 (+1.2R, HOD 12.705), MAE −0.108
(low 12.392, above the original 12.33 stop). No fees.
Classification: **GOOD DECISION + WIN.** Process notes:
- Entry was a COIL near support in the day's RS leader (bucking a red SPY) — the
  deliberate opposite of the morning's paper spike-chases (MARA/RIOT, O002). The coil
  broke UP to 12.705; the spike-chases faded. Same tape, opposite technique, opposite
  result — the day's cleanest confirmation that in a flat tape you buy the pullback,
  not the spike.
- Managed correctly: mandatory stop first (12.33), then RAISED to breakeven (12.48) at
  +0.85R to make it a free trade (Asymmetry Rule), then BANKED the gain when it stalled
  short of the 12.84 target and rolled off its HOD into a soft close — rather than let
  a winner round-trip. No overnight hold.
- Honest: +$0.05 gave back from +1.2R MFE. A tighter trail would have captured more,
  but tightening into the 12.60 base risked the exact whipsaw the journal keeps
  flagging — I chose to let it breathe, and it stalled. Acceptable; the exit was
  green and disciplined. Per rule 19, n-small win does NOT validate the strategy.
Real record now: 2 edge-based trades, 2 wins (AAL +0.33R, CLF +0.30R); lifetime real
P&L −$0.01 (F −$0.11 no-edge, AAL +$0.05, CLF +$0.05) — essentially flat, capital
preserved. The edge-based process is showing small consistent green; keep the sample
growing before drawing conclusions.

### 2026-09-22 EOD summary (4pm last pass)
Real account FLAT, ~$20.00, 0 positions/orders. Paper book flattened.
REAL (STEP A): 1 trade — CLF T-2026-0004 +$0.05 (+0.30R), GOOD DECISION + WIN. Edge-based
record now 2/2 (AAL +0.33R, CLF +0.30R); lifetime real P&L -$0.01 (capital preserved).
PAPER (STEP B) 9/22: 3 trades — MARA -1R & RIOT -1R (spike-chases, loss_class EXECUTION,
O002), CLF +0.47R (coil-continuation, partial). Day -1.5R (-$61.14 sim). Running sample
16 closed: 6 wins / 10 losers.
DAY'S KEY LESSON (real + paper agree): in a flat/choppy tape (SPY ~flat all day),
momentum MEAN-REVERTS — vertical-spike entries get sold (MARA/RIOT/AM real PASSes),
while controlled higher-lows COIL/PULLBACK entries near the HOD work (CLF real +0.30R,
CLF paper +0.47R). Candidate rule for promotion after more samples: "flat tape ->
prefer coil/pullback-continuation over breakout/spike entries; never enter on the
spike bar itself (O002)." Not promoted yet; growing the sample.

### 2026-09-23 11:15 ET engine pass
Tape still RISK-OFF (SPY -0.5%, QQQ -0.75%). REAL: PASS (flat all day; correct in a red tape).
PAPER CLF (P-2026-0017, RS-in-downtape test): WORKING — held the coil (dip to 12.505 > stop
12.45), then broke to a new HOD 12.795 (+1.46R MFE), now 12.78, near the 12.87 target, while
the market stays red. Early read on the test question: relative strength CAN pay even in a
falling tape when the name carries its own bid (CLF steel, idiosyncratic). Note the tension:
the real-$20 regime gate made me PASS this same name at the coil (correct on average — longing
a red tape is -EV), and chasing it real NOW (+2%, post-spike) would violate O002. So the paper
test banks the "it can work" data without taking real risk in a red tape — exactly the split
the two books are for. No new entries (rest of universe red). Leaving CLF paper open toward target.

### 2026-09-23 12:14 ET engine pass
Tape still red (SPY -0.6%, QQQ -0.9%). REAL: PASS (flat all day). PAPER CLF (P-2026-0017):
ran to 12.8599 at noon — literally 1c shy of the 12.87 target (+1.93R MFE) — then faded to
12.77. No target/stop hit; left OPEN (will resolve at target/stop or EOD flatten). The
RS-in-downtape test has clearly answered its question INTRADAY: CLF rallied ~+2.5% off entry
while SPY fell to -0.6% — relative strength with an idiosyncratic bid can run against a red
tape. (Second time this exact target-by-a-penny near-miss has cost CLF a clean +2R tag — candidate
refinement: set the target ~1 tick inside a round/psychological level like 12.85 rather than
12.87.) No new entries. Real $20 flat/preserved in a down day = correct.

### 2026-09-23 1:12 ET engine pass
Tape weakening further (SPY -0.85%, QQQ -1.2%). REAL: PASS (flat all day, correct). PAPER CLF
(P-2026-0017): drifting off its 12.8599 high with the market, now 12.725 (~+1R unrealized),
above stop 12.45; no target/stop hit -> left OPEN (4pm flattens). No new entries (universe red).
Quiet hold; account flat $20.00.

### Trade P-2026-0017 — CLF 2026-09-23  [CLOSED — RS-in-downtape test]
Result: **+2.00R (+$79.80 sim), GOOD DECISION + WIN.** Entry 12.59 (10:15 ET), target 12.87
hit 1:40 ET; MFE 12.93 (+2.43R), MAE only 12.505 (never near the 12.45 stop). CLF rallied
from 12.59 to 12.93 (+2.7%) WHILE SPY fell -0.5% and QQQ -1% the entire time.
The test question — "does relative strength survive a falling tape?" — got a clean YES on
this instance: a name with genuine RS and an idiosyncratic bid (CLF steel) can run a full
2:1 against a red market. IMPORTANT nuance for the real account: the real-$20 regime gate
made me PASS this same setup all day (correct on average — longing a red tape is -EV, and I
cannot know in advance which RS name will buck it). This paper win is evidence, not a mandate:
- Candidate rule refinement (needs MORE samples before promotion): "In a red tape, a real
  long MAY be allowed ONLY for the single strongest RS name that is GREEN and holding a
  higher-lows coil (not a spike), with a tight stop — otherwise stay flat." Do NOT act on
  n=1; keep logging RS-vs-downtape cases. For now the gate stays: red tape -> real PASS.
Also validates the earlier target-placement note: the noon penny-miss (12.8599 vs 12.87)
resolved because I left the target open rather than tightening — patience paid.

### 2026-09-23 3:12 ET engine pass
Tape still red (SPY -0.7%, QQQ -0.9%). Paper book FLAT (CLF P-2026-0017 already closed +2R
at 1:40). Real FLAT all day. No new entries — late day + red tape + no clean coil presenting
(everything red except CLF, which faded off its 12.93 high). Quiet; nothing to manage. 4pm pass
will post the EOD wrap. Account $20.00.

### 2026-09-24 11:13 ET engine pass
Tape weakening (SPY -0.5%, QQQ -0.8%). REAL: PASS (flat all day, correct). PAPER RIVN
(P-2026-0018, RS-in-downtape test #2): FADING — entered 15.38 (extended, the flagged chase),
rolled straight back to 15.08, sitting on the 15.05 stop (low 15.07, not yet hit). Still OPEN.
KEY CONTRAST vs yesterday's CLF (+2R): CLF was entered at the COIL and worked; RIVN was entered
EXTENDED (+3% off the low) and is failing. Same RS-in-downtape thesis, opposite entry location,
opposite result. Refines the candidate rule: the edge isn't "RS name in a red tape" — it's "RS
name entered at a coil/pullback, NOT chased at the highs" (O002). This is exactly why real PASSED
(would have been a chase). Leaving RIVN open toward stop/target. No new entries (universe red).

### 2026-09-24 12:13 ET engine pass — RIVN stopped -1R (chase confirmed)
PAPER RIVN (P-2026-0018) STOPPED -1R (-$39.93) at 15.05, ~11:35 ET. MFE ~0.00 — it never
traded above my 15.38 entry; I bought the exact extended high tick. Textbook chase failure.
RS-in-downtape experiment now has a clean A/B:
  - CLF 9/23: entered at the COIL -> +2R WIN
  - RIVN 9/24: entered EXTENDED (+3% off low) -> -1R LOSS (MFE 0)
Same thesis (lone RS name in a red tape), OPPOSITE entry location, opposite result. Conclusion
strengthening: the edge is the ENTRY (coil/pullback), not merely the relative strength. This is
also precisely why the real $20 correctly PASSED both — CLF was un-triggered at the coil under
the regime gate, and RIVN would have been a chase. REAL: still flat all day (SPY -0.5%, QQQ -0.8%,
3rd red day). No new entries. Real account preserved at $20.00.

### 2026-09-24 1:12 ET engine pass
Tape RECOVERED to flat (SPY/QQQ ~-0.02%, back from -0.5%). REAL: PASS — no clean trigger;
RIVN bounced to +2.1% but is choppy (round-tripped 15.38->15.05->15.33), not a fresh coil, and
chasing its recovery = the same mistake that just cost -1R. Others modest (NCLH +1.2%, AAL +0.9%).
PAPER: no new entries (no clean coil/breakout; choppy). Book flat (RIVN closed -1R earlier). Real
$20 flat/preserved. Quiet hold into the last pass.

### 2026-09-24 2:12 ET engine pass
Tape mild-red (SPY -0.15%, QQQ -0.26%). RIVN pushed to a NEW HOD 15.505 (+3.2%) after stopping
my chased paper entry — this CONFIRMS the lesson: the name (RS holdout) was right, the entry
(chased 15.38 vs the 15.10 coil) was wrong. Chasing it now at a fresh high, late day, repeats the
error -> PASS. REAL: flat all day (correct). PAPER: no new entries (late/O003, RIVN extended, no
fresh coil elsewhere). Book flat; real $20 preserved $20.00. 4pm pass = EOD wrap.

---
### Engine pass 2026-09-25 10:13 ET (14:13Z) — REAL: PASS · PAPER: 0 entries (fade tape)

**Regime flip:** Green open FULLY faded. SPY +0.31%→+0.02% (flat), QQQ +0.45%→+0.12%. Gap-up-and-fade.

**STEP A (real $20):** FLAT, reconciled clean (0 pos / 0 orders). No RS leader making & holding a new
intraday high on volume. AAL, the best affordable RS name, is fading off its OR high (13.63→13.43).
→ PASS. Correct — nothing to take.

**STEP B (paper):** Checked 5-min structure on every name still green/holding (AAL, RIVN, NCLH, F, CCL).
ALL are lower-highs / lower-lows since the open — a unanimous bleed, zero coils or higher-lows setups:
- AAL 13.63→13.43 · NCLH 14.44→14.14 · F 12.72→12.57 · CCL 22.04→21.69 · RIVN choppy fade 15.65→15.33
- Red/collapsing: MARA −5.3%, RIOT −3.4%, CLF −1.3%, HL −0.8%, VALE −0.9%, SOFI −0.7%.
→ 0 paper longs. Standing rule (flat/red tape → tighten, favor coils, no chasing) says do NOT force longs
into a unanimous downtrend. I already have ample "chase-a-fade = loss" samples (RIVN yday, all last week).
The learning move here is recognizing the fade and standing aside. Later passes will catch a coil/reclaim
if the tape stabilizes.

**Tally (9/25):** REAL 0 trades (flat, $20 preserved). PAPER 0 new (book flat). Tape: gap-and-fade to flat.

---
### Engine pass 2026-09-25 11:13 ET (15:13Z) — REAL: PASS · PAPER: 3 new longs

**Regime:** Tape stabilized & ticked back green. SPY +0.20%, QQQ +0.23% (recovered the gap-fade). Fresh RS
leaders appeared: F +1.1% (new session high), HL +1.1% (gold/silver bid, KGC +0.9%). Miners still red (MARA -4.3%, RIOT -2.7%).

**STEP A (real $20): PASS.** Reconciled FLAT (0/0). Two real candidates but neither clears the ≥2:1 gate cleanly:
- F — CLEAN base-breakout-and-hold above 12.72 on volume; best entry location. But it's low-beta Ford: a
  realistic measured-move target (~12.88) only gives ~1:1 with a sane stop; forcing 2:1 needs 13.05 (+3.6%, unlikely). Fails R:R.
- HL — strong higher-lows trend, sector-confirmed. But entry now (18.14) is mid-range AFTER a +3% run =
  chase location (the RIVN mistake), and 2:1 needs an aggressive new-high push. Marginal.
→ Keep real $20 flat rather than force a sub-2:1 or chase. Capital preserved.

**STEP B (paper): 3 valid longs opened** (structure finally present; still selective — 3 valid, not 8 forced):
- P-2026-0019 HL 18.14, stop 17.88, tgt 18.66 (153sh) — extended-trend-continuation entry.
- P-2026-0020 F 12.735, stop 12.57, tgt 13.065 (242sh) — base-breakout-AT-the-break (best location).
- P-2026-0021 NCLH 14.29, stop 14.10, tgt 14.67 (210sh) — pullback-reclaim after the flush.
Deliberate A/B: three DIFFERENT entry locations (extended / at-breakout / reclaim) on the same green tape —
tests whether entry location again separates winners from losers (CLF-coil vs RIVN-chase thesis).

**Tally (9/25):** REAL 0 trades (flat, $20 preserved). PAPER 3 open (HL/F/NCLH). Tape: gap-fade then recovery to soft-green.

---
### Engine pass 2026-09-25 12:13 ET (16:13Z) — REAL: PASS · PAPER: 1 WIN closed, 2 open

**Regime:** Tape now solidly risk-on. SPY +0.59%, QQQ +0.59% (the recovery held & extended). Leaders ran:
AAL +4.0%, CCL +3.0%, KGC +2.1%, NCLH +3.6%.

**PAPER management (3-way entry-location A/B, entered 11:13 ET):**
- P-2026-0021 NCLH (RECLAIM entry 14.29) → **TARGET 14.67 HIT, +2.00R WIN** at ~12:00 ET. MAE ~0 — never
  underwater. Cleanest of the three.
- P-2026-0020 F (AT-BREAKOUT entry 12.735) → OPEN, working (+0.45R MFE, new HOD 12.81, holding). Low-beta so 2:1 (13.065) is slow.
- P-2026-0019 HL (EXTENDED entry 18.14) → OPEN, chopped (dipped to 18.005, held stop) then recovered (+0.54R MFE). Target 18.66 far.
- **Read so far:** reclaim/pullback entry (NCLH) resolved to full +2R first and with zero heat; the extended
  entry (HL) took the most heat. Consistent with CLF-coil vs RIVN-chase: ENTRY LOCATION separates them.

**STEP A (real $20): PASS.** Reconciled FLAT. Tape is strong but the affordable leaders are now EXTENDED
(+3-4%) — entering here = chasing. F is the only non-extended affordable name still making new highs, but
low-beta keeps a realistic 2:1 out of reach. No clean non-chase entry that clears the gate → keep $20 flat.
Watching for a leader (NCLH/AAL) to pull back to a higher-low and coil = a real entry candidate next pass.

**Housekeeping:** repaired a pre-existing stray comma in P-2026-0018 notes (CSV now clean, all rows 30 cols).

**Tally (9/25):** REAL 0 trades (flat, $20 preserved). PAPER 3 taken → 1 WIN (+2R NCLH), 2 open (F, HL). Tape: gap-fade → strong afternoon recovery.

---
### Engine pass 2026-09-25 13:13 ET (17:13Z) — REAL: PASS · PAPER: 2 open (both stalling), 0 new

**Regime:** Still green, eased off noon highs. SPY +0.49%, QQQ +0.51%.

**PAPER management:**
- P-2026-0020 F (breakout 12.735) → OPEN, STALLING. Chopped 12.70-12.81 for an hour; target 13.065 never
  approached (MFE ~0.45R). Low-beta 2:1 problem confirmed in real time.
- P-2026-0019 HL (extended 18.14) → OPEN, STALLING. Range-bound 18.10-18.26; target 18.66 far (MFE ~0.54R).
- Thesis update: the RECLAIM entry (NCLH) already banked +2R and closed; the BREAKOUT and EXTENDED entries
  are both dead-money grinds. Entry location isn't just about heat taken — it's about which entries actually
  reach target. Reclaim/pullback did; breakout-into-stall and extended did not (so far).

**STEP A (real $20): PASS.** FLAT. Leaders extended (NCLH +3.7% at HOD, AAL +3.6%); F/HL stalling & low-beta.
No clean non-chase affordable entry clearing 2:1. Keep $20 flat.

**No new paper adds** — everything is either extended (chase) or stalling; no fresh coil/pullback setup. Discipline over volume.

**Tally (9/25):** REAL 0 trades (flat, $20 preserved). PAPER 3 taken → 1 WIN (+2R NCLH), 2 open/stalling (F, HL).

---
### Engine pass 2026-09-25 14:13 ET (18:13Z) — REAL: PASS · PAPER: 2 open (grinding into EOD)
Regime steady green (SPY +0.54%, QQQ +0.56%). F 12.77 (range 12.70-12.78, target 13.065 unreached) and
HL 18.135 (range 18.05-18.19, target 18.66 far) both still chopping — neither near stop or target; both
likely EOD-flatten candidates. Real FLAT, leaders extended/fading (NCLH back to 14.55), no clean entry → PASS.
No new paper adds. Tally 9/25: REAL 0 (flat, $20 preserved); PAPER 1 WIN (+2R NCLH) + 2 open (F/HL grinding).

---
### Engine pass 2026-09-25 15:13 ET (19:13Z) — REAL: PASS · PAPER: 2 open (hold into EOD)
Green (SPY +0.49%). HL 18.28 grinding to new HOD 18.30 (+0.54R) but tgt 18.66 far; F 12.724 back below entry (dead money). Neither at stop/target. Real FLAT → PASS. Next pass = EOD flatten. Tally: REAL 0 (flat, $20); PAPER 1 WIN + 2 open.

---
### Engine pass 2026-09-28 10:14 ET (14:14Z) — REAL: PASS · PAPER: 2 new RS-in-downtape coils
**Regime:** RISK-OFF, worsening. SPY −0.51%, QQQ −1.16% (tech-led). MARA's morning pop already faded to red
(−0.6%) — the 9:47 pass on it was correct. RS names bucking the tape: CCL +0.9%, SIRI +0.68%, KVUE +0.22%.

**STEP A (real $20): PASS.** FLAT (0/0). The RS leaders (CCL ~$22.4, SIRI ~$26) are BOTH >$19 → can't buy 1
share w/ buffer on $20. KVUE affordable ($17.84) but thin volume + only +0.2% (weak defensive drift), not a
leader. No affordable RS momentum name on a red tape → PASS. (Same structural constraint as Fri: the RS names
that work are too pricey for the $20 account.)

**STEP B (paper): 2 valid RS-in-downtape coils opened** (tightened for red tape → coils only, no breakouts-into-air):
- P-2026-0022 CCL 22.395, stop 22.09, tgt 23.00 (131sh) — 30-min higher-lows coil then new HOD, green +0.9% vs QQQ −1.16%.
- P-2026-0023 SIRI 26.03, stop 25.66, tgt 26.77 (108sh) — higher-lows grind to new HOD, defensive RS.
Both are the core "RS-in-downtape coil" test (the CLF-coil-wins pattern). Same-session pair for clean comparison.

**Tally (9/28):** REAL 0 (flat, $20 preserved, red tape). PAPER 2 open (CCL, SIRI). Book was flat coming in.

---
### Engine pass 2026-09-28 12:14 ET (16:14Z) — REAL: PASS · PAPER: both coils STOPPED −1R each; 0 new
**Regime:** RED and DETERIORATING. SPY −0.78% (from −0.5% at 10am), QQQ −1.23%. A grind-lower tape.

**PAPER management (covering the classifier-outage gap at 11:13 — reconstructed from 5-min bars):**
- P-2026-0022 CCL (coil-breakout 22.395) → STOPPED 22.09 at ~11:00 ET. −1.00R. MFE ~0 (bought the breakout tick, faded instantly).
- P-2026-0023 SIRI (coil 26.03) → STOPPED 25.66 at ~12:00 ET. −1.00R. MFE ~0.05R (entered near HOD).
- Both RS-in-downtape LONGS failed. Net −2R (−$79.92).

**KEY LESSON (new, important):** RS-in-downtape longs are regime-sensitive. The WINNERS (CLF +2R 9/22,
NCLH +2R 9/25) were in FLAT-to-RECOVERING tapes. Today's tape was RED and actively DETERIORATING (−0.5%→−0.8%),
and both RS names got dragged down with it — the relative strength did NOT protect the long. Refinement to the
RS-in-downtape thesis: it needs a STABILIZING backdrop (flat/basing SPY), NOT a tape making fresh lows. Also both
entries were at the coil-BREAKOUT tick (MFE ~0) — reinforces reclaim/pullback > breakout yet again.

**STEP A (real $20): PASS.** FLAT. Deteriorating red tape, no affordable RS leader holding up. Correct — and today
is exactly why the red-tape→PASS gate protects the real $20: both "best" setups of the day lost. Capital intact.

**No new paper adds** — a red, deteriorating tape is a no-long environment; forcing more longs = more −1R donations.

**Tally (9/28):** REAL 0 (flat, $20 preserved). PAPER 2 closed, both −1R (CCL, SIRI) = −2R on the day. Lifetime paper: 23 closed, 9W/14L.

---
### Engine pass 2026-09-28 13:13 ET (17:13Z) — REAL: PASS · PAPER: 0 new (bounce, but unstable)
Tape bounced off lows, still red: SPY −0.35% (from −0.78%), QQQ −0.70% (from −1.23%). CCL reclaimed to +0.67%,
KVUE +0.39% (affordable, steady defensive), VALE +0.26%; laggards still bleeding (CLF −7.5%, HL −4.9%, RIVN −3%).
STEP A real: PASS — still red; only affordable green name is KVUE (thin/weak defensive drift, not a leader). STEP B:
no adds — CCL is back at 22.40, the exact level it FAILED at an hour ago (−1R); re-buying prior resistance on a
bouncing-but-red tape = low conviction, repeats the loss. Wait for a clean green-tape reclaim. Tally 9/28: REAL 0
(flat, $20 preserved); PAPER 2 closed −2R (CCL, SIRI), 0 open.

---
### Engine pass 2026-09-28 14:13 ET (18:13Z) — REAL: PASS · PAPER: 0 new (bounce faded)
The 1pm bounce faded — SPY back to −0.52%, QQQ −0.82% (choppy red, no follow-through). CCL +0.3%/KVUE +0.3% still
green but stalling; no clean RS progress. Real FLAT → PASS (red tape, no affordable leader). No paper adds — the
"stabilization" was a dead-cat bounce; the no-long read from 12:14 holds. Book flat. Tally 9/28: REAL 0 (flat, $20);
PAPER 2 closed −2R, 0 open.

---
### Engine pass 2026-09-28 15:13 ET (19:13Z) — REAL: PASS · PAPER: 0 new (weak into close)
Tape leaking to new lows into the last hour: SPY −0.69%, QQQ −0.98%. Only KVUE +0.3% (defensive) still green; rest red.
No clean setup. Real FLAT → PASS. Book flat, no paper adds. Next pass = post-close EOD wrap. Tally 9/28: REAL 0 (flat, $20); PAPER 2 closed −2R, 0 open.

---
### Engine pass 2026-09-29 ~11:17 ET (15:17Z, fired late) — REAL: PASS · PAPER: 1 new (RIVN coil-after-breakout)
Reconciled FLAT. Tape mixed/soft: SPY −0.20% (red), QQQ +0.24%. Open gap-up faded (AAL back to red −0.15%).
NCLH still +4.5% but rangebound 14.90-15.10 all session (no breakout). RIVN turned RS leader +2.5%: based 14.70 →
higher-lows → broke base on 2x-vol bar to HOD 15.34 → now HOLDING the breakout in a 15.05-15.19 coil. Affordable ~$15.15.

STEP A (real $20): PASS. RIVN is structurally the cleanest affordable setup in days (coil-after-breakout-hold, not a
spike), BUT the pre-trade gate wants a SUPPORTIVE regime and SPY is RED on a proven fade-day. Regime gate → PASS.
Capital preserved. (This is a genuine borderline — noting it: on a green SPY this likely would have been a real take.)

STEP B (paper): P-2026-0024 RIVN 15.16, stop 14.93, tgt 15.62 (173sh) — tests the coil-after-breakout-HOLD entry
in a mixed tape; explicit contrast to P-2026-0018 (RIVN spike-CHASE, −1R). Same name, opposite entry location.

Tally (9/29): REAL 0 (flat, $20 preserved). PAPER 1 open (RIVN). Book was flat coming in.

---
### Engine pass 2026-09-29 12:14 ET (16:14Z) — REAL: PASS · PAPER: RIVN open (stalling), 0 new
Tape weakening: SPY −0.35% (new lows), QQQ +0.02% (flat). RIVN paper coil holding 15.04-15.20 but STALLING — never
approached 15.62 tgt (MFE ~+0.17R), now 15.03 near range low as SPY drops (stop 14.93 intact, still OPEN). This is
validating the real-PASS: the coil isn't following through in a red/weakening tape (same regime lesson as Mon). AAL
−0.5%, NCLH faded to +3.5% rangebound. Real FLAT → PASS. No new adds (weakening tape). Tally 9/29: REAL 0 (flat, $20); PAPER 1 open (RIVN).

---
### Engine pass 2026-09-29 13:13 ET (17:13Z) — REAL: PASS · PAPER: RIVN open (bleeding toward stop), 0 new
Tape soft: SPY −0.39%, QQQ −0.08%. RIVN paper drifting down with the tape: 15.16 entry → 14.98 now (~−0.78R
unrealized), hovering just above 14.93 stop (not hit). Coil held ~1h then rolling over. Real FLAT → PASS; RIVN
underwater keeps validating the regime pass (would be −0.8R if it had been real). No new adds. Tally 9/29: REAL 0 (flat, $20); PAPER 1 open (RIVN, weak).

---
### Engine pass 2026-09-29 14:13 ET (18:13Z) — REAL: PASS · PAPER: RIVN open (held stop, back to BE), 0 new
Tape firmed: SPY −0.26% (off lows), QQQ +0.08%. RIVN never hit 14.93 stop (low ~14.98), bounced to 15.23 then 15.165
= ~breakeven vs 15.16 entry (MFE +0.30R, tgt 15.62 far). Still OPEN — coil survived the bleed. Real FLAT → PASS. No adds.
Tally 9/29: REAL 0 (flat, $20); PAPER 1 open (RIVN ~BE).

---
### Engine pass 2026-09-29 15:13 ET (19:13Z) — REAL: PASS · PAPER: RIVN open (grinding ~BE into EOD), 0 new
Tape firming: SPY −0.14% (off lows), QQQ +0.24%. RIVN chopped 15.13-15.265 all afternoon, holding just above 15.16
entry (now 15.145 ~BE); MFE +0.46R (15.265) but never reached 15.62 tgt, never hit 14.93 stop. Still OPEN → EOD flatten
next pass. Real FLAT → PASS. No adds. Tally 9/29: REAL 0 (flat, $20); PAPER 1 open (RIVN ~BE).

---
### REAL TRADE OPENED 2026-09-30 10:16 ET (14:16Z) — T-2026-0005 LONG 1 VALE @ 13.6472
**First real trade since 9/22 (CLF).** Setup: ORB break-and-hold on a genuinely supportive+broadening tape.
- **Regime (the differentiator):** SPY +0.53%, QQQ +0.69% — green AND strengthening, with 3 affordable names
  (VALE/NCLH/RIVN) breaking their opening ranges TOGETHER = broad risk-on. This is the supportive regime my own
  lessons require and that was ABSENT Fri/Mon/Tue (all correctly passed). Regime gate finally satisfied.
- **Setup:** VALE coiled 13.41-13.48 (OR), then broke the OR high on a 2x-vol bar (439k) to a new HOD 13.61 and
  HELD — valid RS-leader ORB break-and-hold (+2.4% vs SPY +0.53%). Not a vertical spike; controlled coil→break.
- **Execution:** buy 1 share (order 6abd19b6) filled 13.6472; IMMEDIATELY attached mandatory GTC stop-market
  @13.44 (order 6abd19c6). Risk $0.21 (~1.04% of $20). Target 14.06 = exactly 2:1. Spread 0.07%, liquid.
- **Devil's advocate logged:** entry near HOD after a +2.4% run; quarter-end afternoon-reversal risk; breakout
  entries stalled all week — BUT those were choppy/red tapes, and risk is capped tiny ($0.21) with a hard stop.
- **Management:** raise stop to breakeven at ~+1R (asymmetry rule = reduce risk only); bank green / flatten by EOD;
  NEVER hold overnight. Managed on every hourly engine pass + EOD.
- **Why take it (vs the week of passes):** it clears ALL gates the mandate lists — supportive regime, valid
  break-and-hold on volume, affordable 1-share, tight spread. Passing this would be over-applying the
  choppy-tape "reclaim-only" lesson to a genuinely trending tape. n=small; a win won't validate, a loss won't refute.

---
### REAL TRADE CLOSED 2026-09-30 10:58 ET — T-2026-0005 VALE STOPPED −$0.20 (−0.98R)
Entry 13.6472 → stop 13.4437 (10:58 ET). 1 share. Loss −$0.20, ~1% of account. Account $20.00 → ~$19.80.

**What happened:** VALE printed a marginal new high (13.655) in the first minute after entry, then rolled straight
over and faded through the 13.44 stop within ~40 min. MFE ~+0.04R (basically zero). The broad tape STAYED green
(SPY +0.5%, QQQ +0.7%) — this was a VALE-specific fade, not a regime failure.

**Honest self-critique:** the entry LOCATION was the flaw. I bought the breakout tick near the HOD (+2.4% already
run) rather than waiting for a pullback-to-shelf-and-hold. MFE ~0 is the exact signature of the week's failed
breakouts (F, RIVN spike, CCL, SIRI paper). I overrode my own "reclaim/pullback > breakout-chase" edge on the
reasoning that a supportive tape justifies a breakout entry — and it still failed. LESSON, hardened: even on a
green/broadening tape, buying the breakout extension near HOD has poor follow-through; the edge is the
pullback/reclaim entry, not the break itself.

**What went RIGHT (process):** all gates were checked (supportive regime, affordable, tight spread, ≥2:1);
mandatory broker stop attached immediately; loss capped at exactly the plan (~1R / ~1%); no overnight risk; no
averaging down. The system contained a losing idea to $0.20. This is capital preservation working — a bad entry
cost 1% of the account, not a meaningful drawdown.

**Decision now:** FLAT. NO revenge re-entry — VALE just failed the same breakout pattern; chasing NCLH/RIVN
breakouts here would repeat the mistake. One real trade taken today, it lost small, capital intact. Real record
2W/2L; the 2 wins (AAL HOD-hold, CLF coil) and this loss (breakout-chase) all point the same way on entry location.

---
### Engine pass 2026-09-30 12:16 ET (15:13Z) — REAL: PASS (flat, post-stop) · PAPER: 0 new
Tape still green (SPY +0.58%, QQQ +0.76%) but the morning leaders STALLED into midday chop: VALE 13.475 (bounced
after stopping me — whipsaw, now chopping 13.45-13.48, no new high), NCLH 14.99 & RIVN 15.13 chopping mid-range below
HODs, AAL/F red. No clean break-and-hold or pullback-reclaim anywhere. STEP A real: PASS — no qualifying setup AND
no revenge re-entry after the VALE stop (discipline: one real shot taken, it lost small, stand aside). STEP B: 0 paper
adds — nothing clean; the morning breakouts all stalling by midday (even on a green tape) is the day's data point
(quarter-end mean-reversion). FLAT ~$19.80. Tally 9/30: REAL 1 trade (VALE -$0.20), PAPER 0.

---
### Engine pass 2026-09-30 13:13 ET (16:13Z) — REAL: PASS (flat) · PAPER: 0 new
Indices strong (SPY +0.62%, QQQ +0.90% — strength concentrated in big-cap tech I can't afford). Affordable names all
FADED from morning breakouts: VALE 13.44 (+1.1%, chopping near my stop, no new high), NCLH 14.80 (flat, gave back all
cruise gains), RIVN 15.10 (mid-range). No new highs / no clean coil-reclaim = no qualifying setup. Real FLAT → PASS (no
revenge after the VALE stop). No paper adds. Note: today's affordable morning-breakouts (VALE/NCLH/RIVN) ALL faded by
midday despite a green tape — reinforces the day's lesson. Tally 9/30: REAL 1 (VALE -$0.20), PAPER 0. Book flat.

---
### Engine pass 2026-09-30 14:13 ET (17:12Z) — REAL: PASS (flat) · PAPER: 0 new
Tape green (SPY +0.51%, QQQ +0.80%); affordable names chopping — VALE 13.515 (+1.6%, no new high), NCLH 14.70 (red), RIVN 15.09 (mid-range). No qualifying setup. Real FLAT → PASS. No paper adds. Book flat. Tally 9/30: REAL 1 (VALE -$0.20), PAPER 0.

---
### Engine pass 2026-09-30 15:13 ET (18:13Z) — REAL: PASS (flat) · PAPER: 0 new
Tape green, easing (SPY +0.42%, QQQ +0.80%). Affordable names chopping/fading (VALE +1.8% no clean setup, NCLH red, RIVN flat). No qualifying entry → PASS. No paper adds. Book flat (nothing to flatten EOD). Next pass = EOD wrap. Tally 9/30: REAL 1 (VALE -$0.20), PAPER 0.

## 2026-09-30 (Wed) — post-close note: the fade vindicated the stop
Official 4pm closes: SPY 762.36 (−0.24%, RED), QQQ 739.71 (+0.24%), VALE 13.405. At my VALE entry (10:16am) the tape
was genuinely green+broadening (SPY +0.53%) and it held past 9:45 — but it FADED into the bell (SPY gave back ~0.55%
from the 3:17pm +0.32% to close red). VALE never recovered above my 13.6472 entry and closed 13.405. Takeaways:
(1) The 10:58am stop-out at 13.4437 was not just "loss capped" — it removed me from a name that bled all day; holding
    would have been worse, and any revenge re-entry would have compounded the mistake. No-revenge rule paid off.
(2) The quarter-end afternoon-reversal risk I explicitly wrote in the T-2026-0005 devil's-advocate MATERIALIZED. When
    a named tail risk is real, size/stop for it (I did: tiny risk, mandatory stop, no overnight) — that's why a correct
    decision + a lost trade + a fading tape still left capital fully intact.
(3) "Entry location is the edge, regime is the ceiling" got a clean live datapoint: the ceiling itself dropped (green→red
    into the close), so even a better entry location likely loses today. The regime gate is necessary; the close proves
    a supportive OPEN is not a guaranteed supportive DAY.

## 2026-10-01 (Thu) — Engine pass 10:13 ET → REAL PASS + PAPER PASS
Tape rolled over after the 10am ISM print: SPY 760.40 (−0.29%, down from +0.05% at 9:48), QQQ 738.60 (−0.16%) —
the bounce-off-red open failed and flipped to a downtrend. Affordable universe ALL red: HBAN −2.5%, MARA −2.4%,
RIVN −1.4%, AAL −1.4%, VALE −1.2%, NCLH −1.0%, BTG/HL/CLF/F red; only SNAP +0.2% / SOFI flat (neither a setup).
STEP A (real $20): PASS — no RS leader making/holding new highs; red deteriorating tape = regime gate forces pass.
STEP B (paper): PASS — long-only engine, and a red trending-down tape has no valid long setups (everything making
intraday lows, nothing coiling with higher lows). Per the standing lesson (tighten/avoid chasing in red tape;
regime is the ceiling), forcing paper longs for volume here would be low-edge chasing. Account FLAT $19.79, 0/0.
Next pass re-evaluates; a reclaim/coil could still set up if the tape stabilizes.

## 2026-10-01 (Thu) — Engine pass 11:13 ET → REAL PASS + PAPER PASS
Tape still trending down: SPY 759.82 (−0.37%, lower than 10:13's −0.29%), QQQ 737.54 (−0.30%). Universe deeper red
(MARA −2.9%, AAL −2.1%, RIVN −2.0%, VALE −1.7%, NCLH −1.7%, SOFI −1.0%). Lone RS name: HL +0.44% (green vs red tape),
but choppy BELOW its 17.23 OR high — no new intraday high, not a clean coil near HOD. This is the "RS-in-a-downtape"
case the journal flagged: such longs need a STABILIZING tape and fail in a deteriorating one (tape still making lows),
so HL's relative strength is NOT a green light. SNAP flat (+0.1%), no momentum. STEP A (real): PASS — no leader at new
highs, red deteriorating tape. STEP B (paper): PASS — long-only, no valid long setup in a downtrend; not chasing for
volume. 3rd straight PASS today (9:47 / 10:13 / 11:13) — correct restraint on a red day. Account FLAT $19.79, 0/0.

## 2026-10-01 (Thu) — Engine pass 12:13 ET → REAL TRADE OPENED (T-2026-0006 HL) + PAPER PASS
Tape stabilized off the 11:13 lows (SPY -0.28%/760.47 vs -0.37% prior; QQQ -0.25%) — still red but no longer making new
lows. HL emerged as the day's one genuine RS leader: silver/gold miner, GREEN +0.9% against a red tape, printed a new
HOD 17.29 at 10:35 ET on 2x volume, then coiled tightly 17.08-17.29 for ~90 min HOLDING near its highs.
WHY THIS CLEARED THE REAL GATE (and the morning passes did not): (1) RS leader HOLDING near a new HOD, not fading;
(2) GOOD entry location — coil-continuation, not a breakout-tick chase (the VALE fix); (3) counter-cyclical thesis —
HL is a risk-OFF asset, so its RS is DRIVEN by the same flow pressuring equities, which neutralizes the usual
"RS-in-a-downtape fails" lesson (that came from risk-ON names needing broad appetite); (4) affordable 1 share, 0.06%
spread, tiny capped risk. ENTRY long 1 @ 17.1699; stop 16.88 (BELOW day low 16.90, wider than the 17.08 coil base per
the whipsaw lesson) = risk $0.29/1.46%; target 17.75 (2:1). Mandatory GTC stop 6abe876f confirmed live.
STEP B paper: PASS — HL taken REAL (one real position at a time; not duplicating in paper), nothing else is a clean
non-chase long in a red tape. This trade is itself the day's key learning sample: does a counter-cyclical RS leader
hold up in a red-but-stabilizing tape? Manage each pass; breakeven-trail at +1R (17.46); flatten by EOD, never overnight.

## 2026-10-01 (Thu) — Engine pass 1:13 ET → MANAGE HL (hold), PAPER PASS
Position: long 1 HL @ 17.17, stop 16.88 GTC confirmed resting. HL now 17.075 (unrealized ≈ −$0.10 / −0.33R; MFE +0.05
to 17.22, MAE −0.11 to 17.06). Tape RECOVERED toward flat: SPY 761.93 (−0.09%, up from −0.28% at 12:13), QQQ −0.04%.
KEY OBSERVATION: as equities recovered (risk-off easing), HL's precious-metals bid FADED — it's now drifting below a
recovering tape, so the "RS leader" edge has weakened. This is the counter-cyclical thesis working in reverse (the exact
risk flagged in the snapshot devil's-advocate: if risk-off flips to risk-on, gold gives back its bid). DECISION: HOLD.
My written exit trigger ("SPY new lows AND HL loses the 17.08 coil") is NOT met — SPY recovered, HL is sitting ON the
17.06 support, not decisively through it. Tightening the stop now would require moving ABOVE the day low 16.90 into
whipsaw range — violating the whipsaw lesson. So keep the whipsaw-safe 16.88 stop (risk tiny/capped) and cut next pass
only if HL decisively loses 17.00 or keeps lagging. No second position (one real at a time). STEP B paper: PASS (real
position open; tape soft, HL fading — no clean new long). Flatten HL by EOD regardless; never overnight.

## 2026-10-01 (Thu) — Engine pass 2:12 ET → CLOSED HL (T-2026-0006), thesis-invalidation exit
Entry 17.1699 (11:16 ET) → exit 17.0601 (2:13 ET). **−$0.11 / −0.38R. GOOD DECISION + LOSS (thesis invalidation).**
MFE +0.10 (17.27, ~11:30 ET), MAE −0.20 (16.97) — never near the 16.88 stop. Account 19.79 → 19.68, FLAT.
WHY EXITED EARLY (not stopped): the whole thesis was "RS leader." By 2:12 the tape had RECOVERED to GREEN (SPY +0.05%,
QQQ +0.16%) and HL — the supposed leader — was sitting near its lows, lagging. It became a laggard in BOTH regimes: the
risk-off gold bid that justified it evaporated when risk-off eased, and it failed to join the risk-on bounce. When the
reason for a trade disappears, exit; cutting at −0.38R preserved ~0.6R of the risk budget vs donating it to a dead setup.
Cancelled the GTC stop FIRST (freed the share), then sold — clean, no naked orders.
LESSON (new sample, loss_class THESIS_INVALIDATION): a COUNTER-CYCLICAL RS leader is only a leader while the risk-off
flow feeding it persists. HL's edge was real at 12:13 (green vs red tape) but regime-contingent; when the tape reverted
to green, the edge inverted within ~90 min. Takeaways: (1) counter-cyclical RS has a SHORT half-life — it must be managed
tighter and exited the moment the driving regime flips, not given full-stop room; (2) the entry was still defensible
(best setup of the day, good non-chase location), and disciplined early-exit turned a potential −1R into −0.38R — the
management, not the entry, was the win here. Lifetime real: F −0.11, AAL +0.05, CLF +0.05, VALE −0.20, HL −0.11 = −0.32
(2W/3L). No revenge; one real position at a time respected. Flatten-by-EOD moot (already flat).

## 2026-10-01 (Thu) — Engine pass 3:13 ET → REAL PASS + PAPER PASS (post-HL, late day)
Account FLAT $19.68, clean (HL closed at 2:13). Day completed a full V-REVERSAL: red morning -> green afternoon.
SPY 764.50 (+0.25%), QQQ 742.68 (+0.39%). Leaders now: SNAP +3.1% (clear RS leader, new HOD), SOFI +1.0%, F +1.3%.
HL still lagging at 17.075 — confirms the thesis-invalidation exit was correct (it never rejoined). STEP A real: PASS —
it's 3:13pm, ~47 min to the mandatory EOD flatten, so no runway for a 2:1 to mature; entering SNAP here would be a
late-day chase (O003), and I've already taken my one real trade today. STEP B paper: PASS — same late-day logic; EOD
flatten in <1hr makes a new entry low-value. NOTE for tomorrow's watchlist: SNAP showed strong RS on the reversal
(+3.1%, leading a green tape) — track it. Next pass (~20:12Z) = post-close EOD wrap.

## 2026-10-02 (Fri) — Engine pass 10:13 ET → REAL PASS + PAPER PASS
Account FLAT $19.68. Tape still risk-on (SPY +0.98%, QQQ +1.48%) but affordable names remain choppy/mixed post-gap-fade:
HL +1.35% (near OR high but gold = thesis-incoherent in risk-on + recency/revenge caution after yesterday's HL loss),
NCLH +1.2% / SNAP +0.6% (green but below OR highs), SOFI +0.5% (faded), AAL +0.3% (flat), RIVN -3.0% (still collapsing),
F red, MARA +7.6% (extended, O002). No clean pullback-and-hold reclaim triggered anywhere. STEP A real: PASS. STEP B
paper: PASS — green index but no non-chase affordable setup; not forcing volume. Watching SNAP (reclaim of 5.72 OR high)
and NCLH (reclaim of 15.00) for a later trigger. Jobs-day gap that faded at the stock level = exactly the "index risk-on
≠ tradable affordable setup" pattern.

## 2026-10-02 (Fri) — Engine pass 11:13 ET → REAL PASS + PAPER PASS
Account FLAT $19.68. Index gap now COOLING: SPY 768.45 (+0.58%, off +1.0%), QQQ 749.22 (+0.97%, off +1.48%) — giving
back ~half the gap. O002 VALIDATION: MARA collapsed +8% -> +1.9% (12.24 -> 11.42), textbook spike-and-fade — chasing it
at the open (as tempting as +8% looked) would have been a loss; the no-spike-chase rule paid off. SNAP 5.73 (right AT its
5.72 OR high, not clearly held above) and NCLH 14.945 (near 15.00 OR high) are the only two coiling near breakout levels,
but a fresh breakout into a COOLING tape is lower-odds (standing lesson: fading tape -> favor pullbacks, don't chase
breakouts). SOFI/AAL now red; HL faded to +0.5%. STEP A real: PASS. STEP B paper: PASS — no clean hold-above reclaim +
cooling tape = not chasing. Watching SNAP/NCLH for a decisive hold-above; otherwise a quiet jobs-day for the book.

## 2026-10-02 (Fri) — Engine pass 12:13 ET → REAL TRADE OPENED (T-2026-0007 NCLH) + PAPER PASS
After passing the gap-and-faders all morning, NCLH set up the cleanest break-and-hold of the week: gapped +2.7%, faded to
14.58 at the open (shook out chasers), then RECOVERED, reclaimed its 15.00 OR high at ~11:40 ET and HELD 15.00-15.07 for
30+ min. RS leader +2.8% vs SPY +0.76% — and critically a RISK-ON name in a RISK-ON tape (thesis-coherent, unlike 10/1's
counter-cyclical HL). Entry long 1 @ 15.0299 on a PULLBACK to the 15.00 reclaim level (good entry location, the VALE fix),
stop 14.85 (below the 14.95-15.00 hold base), target 15.39 (2:1), risk $0.18/0.91%. GTC stop 6abfd8a5 confirmed.
WHY THIS CLEARED THE GATE when the 9:47/10:13/11:13 passes didn't: the morning names CHASED their gaps and faded; NCLH
instead round-tripped and RECLAIMED on real demand, holding the level — a confirmed break-and-hold, not a gap chase, with
a pullback entry. Manage each pass; breakeven-trail at +1R (15.21); exit on a decisive loss of 15.00 + index roll (HL
lesson); flatten by EOD, never overnight. STEP B paper: PASS (real position open; one at a time).

## 2026-10-02 (Fri) — Engine pass 1:13 ET → MANAGE NCLH (hold), PAPER PASS
Position: long 1 NCLH @ 15.03, stop 14.85 GTC confirmed resting. NCLH 15.045 (~flat, +$0.02). Since entry it's
consolidated tightly 14.97-15.07, HOLDING the 15.00 reclaim level (dips to 14.975-14.985 bought back) — thesis intact,
basing above the reclaim, just no next leg yet. Tape still risk-on (SPY +0.71%, QQQ +0.98%). DECISION: HOLD, stop
unchanged 14.85. Not near +1R (15.21) so no breakeven move yet. Behaving as a continuation setup should (consolidate
above reclaim). STEP B paper: PASS (one real position at a time). Flatten by EOD; exit early only if it decisively loses
15.00 AND the index rolls.

## 2026-10-02 (Fri) — Engine pass 2:13 ET → MANAGE NCLH (hold), PAPER PASS
Position: long 1 NCLH @ 15.03, stop 14.85 GTC resting. NCLH 14.985 (unrealized −$0.045 / −0.25R). Chopped 14.91-15.09
for 2h (one dip to 14.91 recovered, one push to 15.09 faded), now just below 15.00 — dead money intraday BUT still +2.4%
on the day vs SPY +0.66%, i.e. still a day-leader consolidating gains, not breaking down. Tape firm (SPY +0.66%, QQQ
+0.93%). Exit trigger (decisive loss of 15.00 AND index roll) NOT met → HOLD, stop unchanged 14.85 (no tightening into
the chop, whipsaw risk). STEP B paper: PASS (one real position). NOTE: next pass (3:13pm) is the LAST in-market window to
flatten before the 4pm close — will exit NCLH there if not already stopped/targeted (never hold the $20 overnight).

## 2026-10-02 (Fri) — Engine pass 3:13 ET → CLOSED NCLH (T-2026-0007), EOD flatten (scratch)
Entry 15.0299 (12:15 ET) → exit 15.0001 (3:13 ET). **−$0.03 / −0.17R. GOOD DECISION + SCRATCH.** MFE +0.06 (15.09),
MAE −0.12 (14.91) — never near the 14.85 stop. Account 19.68 → 19.65, FLAT.
WHY FLATTENED (not stopped/targeted): it chopped 14.91-15.09 for 3 hours, held its 15.00 reclaim level and stayed a
day-leader (+2.4% vs SPY), but the intraday CONTINUATION never came. This was the last in-market window before the 4pm
close, so per the never-overnight rule I flattened near breakeven rather than carry risk into the close/overnight.
Cancelled the GTC stop first (freed the share), then sold — clean, no naked orders.
ASSESSMENT: the ENTRY was the best of the week (genuine reclaim-and-hold, RS leader, risk-on name in risk-on tape, good
pullback location). It simply didn't follow through — not every valid setup pays. Outcome is a near-zero scratch, which is
exactly what good risk management produces on a no-follow-through trade: tiny defined risk, held the level, exited flat.
NEW DATAPOINT (loss_class EOD_FLATTEN / NO_FOLLOWTHROUGH): a clean setup that holds its level but doesn't advance within
the session is a scratch, not a loss to agonize over — the edge is in taking many such setups; this one just didn't run.
Lifetime real: F −0.11, AAL +0.05, CLF +0.05, VALE −0.20, HL −0.11, NCLH −0.03 = −$0.35 (2W/4L; losses all small/capped).
Final day totals + official closes to be logged at the post-close (~20:12Z) pass.

## 2026-10-02 (Fri) — Engine pass 3:13 ET (19:12Z) → confirmation only (already flat)
This engine notification (19:12Z) coincided with the NCLH flatten already executed this same window (sold 15.0001 at
19:12:56Z). Reconfirmed: account FLAT, 0 positions, 0 open orders, $19.65. NCLH 15.04 just after exit (+$0.04 vs fill —
immaterial, EOD flatten was mandatory regardless). STEP A real: PASS (flat, ~3:15pm late day, no re-entry after the day's
trade). STEP B paper: PASS (no opens). No new action. Full EOD wrap + official closes at the post-close ~20:12Z pass.

## 2026-10-05 (Mon) — Engine pass 10:13 ET → REAL PASS + PAPER OPEN (P-2026-0025 SOFI)
Account FLAT $19.65. Tape firmed to mild green (SPY +0.30%, QQQ +0.36%). Gappers stayed faded (HL -1.3%, VALE choppy
14.30). Two RS leaders emerged: SOFI +2.3% (16.13) and SNAP +2.5% (5.72, low-priced/whippy). SOFI structure = clean
staircase, built a 15.87-16.00 base and broke to new HOD 16.14 on its biggest-vol bar.
STEP A (real): PASS — entry at 16.12 is on the breakout bar AT the HOD = the extended location the VALE lesson flags;
real waits for a pullback-to-16.00-hold or a base-above-16.00 re-break (the better entry). SOFI is the #1 live candidate.
STEP B (paper): OPENED SOFI long 16.13, stop 15.84 (below base), target 16.71 (2:1), 137 sim shares — taken to TEST the
entry-location question (does a base-break-at-HOD entry pay, or does waiting for the pullback win?). Zero real risk; useful
datapoint either way. Manage each pass; flatten EOD. This is the clean split: paper takes the valid-but-marginal-location
setup for learning volume; real holds out for the ideal entry.

## 2026-10-05 (Mon) — Engine pass 11:13 ET → REAL PASS + MANAGE PAPER SOFI (open)
Real FLAT $19.65. Tape still firming green (SPY +0.35%, QQQ +0.47%). PAPER SOFI (P-0025, entry 16.13): popped to HOD 16.19
right after entry then FADED and chopped 15.93-16.19 for an hour; now 16.055 (unrealized ~−$0.08; MFE +0.06 to 16.19, MAE
−0.20 to 15.93). Did NOT hit target 16.71 or stop 15.84 → stays OPEN. EARLY DATAPOINT: buying the base-break AT THE HOD
stalled into a pullback/range immediately — vindicates the real-side "wait for the pullback" discipline (the 15.93 pullback,
which held above the 15.87 base, was the better entry location). STEP A real: PASS — SOFI stalled into a 15.93-16.19 range;
16.06 is mid-range = neither a break-and-hold (want 16.19+) nor a clean pullback-hold (want 15.93). No trigger. Still the
#1 watch for a range resolution. STEP B: manage SOFI paper (open); no new paper (SNAP faded to 5.655, nothing else clean).
Flatten paper at EOD.

## 2026-10-05 (Mon) — Engine pass 12:13 ET → REAL PASS + CLOSED PAPER SOFI (P-0025, entry-location test)
Real FLAT $19.65, tape still green (SPY +0.46%, QQQ +0.50%) — but SOFI did NOT follow: it topped 16.19 right after the
16.13 HOD entry, stalled into a 15.93-16.19 range, then lost its 15.87-16.00 base and drifted to 15.975 WHILE SPY made
new highs = lost its RS. CLOSED paper SOFI at 15.975 = −$21.24 / −0.53R (exited on the base-break-down, thesis-break
discipline, not waiting for the 15.84 stop). MFE +0.06 (16.19), MAE −0.20.
KEY LEARNING (the whole point of the P-0025 experiment): buying the base-break AT THE HOD did NOT pay — it topped
immediately and bled. This directly CONFIRMS the real-side discipline of PASSING that entry (real stayed flat = correct).
The VALE "don't buy the breakout bar near HOD; wait for the pullback/hold" lesson is now re-validated in a controlled paper
test. STEP A real: PASS (SOFI setup failed; no other clean setup — morning movers all faded). STEP B: SOFI closed; no new
paper (nothing clean, SOFI failing). Paper lifetime now 25 closed. Account FLAT, capital intact.

## 2026-10-05 (Mon) — Engine pass 1:13 ET → REAL PASS + PAPER PASS
Account FLAT $19.65, no open paper (SOFI closed). Index grinding to new highs (SPY 774.14 +0.58%, QQQ 754.35 +0.64%) but
the AFFORDABLE universe is lagging/mixed: SOFI 15.98 (failed base), NCLH 14.925 (-1.4%, red), AAL 12.865 (-0.6% red),
RIVN flat, VALE 14.11 (+2.5% but choppy off highs); only SNAP +2.3% holds green (low-priced/whippy, no clean setup).
Recurring structural read: the strength is in the index/mega-caps, not in clean affordable names — the day's tradable
RS leaders keep being unaffordable or failing. STEP A real: PASS (no affordable non-chase setup). STEP B paper: PASS
(nothing clean; SNAP too whippy). Capital intact, no forcing. All-day engine keeps watching; EOD wrap at the post-close pass.

## 2026-10-05 (Mon) — Engine pass 2:13 ET → REAL PASS + PAPER PASS
FLAT $19.65, no open paper. Unchanged from 1:13pm: index new highs (SPY 774.71 +0.66%, QQQ +0.71%), affordable universe
lagging/choppy (SOFI ~16 failed base, NCLH 14.93 -1.4%, AAL -0.4%, VALE/SNAP choppy). No clean affordable non-chase
setup. STEP A PASS, STEP B PASS. Capital intact. EOD wrap at post-close pass.

## 2026-10-05 (Mon) — Engine pass 3:13 ET → REAL PASS + PAPER PASS (last in-market pass)
FLAT $19.65, no position. Index closing strong at new highs (SPY 775.89 +0.81%, QQQ 756.31 +0.90%) but affordable names
stayed choppy all day (SOFI 16.05, SNAP 5.675, VALE 14.33 — none a clean setup); late day (O003). PASS both. No flatten
needed (flat). Clean no-real-trade day — correct given no affordable non-chase setup materialized. EOD wrap at post-close.

---
## 2026-10-06 (Tue) — Intraday engine pass ~10:14 ET (14:14Z)

**Regime:** RISK-ON at new highs. SPY 780.19 (+0.69%), QQQ 761.21 (+0.66%). Clear risk-on rotation: nuclear/uranium theme LEADING (UEC +6.1%, SMR +6.8%, OKLO +7.5%, CCJ +5.3%), cruise strong (NCLH +3.8%, CCL +3.4%), while metals/gold miners are RED (GOLD/AG/KGC/FCX) — money rotating out of defensives into high-beta growth themes.

**STEP A — REAL $20: PASS.** Reconciled FLAT ($19.65, 0/0). Scanned the affordable universe:
- **NCLH** (+3.8%, 15.43) — the #1 real watch — already made its vertical move in the first 15 min (spiked to HOD 15.6103 at 9:45 ET) and has since DRIFTED lower on FADING volume (15.56→15.42→15.46→15.43), now mid/low of its range. Buying here = chasing an extended name mid-consolidation (violates O002 + entry-location rule). No clean trigger. Would need a reclaim-and-hold of 15.56–15.61 on volume, OR a pullback-hold ~15.30 with a reclaim. Still #1 watch.
- **AAL** (now +1.7%, 13.07) — faded from its 9:47 high, rolling over: last bar broke the 13.11–13.16 base to 13.04 on rising volume (665k). Failed-breakout fade. PASS.
- **UEC/SMR/OKLO** — leading but >$8–$38 is fine affordability-wise for UEC/SMR; however these are better expressed in paper (theme concentration + first-pop-then-grind; the real $20 wants ONE clean, affordable, high-conviction setup, not a thematic basket). On the real side I stay patient.
- CLF (+1.2%, faded gapper stabilizing), VALE (red), SOFI (in-line), RIOT/F/HBAN/RIG — no clean affordable non-chase setup.
→ **PASS. Zero-forced-trade discipline holds.** NCLH = #1 watch for the next pass.

**STEP B — PAPER: opened 4 longs** (theme-coherent book across the 2 leading themes; tests whether mid-morning theme-leader continuations follow through on a risk-on new-high day):
- **P-2026-0026 UEC** 9.92, stop 9.68, tgt 10.40 (166sh) — uranium leader, clean base-break to new HOD on 2x vol.
- **P-2026-0027 SMR** 8.20, stop 8.05, tgt 8.50 (266sh) — nuclear, higher-lows continuation toward HOD after morning shakeout.
- **P-2026-0028 OKLO** 38.65, stop 38.05, tgt 39.85 (66sh) — nuclear, same HL recovery structure.
- **P-2026-0029 CCL** 26.43, stop 26.15, tgt 26.99 (142sh) — cruise RS, coil near HOD (B-grade: vol fading into the coil).
All: stop-first, ≥2:1, wider-than-immediate-base stops per whipsaw lesson. PASSED on IONQ (quantum, lower highs/fading), NCLH (drift/fading vol — same read as real side), SOFI (in-line RS), LCID (thin), RIOT/AAL (rolling over).

**Note:** 0 open paper trades carried into this pass (P-0025 closed 10/5). These 4 are the only open paper positions now.
