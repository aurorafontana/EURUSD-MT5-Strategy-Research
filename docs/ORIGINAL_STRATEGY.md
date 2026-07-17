# Original Strategy Baseline

## Origin

This research project started from the public `ryu878/MT5-python-bot` repository, described by its author as **Ryuryu's FOREX MT5 EURUSD Bot**.

Original repository:

`https://github.com/ryu878/MT5-python-bot`

This document describes the baseline concept used as the starting point for independent experimentation. Refer to the upstream repository for the authoritative original source.

## Baseline Characteristics

The original script used in this research has the following key characteristics:

- MetaTrader 5 Python integration;
- EURUSD;
- M1 execution timeframe;
- SELL-only direction;
- SMA-based logic;
- fixed base lot size;
- smaller additional-entry lot configuration in the upstream code;
- fixed take-profit distance;
- stop loss derived from a multiplier of the take-profit distance;
- repeated polling/execution loop.

The baseline parameters visible in the upstream-style script used for this project included:

- `take_profit_short = 21`
- `sl_multiplier = 13`
- therefore a nominal SL distance of `273` MT5 points;
- base lot `0.1`;
- additional lot `0.01` in the original upstream-style configuration.

## Indicator Calculation

The strategy calculates moving averages on M1 bars, including:

- SMA of the 6-period high;
- SMA of the 6-period low;
- SMA 33;
- SMA 60;
- SMA 120;
- SMA 240.

The original entry logic shown in the baseline script primarily uses the short-term SMA condition for actual order triggering, while the additional longer moving averages are calculated but are not necessarily used as entry filters in that version.

## First Entry

The baseline defines a short-entry condition equivalent to price/ask being above the 6-period high SMA.

When no position is detected and that condition is true, a SELL order is sent.

This can be interpreted as a short/mean-reversion-style idea: the system sells after price moves above a short-term reference and expects a relatively small retracement.

## Additional Entry

When a position already exists, the baseline can add another SELL when the short-entry condition remains valid and the SMA 6-low relationship to the existing position price satisfies the additional-entry rule.

This behavior is central to the research problem. Additional entries can improve recovery when price mean-reverts, but they can also increase exposure during a persistent trend.

## Take Profit and Stop Loss

The baseline uses a small TP relative to a much wider SL.

This structure naturally supports a high hit rate if many small retracements occur, but it creates negative payoff asymmetry: one full loss can require many small winners to recover.

The project therefore treats the original TP/SL relationship as a control, not as an assumed optimal configuration.

## Important Implementation Questions

Community code review is requested around:

- whether position detection correctly handles multiple simultaneous positions;
- how the last iterated position affects `pos_price`, `identifier`, and `volume`;
- whether additional-entry SL/TP modification behaves as intended for all positions;
- whether SELL orders should use bid rather than ask for execution assumptions in the request;
- broker filling-mode compatibility;
- repeated-entry frequency in the polling loop;
- race conditions between position retrieval and order execution;
- correct separation of positions by Magic Number;
- robust handling of disconnections and MT5 API errors.

## Research Principle

The original strategy should remain available conceptually as a baseline. Experimental improvements should be compared against a clearly defined control rather than gradually modifying the strategy until the original behavior is no longer identifiable.