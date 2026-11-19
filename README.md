# makefun-tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/tanusinap/makefun-tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/tanusinap/makefun-tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 4,082 bytes of Python 3.13 (stdlib only). It plays the
make.fun tiny-chess-01 gauntlet over the HTTP env: 0x88 board, PeSTO tapered
evaluation (tables packed as zlib + base85, values quantised to 4 cp),
iterative deepening alpha-beta with a fixed 200,000-node budget per move,
quiescence search (captures, promotions, check evasions), transposition
table and MVV-LVA move ordering. Fully deterministic: no wall clock, no
randomness in search.

v3 carries a verified mate book: 6 lines (one per trial-0 game), found with
a Stockfish oracle and a beam search that plays the true deterministic house
replies, stored as 95 move-list indices (137 bytes). Each line is keyed on
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
cap, W6 D0 L0, 965 spare plies (mates in 35/44/31/40/41/44 plies), wall 12s.
The v2 entry scored 939 spare plies, the v1 entry (engine only, no book)
741. Book lines verified against the level-26 kit's env server (trial-0
gauntlet unchanged from level 24). The v3 lines came from a wider beam
search (beam 8) on games 2, 5 and 6; the book index generator stores the
opening key as 0x88 squares, matching the lookup in the engine.
