# MLB Over/Under Quantitative Prediction & Backtesting Engine

A algorithmic betting system designed to model MLB game totals (Over/Under) and backtest expected value against consensus market lines.

This project explores market efficiency in sports betting through statistical modeling and building a realistic Profit & Loss (P&L) simulator using historical odds.

## 📊 Project Overview

The objective of this engine is to identify pricing inefficiencies in MLB totals markets. While the final model did not achieve a positive ROI out-of-sample. Proving the high efficiency of modern sports book lines in MLB Over/Under markets.

## ⚙️ Architecture & Methodology

*   **Data Pipeline & Feature Engineering:** Ingests and processes 2025/2026 MLB game data. Features include rolling offensive metrics, starting pitcher whiff percentages, and bullpen performance indicators.
*   **Statistical Modeling (GLM):** 
    *   Initial iterations utilized Poisson Generalized Linear Models (GLMs).
    *   Transitioned to **Negative Binomial Maximum Likelihood Estimation (MLE)** to properly estimate the dispersion parameter ($\alpha$), accounting for the natural overdispersion inherent in baseball run-scoring environments.
*   **Monte Carlo Simulation:** Uses fitted Negative Binomial expected means ($\lambda$) to simulate 10,000 instances per game, calculating the true model probability of a game landing Over or Under the consensus line.
*   **Market Edge & EV Calculation:** Compares simulated probabilities against the implied probabilities of historical sports book lines (vig-adjusted) to identify positive Expected Value (+EV) thresholds.
*   **P&L Backtesting Engine:** Simulates chronological, season-long betting strategies comparing two staking methods:
    *   **Fixed Staking:** Flat percentage allocation of the starting bankroll.
    *   **Fractional Kelly Criterion:** Dynamic bet sizing based on calculated edge and real-time bankroll to optimize growth and manage variance.

## 💻 Tech Stack

*   **Language:** Python 
*   **Statistical Modeling:** `statsmodels` (GLM, Negative Binomial regression)
*   **Data Manipulation:** `pandas`, `numpy` (Vectorized Monte Carlo draws, timezone-aware manipulation)
*   **Visualization:** `matplotlib` (Equity curve plotting, calibration analysis)

## 📈 Key Findings & Limitations

Calibration analysis indicated the model accurately predicted average run totals; however, the consensus market lines were too efficient to beat mechanically using only rolling box-score and basic pitch-level data. Future alpha generation in this market would likely require granular, pitch-by-pitch biomechanical or localized weather data.
