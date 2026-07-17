# Open Research Questions

This file tracks the highest-value questions for community research.

## 1. Risk/Reward Asymmetry

The strategy historically produces many small winners and fewer but much larger losers.

Questions:

- What is the true expectancy after realistic costs?
- What loss distribution produces the negative tail?
- Can tail losses be reduced without eliminating too many recovering winners?

## 2. Fixed Stop vs Dynamic Stop

Candidate approaches:

- fixed SL;
- ATR-based SL;
- volatility percentile;
- structure-based stop;
- time-dependent stop;
- basket-level maximum loss.

Any proposal should be compared against the same entry sequence in a dynamic backtest.

## 3. FIRST vs ADD

Are losing baskets caused primarily by bad FIRST entries or by continued ADD entries after the initial thesis has deteriorated?

Needed analysis:

- P/L by FIRST vs ADD;
- MAE/MFE by entry type;
- probability of recovery by number of ADDs;
- marginal contribution of each additional entry;
- trend/volatility conditions before each ADD.

## 4. Basket Management

Potential research:

- maximum number of ADD entries;
- maximum basket exposure;
- basket-level stop;
- weighted-average break-even exits;
- partial basket reduction;
- no new ADD after a volatility/trend threshold;
- time stop for stale baskets.

## 5. Market Regime

Can losing baskets be identified as trend-regime events?

Candidate features:

- ADX;
- +DI/-DI;
- moving-average slope;
- M1/M5/M15 trend alignment;
- ATR;
- realized volatility;
- distance from moving averages;
- candle range expansion;
- consecutive directional candles.

## 6. RSI

An M15 RSI filter below 35 was tested experimentally for SELL entries, based on the idea that shorting an already oversold market may be dangerous.

Questions:

- Is M15 too slow for an M1 strategy?
- Would M5 provide better context?
- Is absolute RSI less useful than RSI slope or cross behavior?
- Does RSI add information beyond price trend and volatility?

## 7. Take Profit

TP 21 is the baseline.

Questions:

- What is the MFE distribution of winning trades?
- How many TP21 winners would also reach TP25, TP30, or higher?
- Does a larger TP reduce win rate enough to worsen expectancy?
- Would partial exits capture both high hit rate and larger moves?

## 8. Trading Hours

Historical experiments used multiple time windows.

Needed analysis:

- expectancy by entry hour;
- loss severity by hour;
- FIRST vs ADD by hour;
- performance by London/US session overlap;
- robustness across months.

## 9. Friday Risk

Questions:

- Are Friday entries statistically worse?
- Are Friday ADDs more dangerous than FIRST entries?
- What percentage of Friday positions remain open into the weekend?
- Does restricting late-Friday entries improve risk-adjusted returns?

## 10. BUY vs SELL

The original strategy is SELL only. BUY variants are experimental.

Questions:

- Is the strategy genuinely direction-specific?
- Does mirrored logic preserve the same statistical behavior?
- Should BUY use different parameters?
- Does EURUSD exhibit asymmetry relevant to the strategy?

## 11. Event-Driven Backtesting

This is a high-priority engineering problem.

The backtester should reproduce:

- chronological ticks/bars;
- FIRST and ADD state;
- maximum-position constraints;
- Magic Number isolation;
- TP/SL triggers;
- spread;
- order execution;
- dynamic re-entry after exits;
- basket state.

## 12. Overfitting Control

How should the project define:

- development period;
- validation period;
- walk-forward windows;
- minimum trade counts;
- parameter stability requirements;
- multiple-testing correction?

Contributions that improve experimental rigor are as valuable as strategy changes.