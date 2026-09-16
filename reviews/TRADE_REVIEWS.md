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
Result: OPEN (position live, protected).
Classification: PENDING until exit. **Important:** this was an OWNER-DIRECTED
  trade, not a validated setup — F was flat on a green day (relative weakness),
  no ORB, no edge. Per rule 19, a win here would NOT be proof the process works,
  and per rule 20 a loss would be expected variance of a no-edge entry. Do not
  let the outcome update strategy confidence.
Process notes:
- Rule-2 tension acknowledged (traded without an edge) — justified only by
  explicit owner override on fully-at-risk micro capital; logged transparently.
- Risk control HELD: invalidation defined first, sized from risk, mandatory
  broker-held protective stop attached immediately after fill.
- Pipeline validated end-to-end: reconcile → review → place → fill → stop →
  journal. This is the real value of the trade.
Actions at exit: classify GOOD/BAD × WIN/LOSS, record slippage/MFE/MAE, update
  memory. No strategy change from this single owner-directed trade.
