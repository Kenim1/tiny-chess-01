# tiny-chess-01

[![make.fun](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/kenim1/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/kenim1/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01)

A compact alpha-beta chess engine in 4 KB of Python, built for the
[make.fun](https://make.fun/bounty/tiny-chess-01) bounty
"Build the strongest chess engine in 4 KB of Python".

## The entry

`main.py` is the whole engine: **3,473 bytes**, Python 3.13 stdlib only.
It is a packed entrypoint produced by the kit's own `makefun compress`
from the readable source `source.py` (kept beside this repo; the bundle
sends it along, never redacted). It talks HTTP to the competition env at
`$MAKEFUN_ENV_URL` and plays the house gauntlet.

## How it plays

- 0x88 board, Zobrist hashing, transposition table.
- Negamax + alpha-beta with principal-variation search, null-move pruning
  (R=3) and late-move reductions.
- Killer moves + history ordering, quiescence search on captures.
- Evaluation: material, formula piece-square tables, bishop pair, and a
  tapered king safety term.
- A **fixed node budget of 80,000 nodes per move** (iterative deepening),
  never a clock — so the play is fully deterministic and replays
  move-for-move.

## Local result

Practice trial-0 (6 games vs the first 6 gauntlet rungs, anchors 855–1596)
with the same node budget: **3 wins, 2 draws, 1 loss — about Elo 1,451**,
comfortably above the 1,154 practice floor.

## License

MIT. See [LICENSE](LICENSE).
