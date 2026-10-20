# DerivaQuant — Quantitative Options Pricing & Risk Analytics

A Python-based quantitative finance project for options valuation, risk sensitivity analysis, Monte Carlo simulation, and portfolio risk measurement.

## Overview

DerivaQuant explores how mathematical models can be used to price financial derivatives, estimate implied volatility, and evaluate portfolio risk. It implements analytical and numerical approaches to options pricing and compares their outputs under different market assumptions.

## Features

- **Black–Scholes Model:** Analytical pricing of European call and put options.
- **Option Greeks:** Calculation of Delta, Gamma, Vega, Theta, and Rho to measure option-price sensitivity.
- **CRR Binomial Tree:** Discrete-time option pricing using backward induction, including early-exercise evaluation for American options.
- **Model Convergence:** Analysis of binomial-tree prices as the number of time steps increases.
- **Monte Carlo Option Pricing:** Simulation of underlying asset prices using Geometric Brownian Motion to estimate option values.
- **Implied Volatility:** Numerical estimation using the Newton–Raphson method with a bisection fallback.
- **Convergence Visualization:** Animation illustrating the iterative implied-volatility estimation process.
- **Portfolio Risk Analysis:** Simulation-based Value at Risk (VaR) and Conditional Value at Risk (CVaR) estimation.
- **Market Data Integration:** Historical price data retrieved through Yahoo Finance and an optional risk-free-rate input from FRED.

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core implementation |
| NumPy | Numerical computation and simulation |
| SciPy | Probability distributions and statistical calculations |
| Pandas | Financial data manipulation |
| Matplotlib | Charts and convergence animations |
| yfinance | Historical market data |
| fredapi | Retrieval of FRED economic data |

## Models and Methodology

### 1. Black–Scholes Pricing

The Black–Scholes model estimates European option prices using the underlying asset price, strike price, time to expiry, volatility, and risk-free interest rate.

For a European call:

\[
C=S\,N(d_1)-Ke^{-rT}N(d_2)
\]

For a European put:

\[
P=Ke^{-rT}N(-d_2)-SN(-d_1)
\]

where \(S\) is the underlying price, \(K\) is the strike price, \(T\) is time to expiry, \(r\) is the continuously compounded risk-free rate, and \(N(\cdot)\) is the standard normal cumulative distribution function.

### 2. Option Greeks

The project calculates five common option sensitivities:

- **Delta:** Sensitivity to changes in the underlying asset price.
- **Gamma:** Sensitivity of Delta to changes in the underlying price.
- **Vega:** Sensitivity to changes in implied volatility.
- **Theta:** Sensitivity to the passage of time.
- **Rho:** Sensitivity to changes in the risk-free interest rate.

### 3. Binomial Tree

The Cox–Ross–Rubinstein (CRR) model represents possible underlying prices in a recombining tree. Option values are computed through backward induction. For American options, the model compares the value of holding the option with its immediate exercise value at each node.

### 4. Monte Carlo Simulation

The simulation models possible future asset prices under Geometric Brownian Motion. Discounted option payoffs are averaged to estimate option values. Simulated portfolio outcomes are also used to study potential losses.

### 5. Implied Volatility

Implied volatility is estimated by finding the volatility value that makes the model price match an observed option price. Newton–Raphson iterations are used, with bisection as a fallback when necessary.

### 6. Portfolio Risk: VaR and CVaR

- **Value at Risk (VaR):** Estimates a loss threshold at a selected confidence level over a specified time horizon.
- **Conditional Value at Risk (CVaR):** Estimates the average loss in the tail beyond that threshold.

The estimates depend on the portfolio composition, historical data, simulation assumptions, and number of simulations. They are not guarantees of future losses.

## Installation

Clone the repository:

```bash
git clone <YOUR_REPOSITORY_URL>
cd DerivaQuant
```

Install the dependencies:

```bash
pip install numpy scipy pandas matplotlib yfinance fredapi
```

Open Jupyter Notebook:

```bash
jupyter notebook
```

Open `DerivaQuant.ipynb` and run the cells sequentially.

## Configuration

The notebook can retrieve historical market data through Yahoo Finance. Internet connectivity and successful data retrieval are required for live downloads.

If FRED is used to retrieve the risk-free rate, obtain your own API key from the [FRED API documentation](https://fred.stlouisfed.org/docs/api/api_key.html).

Store the key in an environment variable rather than hardcoding it in the notebook:

```python
import os
from fredapi import Fred

fred = Fred(api_key=os.environ["FRED_API_KEY"])
```

Set `FRED_API_KEY` in your local environment before running the relevant cell. Never publish private API keys or credentials.

## Project Structure

```text
DerivaQuant/
├── DerivaQuant.ipynb
├── README.md
└── requirements.txt
```

The notebook contains the implementation, calculations, visualizations, and simulation outputs. Add separate Python modules and tests if you modularize the implementation.

## Limitations

- Black–Scholes assumes constant volatility and is designed for European options.
- Historical estimates may not represent future market behaviour.
- Monte Carlo estimates contain sampling error and depend on the simulation assumptions.
- VaR and CVaR estimates can change with the selected confidence level, horizon, and portfolio data.
- Market-data availability and external API access are not guaranteed.

## Learning Objectives

- Understand quantitative options pricing and financial derivatives.
- Apply numerical methods to financial modelling problems.
- Analyze option-price sensitivity using Greeks.
- Estimate implied volatility using numerical optimization.
- Evaluate portfolio downside risk using Monte Carlo simulations, VaR, and CVaR.

## Limitations

- Black–Scholes assumes constant volatility and is designed for European options.
- Historical market data may not represent future market conditions.
- Monte Carlo estimates depend on simulation assumptions and sample size.
- VaR and CVaR are estimates, not guarantees of future losses.
- Live market-data and economic-data APIs may be unavailable.

## Disclaimer

This project is intended for educational and research purposes only. It does not constitute financial or investment advice.