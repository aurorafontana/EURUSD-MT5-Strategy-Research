# A/B Test History

## Purpose

The project evolved from one strategy into multiple simultaneous experiments identified by separate Magic Numbers. The goal was to compare trading windows, filters, direction, and exit parameters using the same general strategy family.

This document is a research map. Some variants changed during development, so the exact source code and test dates must be preserved before using historical results for formal statistical comparison.

## Test A — Baseline Controlled SELL

Research role: primary reference strategy.

Typical configuration during the main testing phase:

- SELL direction;
- original-style M1 entry logic;
- trading window approximately 08:00–17:00 local/test configuration;
- maximum concurrent positions introduced to control unlimited accumulation;
- lot size standardized to 0.10 during parts of demo testing;
- TP 21 as the baseline;
- original SL 273 as control.

This became the main benchmark against which other tests were interpreted.

## Test B — Morning Window

Research hypothesis: the strategy might perform better when restricted to the morning, avoiding weaker midday/afternoon conditions.

A tested window was approximately 08:00–12:00.

Status: historical experiment; later considered a candidate for removal due to insufficient incremental value.

## Test C — Alternative Time Window

Research hypothesis: isolate another subset of the trading day to identify whether losses cluster by hour.

Status: historical experiment. Exact configuration should be tied to the archived script version before formal reuse.

## Test D — 09:00–12:00 / Higher Position Allowance

Research hypothesis: concentrate trading in a narrower morning window while allowing more simultaneous opportunities.

A configuration discussed/tested used:

- approximately 09:00–12:00;
- maximum 10 positions.

Status: historical experiment; later considered for removal.

## Test E — RSI M15 Filter

Research hypothesis: avoid SELL entries when M15 RSI is below 35, because a short-only strategy entering after the market is already oversold may be vulnerable to reversal.

An experimental version used a substantially larger maximum-position allowance to collect more observations while filtering entries according to RSI M15.

Important clarification: the intended filter was to **exclude** entries when RSI M15 < 35, not to enter only when RSI M15 < 35.

This test generated very few or no trades in some observed periods, leading to questions about:

- whether the filter was implemented correctly;
- whether the operating hours were too restrictive;
- whether the base entry condition and RSI condition rarely overlapped;
- whether M15 was too slow for the M1 execution strategy.

Status: historical / under review; later considered a candidate for removal.

## Test F — BUY Experiment

Research hypothesis: determine whether a mirrored or adapted BUY-side strategy can exploit comparable conditions in the opposite direction.

The initial concept was designed to resemble Test A in operating hours while reversing trade direction and corresponding entry logic.

Important: a mechanically mirrored BUY strategy should not automatically be assumed equivalent to the SELL strategy. Spread, trend behavior, indicator conditions, and additional-entry logic must be validated independently.

Status: experimental.

## Test G — Take-Profit Experiment

Research hypothesis: the original TP 21 may leave favorable excursion uncaptured. A higher TP was tested in isolation to determine whether average profit can increase without materially reducing the win rate.

The project later decided to restore TP 21 as the control so that risk-management experiments could be isolated more cleanly.

Status: experimental; TP 21 remains the primary control value.

## Test H — M5 / Higher-Timeframe Filter Research

Research hypothesis: M1 entries may benefit from additional context from M5 to avoid low-quality FIRST entries or adverse market regimes.

Status: experimental / under review.

The key research challenge is to add information without over-filtering a strategy whose edge, if any, may depend on frequent short-term entries.

## Test I — BUY FIRST-Only Research

Research hypothesis: the BUY side may behave differently when limited to FIRST entries without the same averaging/additional-entry structure.

Status: experimental.

## Why Some Tests Are Being Removed

Running many strategies simultaneously creates several problems:

- overlapping and correlated positions;
- difficult attribution of account-level drawdown;
- small sample sizes per variant;
- increased logging complexity;
- harder interpretation of market conditions;
- risk of changing several variables simultaneously.

The current direction is to retire low-information variants and focus on a small set of controlled comparisons.

## Proposed Next Controlled Test

A high-priority experiment is:

### Control

- same baseline SELL entry logic;
- TP 21;
- SL 273;
- identical hours;
- identical position limits;
- identical lot sizing.

### Candidate

- same exact entry logic;
- TP 21;
- SL 245;
- all other parameters identical.

This directly tests the hypothesis generated by MAE analysis while minimizing confounding variables.

## Requirement for Future Tests

Every future test should document:

- test name;
- Magic Number;
- Git commit SHA;
- start/end date;
- broker/server timezone;
- local timezone;
- trading hours;
- lot sizing;
- maximum positions;
- FIRST logic;
- ADD logic;
- TP;
- SL;
- filters;
- transaction costs;
- results.

Without this metadata, comparisons should be treated as exploratory rather than definitive.