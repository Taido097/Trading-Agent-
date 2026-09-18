# LESSONS.md — Level 2 → Level 3 Learning

> **Three memory levels.** Keep them separate:
> - **Level 1 — FACTS:** what happened (raw trade history in `data/`). Never rewritten.
> - **Level 2 — OBSERVATIONS:** possible patterns, not yet rules. They live here.
> - **Level 3 — VALIDATED RULES:** promoted to `TRADING_PLAYBOOK.md` only after
>   sufficient evidence (see `design/LEARNING_PIPELINE.md`).
>
> Do not create a permanent rule from one trade. Avoid overfitting.

---

## Open Observations (Level 2)

| ID | Date | Observation | Support (n) | Status | Next step |
| -- | ---- | ----------- | ----------- | ------ | --------- |
| O001 | 2026-09-16 | Trading on command with no setup (T-2026-0001, F) produced a small loss (−0.77R); a name that is red while the market is green (relative weakness) is a poor long. | 1 | observation | Only enter on a documented setup; treat relative weakness as a long-disqualifier |
| O002 | 2026-09-18 | On fast momentum names a passive limit AT the breakout level often misses (MARA: limit 12.36 missed as it went 12.33→12.48 in ~90s). Missing beats chasing. | 1 | observation | Use a marketable-limit slightly THROUGH the level to catch the break; if missed, do not chase after extension |

Template:
```
### O00X — <observation>
- First noticed:
- Supporting trades (IDs):
- Sample size:
- Confidence stage: observation / repeated / possible-pattern / statistical / backtested
- Counter-evidence:
- Decision: keep watching / promote candidate / discard
```

## Promoted to Playbook

_(none yet — links to TRADING_PLAYBOOK.md rules will appear here)_

## Discarded Observations (kept for the record)

_(none yet — patterns that failed validation are archived, not deleted)_
