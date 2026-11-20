# tiny-chess-01 v2

`main.py` = LZMA-packed `engine.py` (made with `makefun compress`). Run:
`MAKEFUN_ENV_URL=<env> python3 -P -s main.py`

Design (sunfish-style 120-square board, rewritten):
- negamax alpha-beta + PVS, transposition table, killer + history ordering
- late-move reductions, null move, quiescence on captures
- iterative deepening on a node budget (NB=50000, about 1.3 s/move at ~38k nodes/s)
  with a hard abort at 3x; NB=100000 loses on time, so keep it near 50k
- mate/stalemate detection, repetition = draw (from the env's move list)
- king PST switches to an endgame table when material is low

Local practice (6 games per trial, kit scorer): NB=24000 mean ~1335;
NB=50000: 1451 / 1654 / 1545 (mean ~1550). Below rank 1 (2,110).
