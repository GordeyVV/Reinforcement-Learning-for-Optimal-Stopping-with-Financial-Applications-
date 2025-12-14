# Reinforcement Learning for Optimal Stopping with Financial Applications

This repository contains four artifacts that together demonstrate theory, simulation, and trading-style visualization for optimal stopping under uncertainty.

## Contents
- `Optimal_Stopping_via_EntropicRL.ipynb` — notebook implementing entropy-regularized optimal stopping from the referenced paper. Includes:
  - `RealOptionModel` for the GBM-based real option with analytical boundary `g_λ(x)`.
  - Policy Iteration (Algorithm 1) reproduced with corrections; converges to the analytical boundary with tiny L1 error.
  - Zeroth-order gradient descent to learn the initial boundary value `g₀(0)` (Algorithm 2).
  - Monte Carlo simulator (Algorithm 3) that reflects the controlled process and estimates value functions.
  - Plots comparing learned vs. analytical boundaries and sample controlled trajectories.
- `Optimal_Stopping_2_agent_RL.ipynb` — offline RL prototype on synthetic GBM stock data:
  - Generates and saves `synthetic_stock.csv`, performs descriptive stats, rolling MAs/volatility.
  - LSTM encoder + MLP policy for optimal stopping (continue vs stop) trained via replay buffer and target network.
  - Evaluation on fresh GBM paths; extends to dual call/put agents and a collaborative payoff view.
- `OSRL_trading.ipynb` — dynamic trading boundary experiment on real market data:
  - Downloads intraday prices for a basket of large-cap tickers via `yfinance`.
  - Estimates GBM parameters on sliding windows, updates the real-option boundary (`b*`/`a*`) on the fly.
  - Emits BUY/SELL signals when normalized price crosses boundaries; tracks cumulative P&L and boundary history.
  - Builds Matplotlib plots and Dash/Plotly-ready figures for price, signals, profits, and boundary evolution.
- `OSRL_trading_dashboard.html` — static Plotly dashboard with embedded data/figures:
  - Dropdowns for ticker and analysis type (price, profit, signals).
  - Panels for summary stats, portfolio overview, main price+boundary chart, profit curve, and signal table.
  - Opens locally in a browser (no backend required).

## Getting Started
1. Use Python 3.9+.
2. Install dependencies.
3. Open and run the notebooks in Jupyter/Lab. Cells are ordered to run top-to-bottom.
4. To view the dashboard, open `OSRL_trading_dashboard.html` in your browser. To regenerate it, rerun the plotting/export cells in `OSRL_trading.ipynb` (figures are built with Plotly).

