# Research Methodology

## Objective

The objective is to determine whether the EURUSD MT5 strategy can achieve positive and robust risk-adjusted expectancy after realistic costs, without relying on a misleadingly high win rate.

## Evidence Levels

Results should be labeled according to evidence quality:

1. **Observation** — behavior seen in a chart, log, or short forward-test period.
2. **Exploratory analysis** — retrospective analysis used to generate hypotheses.
3. **Static simulation** — historical trades modified without fully reconstructing future strategy state.
4. **Event-driven backtest** — strategy logic replayed chronologically with state changes.
5. **Out-of-sample test** — parameters frozen before evaluation on unseen data.
6. **Demo forward test** — real-time execution in a demo environment.
7. **Live evidence** — real-money execution including real costs and operational risk.

These categories must not be treated as interchangeable.

## Core Metrics

At minimum, every experiment should report:

- number of trades;
- winning and losing trades;
- win rate;
- average win;
- average loss;
- payoff ratio;
- expectancy;
- gross profit;
- gross loss;
- net profit;
- profit factor;
- maximum drawdown;
- consecutive wins/losses;
- maximum simultaneous positions;
- maximum notional exposure;
- MAE;
- MFE;
- holding time.

For basket strategies, also report:

- basket ID;
- number of entries per basket;
- FIRST vs ADD entries;
- weighted average entry;
- basket MAE/MFE;
- basket realized P/L;
- basket duration;
- maximum floating loss;
- reason for basket termination.

## Time Alignment

MT5 report timestamps, broker server time, local time, and exported market-data timestamps must be explicitly aligned.

The research has previously required timestamp-offset validation by matching trade exit prices against EURUSD M1 candles. Future datasets should record timezone metadata directly to reduce ambiguity.

## Avoiding Overfitting

Do not select parameters solely because they maximize historical net profit.

A candidate parameter should be preferred when:

- performance is stable across nearby parameter values;
- results persist across different market regimes;
- the mechanism is economically plausible;
- out-of-sample performance remains acceptable;
- transaction-cost assumptions are realistic.

## Suggested Validation Framework

1. Use an initial development period for exploratory analysis.
2. Define candidate rules before examining the validation period.
3. Freeze parameters.
4. Test on unseen historical data.
5. Perform walk-forward analysis.
6. Stress test spread/slippage assumptions.
7. Forward-test in demo.
8. Only then consider a very small live-risk experiment, if appropriate.

## Comparing A/B Tests

A/B tests should ideally run under identical:

- market period;
- broker environment;
- data feed;
- execution infrastructure;
- lot sizing;
- transaction-cost assumptions.

Only the variable under investigation should change whenever possible.

## MAE/MFE Research

MAE and MFE should be measured from entry until exit using sufficiently granular market data.

For SELL trades:

- adverse excursion is driven by price moving upward;
- favorable excursion is driven by price moving downward.

For BUY trades, the relationship is reversed.

Bid/ask effects should be modeled correctly when determining whether TP or SL would actually have triggered.

## Costs

A strategy with a small TP is highly sensitive to execution costs. Backtests should include:

- spread;
- commission;
- slippage;
- swap for overnight positions;
- possible weekend gaps;
- broker execution constraints.

## Friday and Weekend Analysis

Friday should be analyzed separately because positions left open may carry weekend gap and swap risk and can alter Monday's starting exposure.

Candidate experiments include:

- stop new FIRST entries after a defined Friday hour;
- stop ADD entries after a defined Friday hour;
- close baskets before market close;
- leave profitable/low-risk baskets only;
- compare all policies out of sample.

No Friday rule should be adopted based on a single week.

## Reproducibility

Every published result should be traceable to:

- code commit;
- configuration;
- data period;
- data source;
- timezone mapping;
- experiment/Magic Number;
- analysis script version.

The long-term goal is to make every important result independently reproducible.