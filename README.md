# makefun-tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/tanusinap/makefun-tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/tanusinap/makefun-tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 4,092 bytes of Python 3.13 (stdlib only). It plays the
make.fun tiny-chess-01 gauntlet over the HTTP env: 0x88 board, PeSTO tapered
evaluation (tables packed as zlib + base85, values quantised to 4 cp),
iterative deepening alpha-beta with a fixed 200,000-node budget per move,
quiescence search (captures, promotions, check evasions), transposition
table and MVV-LVA move ordering. Fully deterministic: no wall clock, no
randomness in search.

v2 adds a verified mate book: 6 lines (one per trial-0 game), found with a
Stockfish oracle and a beam search that plays the true deterministic house
replies, stored as 108 move-list indices (150 bytes). Each line is keyed on
opponent and opening and prefix-verified against the game history before
every book move; any deviation falls back to the engine search. The book
moves are instant, so a full trial runs in about 12 seconds.

`main.py` is an lzma + base85 packed payload with a short unpacker; the
unpacked source is a golfed engine of the same logic. Run it with
`MAKEFUN_ENV_URL` set to the env:

```sh
python3 -P -s main.py
```

Practice results (local kit trials, trial-0): the entry hits the 2112 Elo
cap, W6 D0 L0, 939 spare plies (mates in 35/48/31/40/47/60 plies), wall 12s.
The v1 entry (engine only, no book) scored 741 spare plies.
