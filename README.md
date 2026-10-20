# DerivaQuant — Quantitative Options Pricing & Risk Analytics

A Python-based quantitative finance project exploring options valuation, risk sensitivities, numerical pricing methods, implied volatility estimation, and portfolio risk measurement.

## Overview

DerivaQuant brings together analytical and simulation-based methods for studying financial derivatives. It implements option pricing models, calculates the Greeks, estimates implied volatility, and uses Monte Carlo simulation to analyze potential portfolio outcomes.

This project is intended for educational and quantitative research purposes.

## Features

- **Black–Scholes Model:** Analytical pricing for European call and put options.
- **Option Greeks:** Calculation of Delta, Gamma, Vega, Theta, and Rho.
- **CRR Binomial Tree:** Option valuation using backward induction, including early-exercise evaluation for American options.
- **Model Convergence:** Analysis of binomial-tree prices as the number of time steps increases.
- **Monte Carlo Option Pricing:** Simulation of asset prices using Geometric Brownian Motion (GBM).
- **Implied Volatility Solver:** Newton–Raphson iteration with a bisection fallback.
- **Convergence Visualization:** Animation of the iterative implied-volatility estimation process.
- **Portfolio Risk Analysis:** Simulation-based Value at Risk (VaR) and Conditional Value at Risk (CVaR).
- **Market Data Integration:** Historical prices through Yahoo Finance and optional risk-free-rate retrieval through FRED.

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Core implementation |
| NumPy | Numerical computation and simulation |
| SciPy | Probability distributions and statistical calculations |
| Pandas | Financial data manipulation |
| Matplotlib | Charts and animations |
| yfinance | Historical market data |
| fredapi | FRED economic data access |

## Models and Methodology

### 1. Black–Scholes Pricing

The Black–Scholes model estimates European option prices using the underlying asset price, strike price, time to expiry, volatility, and risk-free interest rate.

For a European call:

\[
C = S N(d_1) - K e^{-rT} N(d_2)
\]

For a European put:

\[
P = K e^{-rT} N(-d_2) - S N(-d_1)
\]

where:

\[
d_1 = \frac{\ln(S/K)+(r+\sigma^2/2)T}{\sigma\sqrt{T}}
\]

\[
d_2 = d_1-\sigma\sqrt{T}
\]

Here, \(S\) is the underlying asset price, \(K\) is the strike price, \(T\) is time to expiry in years, \(r\) is the continuously compounded risk-free rate, \(\sigma\) is volatility, and \(N(\cdot)\) is the standard normal cumulative distribution function.

### 2. Option Greeks

The project calculates five standard measures of option-price sensitivity:

- **Delta:** Sensitivity to changes in the underlying asset price.
- **Gamma:** Rate of change of Delta with respect to the underlying price.
- **Vega:** Sensitivity to changes in volatility.
- **Theta:** Sensitivity to the passage of time.
- **Rho:** Sensitivity to changes in the risk-free interest rate.

The units of Vega, Theta, and Rho depend on the implementation and scaling conventions used in the notebook.

### 3. CRR Binomial Tree

The Cox–Ross–Rubinstein model represents possible underlying asset prices using a recombining tree. Option values are calculated through backward induction.

For American options, the model compares the continuation value with the immediate exercise value at each node, allowing for early exercise.

### 4. Monte Carlo Simulation

The simulation models possible future asset prices using Geometric Brownian Motion. Discounted option payoffs are averaged to estimate option values.

Monte Carlo simulation is also used to generate possible portfolio outcomes and examine the distribution of potential losses.

### 5. Implied Volatility

Implied volatility is the volatility value that makes a theoretical option price match an observed market price.

The solver uses Newton–Raphson iteration and falls back to bisection when necessary. Its accuracy depends on the option inputs, numerical tolerance, and convergence behaviour.

### 6. Portfolio Risk: VaR and CVaR

- **Value at Risk (VaR):** Estimates a loss threshold at a specified confidence level and time horizon.
- **Conditional Value at Risk (CVaR):** Estimates the average loss in the tail beyond the VaR threshold.

Both measures depend on portfolio composition, market data, simulation assumptions, and sample size. They are estimates rather than guarantees of future losses.

## Installation

Clone the repository:

```bash
git clone https://github.com/TarunDev-stack/DerivaQuant.git
cd DerivaQuant
```

Install the dependencies:

```bash
pip install numpy scipy pandas matplotlib yfinance fredapi py_vollib
```

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open `OP.ipynb` and execute the cells in order.

> The notebook currently retains the filename `OP.ipynb`. Update this instruction if you rename it later.

## Configuration

### Market Data

Historical market data is retrieved through Yahoo Finance. Successful downloads require an internet connection and data availability for the selected tickers.

### FRED Risk-Free Rate

If you enable FRED integration, obtain your own API key from the [FRED API documentation](https://fred.stlouisfed.org/docs/api/api_key.html).

Store your key in an environment variable instead of hardcoding it in the notebook.

```python
import os
from fredapi import Fred

fred = Fred(api_key=os.environ["FRED_API_KEY"])
```

Set `FRED_API_KEY` in your local environment before executing the relevant cell. Never publish API keys or credentials.

## Project Structure

```text
DerivaQuant/
├── OP.ipynb
├── README.md
├── implied_vol_nr.gif
├── monte-carlo result.png
└── multi-tree.JPG
```

The notebook contains the pricing implementations, calculations, simulation outputs, and visualizations. The image files provide supporting visual results.

## Limitations

- Black–Scholes assumes constant volatility and is designed for European options.
- Historical market data may not represent future market conditions.
- Monte Carlo estimates contain sampling error and depend on the simulation assumptions and number of paths.
- VaR and CVaR estimates vary with the confidence level, time horizon, portfolio composition, and underlying loss distribution.
- External market-data and economic-data APIs may be unavailable or return incomplete data.
- Numerical models rely on their input assumptions and implementation details.

## Learning Objectives

- Understand quantitative options pricing and financial derivatives.
- Apply analytical and numerical methods to financial modelling.
- Analyze option-price sensitivities using Greeks.
- Estimate implied volatility through numerical root-finding methods.
- Evaluate potential portfolio losses using Monte Carlo simulation, VaR, and CVaR.

## Disclaimer

This project is intended for educational and research purposes only. It does not constitute financial or investment advice.
