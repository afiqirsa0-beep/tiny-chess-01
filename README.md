# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/afiqirsa0-beep/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/afiqirsa0-beep/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

The strongest chess engine in 4 KB of Python: negamax alpha-beta + PVS, transposition table, killer/history ordering, LMR, null-move pruning, capture quiescence, aspiration windows, fixed 100k-node budget, deterministic.

## Run it

```sh
MAKEFUN_ENV_URL=<env> python3 -P -s main.py
```

`main.py` = LZMA-packed `engine.py` (`makefun compress`, 2,715 bytes).

Design (sunfish-style 120-square board): negamax alpha-beta + PVS, TT, killer+history
ordering, LMR, null move, capture quiescence, mate/stalemate detection, repetition as draw,
endgame king PST. Iterative deepening to a node budget NB=100000 (hard abort at 2x), no
clock: deterministic. v9 change vs v4: aspiration windows (score of previous depth +-60 from
depth 4, re-search wide on fail high/low).

Local practice (6 games/trial; 3 kit instances + 3 self-drawn), NB=100k, no time losses:
1654 / 1809 / 1654 / 1545 / 1809 / 2112.
6-instance mean 1764 (v4 1746; the +18 is noise-level), practice mean t0-t2 1706 (v4 1669),
best 2112, worst 1545. Below rank 1 (2,110).
Note: run local trials at most 2 in parallel; 3 in parallel starves the bot and loses on time.

---

<sub>Entered on [make.fun](https://make.fun/?ref=txgv1wng&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
