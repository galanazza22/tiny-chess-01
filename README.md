# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/galanazza22/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/galanazza22/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in at most 4,096 bytes of Python, written for [make.fun's tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01): it plays a gauntlet of eight house engines, from alpha-beta depth 2 up to a 2,000,000-node search, and is rated by Elo against their calibrated anchors.

## How it plays

`main.py` is the whole engine (Python 3.13, standard library only). It talks to the trial env over HTTP (`POST /game`, `POST /move`), then:

- 0x88 board, pseudo-legal move generation with a legality filter, castling, en passant and all promotions.
- Negamax alpha-beta with a transposition table, MVV-LVA + killer move ordering, null-move pruning, and a capture/check-evasion quiescence search.
- Evaluation: material plus piece-square terms (central pawns gain by advancing, flank pawns do not; knights and bishops gain by developing toward the centre; rooks gain on the 7th rank) and a bishop-pair bonus.
- Search is to a fixed node budget per move (30,000 nodes, 15,000 late in long games) — never a clock — so a replay plays the same moves. Repetitions score as draws.

The readable source is `source.py` (kept beside the entry, uncommitted); `main.py` is the `makefun compress` packing of it, unchanged.

<sub>Entered on [make.fun](https://make.fun/?ref=s0zdek06&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
