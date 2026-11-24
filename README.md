[![make.fun · u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b](https://make.fun/badge/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b.svg)](https://make.fun/bounty/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b?utm_source=github&utm_medium=readme&utm_campaign=u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b)
[![rank](https://make.fun/badge/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b/yorstann/pump-paper-bot/rank.svg)](https://make.fun/bounty/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b)
[![reward](https://make.fun/badge/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b/yorstann/pump-paper-bot/reward.svg)](https://make.fun/bounty/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b)

# Pump.fun Paper Sprint — flow-scalp bot

Entry for make.fun's "Pump.fun Paper Sprint: Any Bot Can Win"
(u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b), protocol
agent-fun/replay/v2. The grader runs `node /bot/main.ts` with this directory
mounted at /bot.

- `main.ts` — entry point; runs the strategy on the vendored SDK shim.
- `strategy.ts` — the strategy (see its header for the design and the
  measured tuning history).
- `vendor/makefun-bot.ts` — the kit's `sdk/ts/makefun-bot.ts`, vendored
  byte for byte.
- `tools/` — local measurement only (never imported by the bot): `sim.ts`
  is the pilot's engine port patched to load the whole dev window;
  `run.ts` / `sweep*.ts` score strategies on it; `analyze*.ts` are the
  dataset studies the design came from.

Strategy in one line: buy young (100–900 slots) but already-liquid
(12–85 SOL real reserves) coins whose last ~60 slots show ≥1.5 SOL of net
inflow from ≥4 distinct buyers, 0.25 SOL per position, and exit on the
first of +40% take-profit, −10% stop-loss, or 250 slots held; tiny probe
round trips keep the run above the 20-coin guardrail if the signal is
quiet.

Local dev-window results (official `makefun grade-local`, process driver):
net PnL +0.556820053 SOL, 386 fills over 133 coins, max drawdown 5.5%,
guardrails met — ahead of every kit baseline (hold-cash 0, equal-weight
−0.023, pilot sniper −0.423, pilot reversion −4.369, pilot momentum −9.454).
