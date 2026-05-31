# Memory-Driven Option Pricing: A Multi-Factor Affine Stochastic Volatility Framework for Option Valuation and Mispricing Detection

## Stochastic Foundations

> **"Before one can model volatility, one must first understand randomness itself."**

### 1. Introduction

Modern quantitative finance is fundamentally built upon stochastic processes. Asset prices evolve through time under uncertainty. Interest rates fluctuate. Volatility changes dynamically. Derivative prices depend upon future random outcomes.

Consequently, any rigorous framework for option pricing must begin with a mathematical theory of randomness.

The purpose of this chapter is to establish the probabilistic and stochastic foundations required for the development of the **Memory-Driven Affine Volatility Framework**.

We introduce:

- Probability spaces
- Random variables
- Filtrations
- Stochastic processes
- Brownian motion
- Martingales
- Itô calculus
- Stochastic differential equations
- Measure changes
- Risk-neutral valuation

These concepts form the mathematical language through which modern derivative pricing is constructed.

---

### 2. Probability Spaces

The mathematical representation of uncertainty begins with a **probability space**:

$$
(\Omega, \mathcal{F}, \mathbb{P})
$$

**Sample Space** ($\Omega$): Contains all possible outcomes.  
**Sigma Algebra** ($\mathcal{F}$): Defines measurable events.  
**Probability Measure** ($\mathbb{P}$): Assigns probabilities to events.

---

### 3. Random Variables

A random variable is a measurable mapping:

$$
X: \Omega \rightarrow \mathbb{R}
$$

Examples: future stock price, future volatility, option payoff.

---

### 4. Expectation

For a continuous random variable $X$ with density $f(x)$:

$$
\mathbb{E}[X] = \int_{-\infty}^{\infty} x f(x) \, dx
$$

Most pricing formulas ultimately take the form:

$$
\text{Price} = \mathbb{E}[\text{Discounted Payoff}]
$$

---

### 5. Conditional Expectation

$$
\mathbb{E}[X \mid \mathcal{G}]
$$

where $\mathcal{G}$ represents the available information at a given time. This is central to dynamic pricing.

---

### 6. Information and Filtrations

A **filtration** is an increasing family of sigma algebras:

$$
\{\mathcal{F}_t\}_{t \ge 0} \quad \text{such that} \quad \mathcal{F}_s \subseteq \mathcal{F}_t \quad (s < t)
$$

It formalizes the gradual flow of information in financial markets.

---

### 7. Stochastic Processes

A stochastic process is a collection of random variables indexed by time:

$$
\{X_t\}_{t \ge 0}
$$

Examples: asset price $S_t$, variance $v_t$, memory factors $U_t^{(i)}$.

---

### 8. Brownian Motion

Standard Brownian motion $W_t$ satisfies:

- $W_0 = 0$
- Independent increments
- $W_t - W_s \sim N(0, t-s)$
- Continuous paths

Brownian motion represents pure random market noise.

---

### 9. Quadratic Variation

A key property:

$$
(dW_t)^2 = dt \quad \text{or} \quad [W]_t = t
$$

This underpins Itô calculus.

---

### 10. Martingales

A process $M_t$ is a martingale if:

$$
\mathbb{E}[M_t \mid \mathcal{F}_s] = M_s \quad (s < t)
$$

Under the risk-neutral measure, discounted asset prices are martingales.

---

### 11. Itô Processes

Most financial variables follow:

$$
dX_t = \mu_t \, dt + \sigma_t \, dW_t
$$

---

### 12. Itô's Lemma

For $f(t, X_t)$ where $dX_t = \mu_t dt + \sigma_t dW_t$:

$$
df = \left( \frac{\partial f}{\partial t} + \mu_t \frac{\partial f}{\partial x} + \frac{1}{2} \sigma_t^2 \frac{\partial^2 f}{\partial x^2} \right) dt + \sigma_t \frac{\partial f}{\partial x} \, dW_t
$$

This is one of the most important tools in quantitative finance.

---

### 13. Stochastic Differential Equations (SDEs)

**Geometric Brownian Motion:**

$$
dS_t = \mu S_t \, dt + \sigma S_t \, dW_t
$$

**CIR Variance Process:**

$$
dv_t = \kappa(\theta - v_t) \, dt + \xi \sqrt{v_t} \, dW_t
$$

**Memory Factor Dynamics (later):**

$$
dU_t^{(i)} = (-\lambda_i U_t^{(i)} + v_t) \, dt + \epsilon_i \sqrt{v_t} \, dZ_t^{(i)}
$$

---

### 14. Correlated Brownian Motions

$$
dW_t \, dZ_t = \rho \, dt
$$

Negative $\rho$ produces the leverage effect and volatility skew.

---

### 15. Change of Measure & Girsanov's Theorem

Transforms the real-world measure $\mathbb{P}$ to the risk-neutral measure $\mathbb{Q}$ by adjusting drifts.

---

### 16. Risk-Neutral Valuation

Under $\mathbb{Q}$:

$$
dS_t = r S_t \, dt + \sigma_t S_t \, dW_t^{\mathbb{Q}}
$$

The price of a derivative with payoff $H(S_T)$ is:

$$
V_t = e^{-r(T-t)} \mathbb{E}^{\mathbb{Q}} \left[ H(S_T) \mid \mathcal{F}_t \right]
$$

---

### 17. Fundamental Theorem of Asset Pricing

**No Arbitrage** ⇔ **Existence of a Risk-Neutral Measure**

---

### 18. From Stochastic Foundations to Affine Volatility Models

The Memory-Driven Framework combines:

- Stochastic differential equations
- Correlated Brownian motions
- Risk-neutral dynamics
- Martingale pricing
- Affine process theory

All memory factors $U_t^{(i)}$ are stochastic processes built on these foundations.

---

## Conclusion

This chapter established the probabilistic language underlying modern quantitative finance — from probability spaces to risk-neutral valuation.

These concepts provide the mathematical infrastructure upon which the multi-factor memory-driven volatility model is constructed.

---

**Next Chapter Preview:** The next section introduces volatility memory and develops the mathematical structure of multi-horizon memory factors.

---
