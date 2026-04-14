# Asian Call Option Pricing via Monte Carlo Simulation

This repository contains a Python implementation of an **Arithmetic Asian Call Option** pricer using Monte Carlo simulation. The model assumes underlying asset prices follow a **Geometric Brownian Motion (GBM)**.

## Overview

Unlike European options, which only depend on the asset price at maturity, **Asian options** are path-dependent. Their payoff is determined by the **arithmetic average price** of the underlying asset over the life of the option.

This pricer simulates thousands (or millions) of potential price paths, calculates the arithmetic average for each, determines the payoff, and discounts the expected value back to the present.

## Key Features

* **Vectorized Simulation**: Uses NumPy to generate price paths efficiently.
* **Batch Processing**: Implements batch-based computation to handle large-scale simulations ($N > 1,000,000$) without exhausting system RAM.
* **Statistical Precision**: Utilizes the **Central Limit Theorem (CLT)** to provide a confidence interval for the calculated price.
* **Dividends & Yields**: Supports continuous dividend yield ($q$) and risk-free rate ($r$) adjustments.

## Financial Logic

The simulation follows the stochastic differential equation for GBM:

$$ dS_t = (r - q) S_t dt + \sigma S_t dW_t $$

The price at each discrete step is calculated as:
$$ S_{t+\Delta t} = S_t \exp\left( (r - q - \frac{\sigma^2}{2})\Delta t + \sigma \sqrt{\Delta t} Z \right) $$

Where $Z \sim N(0, 1)$.

## Error Estimation & CLT

The accuracy of a Monte Carlo simulation is governed by the **Central Limit Theorem**. The code provides an error margin calculated as:

$$ P\left( \hat{C} - z_{\alpha/2} \frac{\sigma}{\sqrt{N}} \leq C \leq \hat{C} + z_{\alpha/2} \frac{\sigma}{\sqrt{N}} \right) = 1 - \alpha $$

