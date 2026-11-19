# makefun-tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/tanusinap/makefun-tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/tanusinap/makefun-tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 4,082 bytes of Python 3.13 (stdlib only). It plays the
make.fun tiny-chess-01 gauntlet over the HTTP env: 0x88 board, PeSTO tapered
evaluation (tables packed as zlib + base85), iterative deepening alpha-beta
with a fixed 200,000-node budget per move, quiescence search (captures,
promotions, check evasions), transposition table, MVV-LVA move ordering,
late-move reductions and null-move pruning. Fully deterministic: no wall
clock, no randomness in search.

`main.py` is an lzma + base85 packed payload with a short unpacker; the
unpacked source is a golfed engine of the same logic (see the dev version
used to build and verify it). Run it with `MAKEFUN_ENV_URL` set to the env:

```sh
python3 -P -s main.py
```

Practice results (local kit trials, trial-0): the full-featured dev engine
hits the 2112 Elo cap at 200k nodes (W6 D0 L0, 659 spare plies, wall
1048s; 1654 at 120k nodes). The packed 4 KB entry (this repo) also hits
the 2112 cap on trial-0: W6 D0 L0, 741 spare plies, wall 1114s.
