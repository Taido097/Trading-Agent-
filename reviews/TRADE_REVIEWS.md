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
