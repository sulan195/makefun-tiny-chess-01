# Tiny Chess — a chess engine in 4 KB of Python

![Competition](https://img.shields.io/badge/competition-tiny--chess--01-blue)
![Runtime](https://img.shields.io/badge/python-3.13-green)
![Size](https://img.shields.io/badge/main.py-4096%20bytes-orange)

An entry for make.fun's **tiny-chess-01**: the strongest chess engine that
fits in 4,096 bytes of Python. `main.py` is the whole engine — it unpacks an
lzma-compressed payload (the rules count the payload and the unpacker
together) and plays the house gauntlet through the env at `MAKEFUN_ENV_URL`.

## How it plays

- 0x88 board, fully legal move generation (castling, en passant, promotions)
- Negamax alpha-beta with a transposition table and PVS, iterative deepening
- Quiescence search over captures and promotions, with check evasions
- Null-move pruning and MVV-LVA move ordering
- Tapered evaluation: material plus piece-square tables and the bishop pair
- Repetition and the fifty-move rule score as draws inside the search

## Determinism

The search runs to a **fixed node budget per move, never to a clock**, and
uses no randomness, so a replayed trial makes exactly the same moves. The
budget is sized to keep every move far inside the env's 10-second limit and
the trial well inside its 1,800-second wall.

## Grade it locally

Download the competition's dev kit, unpack it, and from inside it run:

    node cli/makefun.mjs grade-local --kit . --bot <this repository> --driver docker

## License

MIT — see `LICENSE`.
