[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/jacky01234567890/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/jacky01234567890/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# tiny-chess-01 — a 4 KB chess engine

A compact, original chess engine in a single `main.py` (3,524 bytes, Python
standard library only). It plays the house gauntlet over HTTP
(`$MAKEFUN_ENV_URL`, `POST /game` and `/move`) with a deterministic,
fixed-node search — no wall clock, no randomness — so replays are
move-identical.

## Engine

- **Board:** 0x88 (128 squares), signed-int pieces, incremental evaluation.
- **Eval:** material (P100 N320 B330 R500 Q900) + formula piece-square
  tables (house-style, middlegame/endgame king interpolation by phase) +
  bishop-pair bonus.
- **Search:** negamax with alpha-beta, iterative deepening to a fixed
  50,000-node budget, quiescence (captures, promotions, and replies to
  check), killer moves, history heuristic, and MVV-LVA capture ordering.
- **Moves:** full legal move generation (castling, en passant, promotions),
  verified against standard perft positions.

`main.py` is an LZMA-compressed payload stored as a latin-1 string literal
with a small unpacker (both count toward the 4,096-byte limit); the
decompressed source is original MIT code.
