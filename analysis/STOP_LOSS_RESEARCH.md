# Stop-Loss Research

## Problem

The baseline strategy combines a small TP with a substantially wider SL. This supports a high win rate but exposes the system to large negative-tail events.

The research question is not simply "What SL produces the best historical result?" The more important question is:

> What risk rule reduces catastrophic losses while preserving enough of the strategy's recovery behavior to improve out-of-sample expectancy?

## Historical MAE Evidence

For 1,512 winning trades in the aggregate June–July research sample:

- median MAE: 3.6 pips;
- mean MAE: 6.1 pips;
- 90th percentile: 14.8 pips;
- 95th percentile: 20.2 pips;
- 99th percentile: 24.2 pips.

The original nominal stop was approximately 27.3 pips.

## Static Candidate

A static sensitivity analysis suggested approximately 24.5 pips (245 points) as an interesting candidate. In that historical reconstruction it stopped 12 of 1,512 eventual winners (0.79%).

This does **not** establish 245 as an optimal SL.

## Why Optimization Is Dangerous

Selecting the single best value from one historical sample can overfit noise. A robust candidate should show acceptable performance across a neighborhood of values and across multiple market regimes.

The observed region around 240–250 points is therefore more informative than treating 245 as a magical exact number.

## Proposed Forward Test

Run two isolated variants simultaneously:

### Control

- identical SELL entry logic;
- TP 21;
- SL 273;
- same hours;
- same lot;
- same max positions.

### Candidate

- identical SELL entry logic;
- TP 21;
- SL 245;
- all other parameters unchanged.

Use separate Magic Numbers and log every FIRST/ADD entry.

## Success Criteria

Do not judge only by net P/L.

Compare:

- trade count;
- win rate;
- average win/loss;
- expectancy;
- profit factor;
- max drawdown;
- number of full SL events;
- basket loss distribution;
- number of historical-style recovery trades lost;
- MAE/MFE;
- maximum concurrent exposure.

## Alternative Hypotheses

A fixed SL may not be the best solution. Future experiments could compare:

- ATR-adjusted stop;
- basket-level stop;
- stop tightening after N additional entries;
- stop based on trend strength;
- time stop;
- volatility-regime-dependent stop.

Each should be tested independently before combining rules.