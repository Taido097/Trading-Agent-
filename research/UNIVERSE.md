# UNIVERSE.md — Micro-Live Screening Universe

Purpose: widen the daily net for the Opening-Range Breakout while keeping the
**same** quality bar. Each morning the prep step pulls quotes for this candidate
pool (plus, when available, a scanner sweep for sub-$19 high-relative-volume
gainers), then narrows to that day's watchlist by the filters below.

## Hard screen (a name must pass ALL to reach the watchlist)
- **Affordable:** 1 whole share ≤ ~$19 (must fit in real buying power with buffer,
  so a broker-held whole-share stop is possible). RISK_RULES §9.
- **Liquid:** high average volume; deep book.
- **Tight spread:** bid/ask spread small in $ and % (roughly ≤ ~0.3–0.5%).
- **Not too low-priced:** avoid names so cheap (≲ $4) that a sensible stop is
  smaller than the spread (NIO/GRAB/PLUG/LCID flagged for this).

## Then rank by
- **Relative strength** vs SPY/QQQ (up more than the market), and
- a clean, tradeable opening range (not a spiky/illiquid tape).

## Candidate pool (screened live each morning; prices drift, so affordability is
re-checked daily — a name over ~$19 that day is simply skipped)

| Sector | Tickers |
| ------ | ------- |
| Fintech / tech | SOFI, SNAP, CHPT, GRAB* |
| EV / auto | F, RIVN, LCID*, NIO* |
| Airlines / travel | AAL, CCL†, NCLH† |
| Miners / materials | VALE, CLF, KGC, HL, BTG, MARA, RIOT† |
| Financials | HBAN, KEY, RF |
| Energy | RIG |
| Media / staples | SIRI, AMCR, KVUE |

\* low-priced — usually fails the "not too low-priced" filter; kept for reference.
† often > $19 — included only on days their price fits the budget.

## Notes
- This is a screening list, not a buy list. Most names PASS most days.
- The pool is expanded/curated over time; changes are logged in SYSTEM_CHANGELOG.
- A market scanner (Robin scan tools) may supplement this with fresh sub-$19
  relative-strength movers each morning.
