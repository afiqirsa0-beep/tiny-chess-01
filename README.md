# tiny-chess-01 v4

`main.py` = LZMA-packed `engine.py` (`makefun compress`). Run: `MAKEFUN_ENV_URL=<env> python3 -P -s main.py`

Design (sunfish-style 120-square board): negamax alpha-beta + PVS, TT, killer+history
ordering, LMR, null move, capture quiescence, mate/stalemate detection, repetition as draw,
endgame king PST. Iterative deepening to a node budget NB=100000 (hard abort at 2x),
no clock: deterministic. Unloaded ~86k nodes/s, ~1.5 s/move, max ~2.7 s solo.

Local practice (6 games/trial; 3 kit instances + 3 self-drawn with the kit generator),
NB=100k, no time losses: 1654 / 1809 / 1545 / 1545 / 1809 / 2112.
Mean 1746, best 2112, worst 1545. Below rank 1 (2,110).
Note: run local trials at most 2 in parallel; 3 in parallel starves the bot and loses on time.
