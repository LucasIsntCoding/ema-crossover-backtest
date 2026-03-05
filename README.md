# EMA Crossover Backtesting Engine

A technical Python-based backtesting framework for evaluating **exponential moving average (EMA) crossover strategies** on historical price data. The project implements a **long/flat systematic trading model**, simulates portfolio performance under configurable execution assumptions, and provides detailed analytics for strategy evaluation.

## Overview

This project tests a classic trend-following strategy in which trading signals are generated from the interaction between a **short-term EMA** and a **long-term EMA**:

- **Enter long** when the short EMA crosses above the long EMA
- **Exit to cash** when the short EMA crosses below the long EMA

The engine is designed to go beyond a basic toy backtest by incorporating:

- vectorised portfolio simulation
- position sizing logic
- transaction cost modelling
- trade extraction and blotter generation
- equity curve and drawdown tracking
- professional performance metrics

It is intended as a practical introduction to **systematic strategy development**, **backtest architecture**, and **quantitative performance analysis**.

---

## Features

- **EMA crossover signal generation**
  - configurable fast and slow EMA windows
  - clean crossover logic with lookahead bias avoided via shifted execution

- **Long/flat portfolio simulation**
  - fully vectorised daily-bar backtest
  - portfolio equity tracked over time

- **Position sizing**
  - fixed fractional exposure
  - optional volatility-targeted exposure

- **Transaction cost modelling**
  - commissions
  - slippage
  - optional bid/ask spread proxy

- **Trade blotter generation**
  - entry/exit timestamps
  - holding period
  - gross and net trade returns

- **Performance analytics**
  - total return
  - CAGR
  - annualised return and volatility
  - Sharpe ratio
  - Sortino ratio
  - Calmar ratio
  - maximum drawdown
  - VaR / CVaR
  - skew / kurtosis
  - turnover and exposure statistics
  - win rate, profit factor, expectancy

- **Visualisation**
  - price chart with EMAs
  - entry and exit markers
  - equity curve
  - drawdown series

- **Optional parameter search**
  - brute-force optimisation across EMA window pairs

---

## Strategy Logic

The strategy uses two exponential moving averages:

- **Fast EMA**: reacts more quickly to recent price changes
- **Slow EMA**: represents the broader price trend

Signal definition:

- `1` when `EMA_fast > EMA_slow`
- `0` otherwise

To avoid lookahead bias:

- the signal is computed on bar `t`
- the position is applied on bar `t+1`

This ensures the backtest reflects a more realistic execution process.

---

## Project Structure

```text
.
├── backtest.py          # core backtest engine
├── prices.csv           # optional local price data
├── README.md            # project documentation
