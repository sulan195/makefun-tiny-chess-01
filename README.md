# makefun-tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/sulan195/makefun-tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/sulan195/makefun-tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An entry for make.fun's **tiny-chess-01**: the strongest chess engine that
fits in 4,096 bytes of Python. `main.py` is the whole engine — it unpacks an
lzma-compressed payload (the rules count the payload and the unpacker
together) and plays the house gauntlet through the env at `MAKEFUN_ENV_URL`.

How it plays:

- 0x88 board, fully legal move generation (castling, en passant, promotions)
- Negamax alpha-beta with a transposition table, PVS and late-move
  reductions, iterative deepening
- Quiescence search over captures and promotions, with check evasions
- Null-move pruning and MVV-LVA move ordering
- Tapered evaluation: material plus piece-square tables, with a dedicated
  king table for the endgame
- Repetition and the fifty-move rule score as draws inside the search

Determinism: the search runs to a **fixed node budget per move, never to a
clock**, and uses no randomness, so a replayed trial makes exactly the same
moves. The budget is 20,000 nodes a move: the slowest move measured on hard
positions takes about a second on one CPU, far inside the env's 10-second
limit, and the whole trial finishes in a few minutes of its 1,800-second
wall. (An earlier build searched 60,000 nodes a move; on the grading
container's single CPU its longest moves ran too close to the limit and its
practice grade fell under the floor, so the budget was cut and the search
made stronger per node instead.)

## Run it

```sh
node cli/makefun.mjs grade-local --kit . --bot <this repository> --driver docker
```

(from inside the competition's unpacked dev kit)

## License

MIT — see `LICENSE`.

---

<sub>Entered on [make.fun](https://make.fun/?ref=mmtmfkx5&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
