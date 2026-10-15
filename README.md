# Bayesian Statistics Assignment: Bayesian Regression and State-Space Modeling

**Course:** Bayesian Statistics  
**Student ID:** 0152310002  

---

## Overview

This repository contains the comprehensive implementation and empirical evaluation for the course assignment on **Bayesian Regression and State-Space Modeling**. All models were implemented in Python using **PyMC** and **ArviZ**, using NUTS MCMC sampling.

## Notebook Submissions
- [`0152310002.ipynb`](./0152310002.ipynb): Main executed notebook formatted according to course submission requirements (containing all outputs, diagnostic tables, and high-resolution visualizations).
- [`0152310002_Bayesian.ipynb`](./0152310002_Bayesian.ipynb): Duplicate notebook following alternate naming convention.

---

## Tasks Summary

### Task 1: Bayesian Logistic Regression (Binary Classification)
- **Dataset:** 35 clinical observations ($N = 35$) with continuous biomarker risk score $X \in [15, 65]$ and binary disease outcome $Y \in \{0, 1\}$.
- **Model:** Bernoulli likelihood with sigmoid link: $p_i = \sigma(\beta_0 + \beta_1 X_i)$, $\beta_0, \beta_1 \sim \mathcal{N}(0, 10^2)$.
- **Inference:** Sampled via NUTS MCMC (4 chains, 2000 draws, 1000 tuning steps).
- **Diagnostics & Results:** Posterior mean and 95% HDI reported. $\beta_1 > 0$ strictly positive with odds multiplier $\exp(\beta_1)$.
- **Evaluation:** Accuracy $\approx 88.6\%$, Precision, Recall, Specificity, F1-score, and Confusion Matrix.
- **Visualization:** Observed data, posterior mean probability sigmoid curve, and 95% Highest Density Credible Interval (HDI).

### Task 2: Bayesian Poisson Regression (Count Modeling)
- **Dataset:** 32 operational workload observations ($N = 32$) with covariate $X \in [0.5, 7.0]$ and incident counts $Y \in \mathbb{N}_0$.
- **Model:** Poisson likelihood with log-link: $\log(\mu_i) = \beta_0 + \beta_1 X_i$, $\beta_0, \beta_1 \sim \mathcal{N}(0, 10^2)$.
- **Diagnostics & Results:** Multiplicative rate scaling factor $\exp(\beta_1) \approx 1.38$ (+38% expected incident rate per workload unit).
- **Evaluation:** Mean Absolute Error (MAE) and Root Mean Squared Error (RMSE).
- **Visualization:** Observed incident counts, fitted posterior mean expected rate, 95% Credible Interval (epistemic mean uncertainty), and 95% Posterior Predictive Interval (aleatoric count noise).

### Task 3: Bayesian State-Space Model (Latent Random Walk)
- **Model:** Gaussian Random Walk hidden trajectory with observation equation:
  $$\theta_t \sim \mathcal{N}(\theta_{t-1}, \tau^2), \quad Y_t \sim \mathcal{N}(\theta_t, \sigma^2)$$
  $$\tau \sim \text{HalfNormal}(5), \quad \sigma \sim \text{HalfNormal}(5)$$
- **Experiment 1 (Modified Settings):** $T = 70$, $\tau_{\text{true}} = 1.20$, $\sigma_{\text{true}} = 2.40$, initial state $\theta_0 = 85.0$, seed = 303.
- **Diagnostics:** $\hat{R} \le 1.01$, ESS bulk/tail $> 400$, RMSE $\approx 1.08$, MAE $\approx 0.88$, mean 95% credible band width $\approx 4.09$.
- **Experiment 2 (High Volatility Comparison):** Altered state-transition noise $\tau_{\text{true}} = 3.20$ vs $\tau = 1.20$.
- **Analysis:** Demonstrates that higher system drift volatility reduces prior smoothing constraint, increasing credible band width and state reconstruction error.

### Task 4: Cross-Model Synthesis and Uncertainty Analysis
- **Summary Table:** Comprehensive comparison table consolidating posterior means, SDs, 95% HDIs, $\hat{R}$, ESS, and performance metrics across all models.
- **Visual Synthesis:** Two-panel comparative chart depicting normalized epistemic uncertainty across models and reconstruction error comparison.
- **Uncertainty Decomposition:** Theoretical and practical comparison of parameter (epistemic) vs observation/outcome (aleatoric) vs structural dynamic trajectory uncertainty.
- **Findings & Extensions:** In-depth discussion of MCMC convergence, overdispersion handling via Negative Binomial models, and higher-order state dynamics.
