# Memory-Driven-Option-Pricing

## A Multi-Factor Memory-Based Affine Stochastic Volatility Framework for Option Pricing, Volatility Surface Modeling, Calibration, and Systematic Mispricing Detection

---

## Overview

Memory-Driven-Option-Pricing is a quantitative finance research framework that introduces a Multi-Factor Memory-Based Affine Stochastic Volatility Model for derivative pricing and volatility surface analysis.

The framework extends traditional stochastic volatility models by incorporating multiple interacting memory factors operating across different time horizons while preserving affine tractability.

The resulting model supports:

- Option Pricing
- Volatility Surface Construction
- Characteristic Function Methods
- Fourier Pricing
- FFT Acceleration
- Model Calibration
- Volatility Forecast Integration
- Systematic Mispricing Detection
- Indian Index Option Extensions

The primary objective is to create a mathematical bridge between volatility forecasting and option valuation.

---

# Motivation

Most option pricing models assume volatility can be represented by a single latent factor.

Examples include:

- Black-Scholes
- Heston
- SABR
- Local Volatility Models

While successful in many settings, these frameworks often struggle to capture:

- Volatility Clustering
- Long Memory
- Multi-Horizon Persistence
- Skew Persistence
- Smile Dynamics
- Market Microstructure Effects

Empirical evidence suggests volatility evolves simultaneously across multiple horizons.

For example:

```text
Intraday Volatility
        +
Daily Volatility
        +
Weekly Volatility
        +
Monthly Volatility
        +
Regime-Level Volatility
```

The Memory-Driven framework models these components explicitly.

---

# Model Architecture

The framework consists of four major layers.

```text
Memory Dynamics
        ↓
Variance Process
        ↓
Characteristic Function
        ↓
Option Pricing Engine
        ↓
Mispricing Detection
```

---

# Risk-Neutral Dynamics

Under the risk-neutral measure:

\[
dS_t = rS_tdt+\sqrt{v_t}S_tdW_t
\]

where:

| Symbol | Description |
|----------|-------------|
| \(S_t\) | Asset Price |
| \(v_t\) | Instantaneous Variance |
| \(r\) | Risk-Free Rate |
| \(W_t\) | Brownian Motion |

Applying Ito's Lemma:

\[
dX_t=
\left(
r-\frac12v_t
\right)dt
+\sqrt{v_t}dW_t
\]

where:

\[
X_t=\log(S_t)
\]

---

# Memory Factors

Introduce:

\[
U_t^{(1)},U_t^{(2)},...,U_t^{(m)}
\]

Each factor represents a different memory horizon.

Example:

| Factor | Interpretation |
|----------|-------------|
| U₁ | Intraday Memory |
| U₂ | Daily Memory |
| U₃ | Weekly Memory |
| U₄ | Monthly Memory |
| U₅ | Long-Term Regime Memory |

Unlike traditional models, volatility becomes a superposition of multiple persistence scales.

---

# Variance Specification

The variance process is defined as:

\[
v_t
=
\omega
+
\sum_{i=1}^{m}
\alpha_iU_t^{(i)}
\]

where:

| Parameter | Interpretation |
|------------|---------------|
| ω | Baseline Variance |
| αᵢ | Memory Loading |

Interpretation:

```text
Variance
=
Baseline
+
Short-Term Memory
+
Medium-Term Memory
+
Long-Term Memory
```

---

# Memory Dynamics

Each memory factor evolves according to:

\[
dU_t^{(i)}
=
\left(
-\lambda_iU_t^{(i)}
+
v_t
\right)dt
+
\epsilon_i\sqrt{v_t}dZ_t^{(i)}
\]

where:

| Parameter | Meaning |
|------------|----------|
| λᵢ | Mean-Reversion Rate |
| εᵢ | Volatility-of-Volatility |
| Zᵢ | Brownian Motion |

Interpretation:

Large λ:

```text
Fast Decay
Short Memory
```

Small λ:

```text
Slow Decay
Long Memory
```

---

# Correlation Structure

The driving processes satisfy:

\[
dW_tdZ_t^{(i)}
=
\rho_i dt
\]

where:

\[
-1<\rho_i<1
\]

Negative values generate:

- Leverage Effects
- Negative Equity Skew
- Return-Volatility Asymmetry

---

# Complete System

The complete model is:

\[
dX_t=
\left(
r-\frac12v_t
\right)dt
+
\sqrt{v_t}dW_t
\]

\[
v_t=
\omega
+
\sum_{i=1}^{m}
\alpha_iU_t^{(i)}
\]

\[
dU_t^{(i)}
=
(-\lambda_iU_t^{(i)}+v_t)dt
+
\epsilon_i\sqrt{v_t}dZ_t^{(i)}
\]

---

# Affine Structure

Define:

\[
Y_t
=
(X_t,U_t)
\]

The process belongs to the class of affine stochastic processes.

This is important because affine processes admit:

- Closed-Form Characteristic Functions
- Efficient Pricing
- Efficient Calibration
- Analytical Sensitivities

---

# Characteristic Function Representation

The conditional characteristic function is:

\[
\phi(u,T)
=
\mathbb E^Q
\left[
e^{iuX_T}
\middle|
\mathcal F_0
\right]
\]

Affine theory implies:

\[
\phi(u,T)
=
\exp
\left(
A(T,u)
+
B(T,u)^TU_0
+
iuX_0
\right)
\]

This representation is the foundation of the pricing engine.

---

# Riccati System

Define:

\[
\kappa(u)
=
\frac12(u^2+iu)
\]

and

\[
G(T,u)
=
-\kappa(u)
+
\sum_{j=1}^{m}
B_j(T,u)
\]

Then:

\[
\frac{dB_i}{dT}
=
-\lambda_iB_i
+
\alpha_iG
+
\frac12\epsilon_i^2B_i^2
+
\rho_i\epsilon_iiuB_i
\]

and

\[
\frac{dA}{dT}
=
iur
+
\omega G
\]

The solution of this system fully determines future return distributions.

---

# European Option Pricing

For a strike \(K\) and maturity \(T\):

\[
C(K,T)
=
e^{-rT}
\mathbb E^Q[(S_T-K)^+]
\]

Using Fourier methods:

\[
C(K,T)
=
e^{-rT}
\frac1\pi
\int_0^\infty
Re
\left[
\frac{
e^{-iu\log K}
\phi(u-i,T)
}
{
iu\phi(-i,T)
}
\right]
du
\]

Every aspect of the volatility structure enters through the characteristic function.

---

# FFT Pricing Engine

Direct pricing:

\[
O(N^2)
\]

FFT pricing:

\[
O(N\log N)
\]

Advantages:

- Fast Surface Construction
- Institutional Scale Pricing
- Efficient Calibration Loops

---

# Calibration Framework

The parameter vector is:

\[
\theta
=
(
\omega,
\alpha_i,
\lambda_i,
\epsilon_i,
\rho_i
)
\]

Given market implied volatilities:

\[
\sigma_i^{market}
\]

the model generates:

\[
\sigma_i^{model}
\]

Loss function:

\[
L(\theta)
=
\sum_{i=1}^{N}
w_i
(
\sigma_i^{model}
-
\sigma_i^{market}
)^2
\]

Calibration solves:

\[
\theta^*
=
argmin_\theta
L(\theta)
\]

---

# Analytical Jacobian

Residual:

\[
r_i
=
\sigma_i^{model}
-
\sigma_i^{market}
\]

Jacobian:

\[
J_{ij}
=
\frac{\partial r_i}
{\partial\theta_j}
\]

Differentiating the Riccati system provides analytical gradients.

Benefits:

- Faster Calibration
- Numerical Stability
- Reduced Computational Cost

---

# Gauss-Newton Optimization

Gradient:

\[
\nabla L
=
2J^Tr
\]

Approximate Hessian:

\[
H
\approx
2J^TJ
\]

Update:

\[
\theta_{n+1}
=
\theta_n
-
(J^TJ)^{-1}
J^Tr
\]

---

# Levenberg-Marquardt Regularization

Modified Hessian:

\[
H_{LM}
=
J^TJ
+
\eta I
\]

Update:

\[
\theta_{n+1}
=
\theta_n
-
(J^TJ+\eta I)^{-1}
J^Tr
\]

This combines:

- Gauss-Newton Speed
- Gradient Descent Stability

---

# Volatility Skew

ATM skew approximation:

\[
\left.
\frac{\partial\sigma_{imp}}
{\partial k}
\right|_{k=0}
=
\frac1{2\sqrt{v_0}}
\sum_{i=1}^{m}
\alpha_i\epsilon_i\rho_i
\]

Interpretation:

- Negative ρ → Negative Skew
- Large ε → Stronger Skew
- Multiple Factors → Persistent Skew

---

# Volatility Smile Curvature

\[
\left.
\frac{\partial^2\sigma_{imp}}
{\partial k^2}
\right|_{k=0}
\propto
\sum_{i=1}^{m}
\alpha_i\epsilon_i^2
\]

Produces:

- Smile Flexibility
- Stable Long-Term Curvature
- Better Surface Fit

---

# Tail Behavior

Extreme-strike behavior is governed by:

\[
\frac12\epsilon_i^2B_i^2
\]

This controls:

- Tail Thickness
- Moment Explosions
- Deep OTM Option Prices

---

# Mispricing Detection Framework

The framework converts volatility forecasts into option signals.

Model Price:

\[
C_{model}
\]

Market Price:

\[
C_{market}
\]

Mispricing:

\[
\Delta C
=
C_{market}
-
C_{model}
\]

Interpretation:

| Condition | Meaning |
|------------|----------|
| ΔC > 0 | Option Expensive |
| ΔC < 0 | Option Cheap |

---

# Signal Generation

Normalized score:

\[
Z
=
\frac{
C_{market}
-
C_{model}
}
{\sigma_{\Delta}}
\]

Trading framework:

| Z-Score | Interpretation |
|----------|---------------|
| \|Z\| > 2 | Potential Opportunity |
| \|Z\| > 3 | Strong Signal |

Pipeline:

```text
Volatility Forecast
        ↓
Memory Factors
        ↓
Variance Dynamics
        ↓
Option Valuation
        ↓
Market Comparison
        ↓
Mispricing Detection
        ↓
Trading Signal
```

---

# Indian Market Extension

The framework can be extended to:

- NIFTY Options
- BANKNIFTY Options
- FINNIFTY Options

Additional features:

### Expiry Effects

- Weekly Expiry Dynamics
- Theta Compression
- Expiry Volatility Spikes

### Market Positioning

- Open Interest Factors
- Dealer Positioning
- Put-Call Ratio Effects

### Event Risk

- RBI Announcements
- Union Budget
- Elections
- Macro Events

### Jump Components

- Event-Driven Volatility Shocks
- Poisson Jump Extensions

---

# Research Applications

The framework can be used for:

- Option Pricing
- Volatility Surface Construction
- Volatility Forecasting
- Quantitative Research
- Derivatives Modeling
- Systematic Trading
- Risk Management
- Market Making
- Relative Value Trading
- Statistical Arbitrage

---

# Future Development

Planned research directions:

- Rough Volatility Extensions
- Neural Calibration Methods
- Volterra Memory Kernels
- Regime Switching Dynamics
- Multi-Asset Extensions
- Stochastic Correlation Models
- Portfolio-Level Option Pricing
- Market Microstructure Integration

---

# License

This repository is intended for quantitative research, academic development, and systematic derivatives modeling.

