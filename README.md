# tiny-chess-01 v9

`main.py` = LZMA-packed `engine.py` (`makefun compress`, 2,715 bytes). Run: `MAKEFUN_ENV_URL=<env> python3 -P -s main.py`

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
