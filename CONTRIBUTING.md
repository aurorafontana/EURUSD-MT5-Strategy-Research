# Contributing

Thank you for considering a contribution to EURUSD MT5 Strategy Research.

This project is intended to be an evidence-based research environment. The goal is not to maximize the number of strategy variations. The goal is to understand why the system wins, why it loses, and whether changes improve risk-adjusted performance in a reproducible way.

## Ways to Contribute

You can help with:

- Python/MetaTrader 5 code review;
- identifying bugs or execution inconsistencies;
- event-driven backtesting;
- statistical analysis;
- MAE/MFE research;
- FIRST vs ADD entry analysis;
- basket-level risk management;
- stop-loss and take-profit research;
- volatility and market-regime filters;
- logging improvements;
- walk-forward validation;
- documentation.

## Before Proposing a Strategy Change

Please describe:

1. **Hypothesis** — What problem are you trying to solve?
2. **Exact rule** — What precisely changes?
3. **Mechanism** — Why should the change improve the strategy?
4. **Control** — What existing configuration will it be compared against?
5. **Dataset** — Which period and market data will be used?
6. **Metrics** — Net P/L, profit factor, drawdown, expectancy, win rate, MAE/MFE, etc.
7. **Validation** — How will you test out of sample?

Avoid proposals based only on one unusually good or bad trading day.

## Experimental Discipline

Whenever possible, change one major variable at a time. Use unique Magic Numbers or experiment identifiers, preserve the code version used for each test, and report losing results as clearly as winning results.

Do not optimize only for win rate. A high win rate with negative expectancy is not a successful outcome.

## Code Contributions

Please keep changes focused and documented. Never commit credentials, MT5 account IDs, passwords, API keys, private broker information, or personal data.

If you modify trading logic, document the exact behavioral difference and provide enough information for another contributor to reproduce the test.

## Data Contributions

Do not upload sensitive account exports without sanitizing them. Remove account numbers, names, broker identifiers where unnecessary, and any other private information.

Prefer compact, anonymized datasets that are sufficient to reproduce the analysis.

## Discussion Standard

Constructive criticism is welcome. Claims about performance should be supported by data and methodology. Please distinguish clearly between observed results, hypotheses, simulations, and forward-test evidence.

## Financial Disclaimer

Contributing to this project does not imply that any strategy is suitable for live trading. All code and research are provided for educational and experimental purposes.