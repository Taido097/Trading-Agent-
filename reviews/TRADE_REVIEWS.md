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
