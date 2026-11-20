# tiny-chess-01 v3

`main.py` = LZMA-packed `engine.py` (made with `makefun compress`). Run:
`MAKEFUN_ENV_URL=<env> python3 -P -s main.py`

Design (sunfish-style 120-square board, rewritten):
- negamax alpha-beta + PVS, transposition table, killer + history ordering
- late-move reductions, null move, quiescence on captures
- incremental make/unmake (v3 speed fix: no board rebuild per move)
- iterative deepening on a node budget (NB=80000 default; ~75k nodes/s after
  the v3 speed fix, max move ~1.0 s at NB=100k, no games lost on time)
- mate/stalemate detection, repetition = draw (from the env's move list)
- king PST switches to an endgame table when material is low

Local practice (6 games per trial, kit scorer):
- v2 NB=50000: 1451 / 1654 / 1545 (mean ~1550)
- v3d NB=100k: 1654 / 2112 / 1451 (mean ~1739, best 2112 = perfect 6-0)
- v3f NB=80k: 1654 / 1451 / 2112 (mean ~1739, best 2112 = perfect 6-0)
- Mean still below rank 1 (2,110), but the engine has hit the 2,112 cap twice.
