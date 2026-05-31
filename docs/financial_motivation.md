
# Memory-Driven Option Pricing: A Multi-Factor Affine Stochastic Volatility Framework for Option Valuation and Mispricing Detection

## Financial Motivation

> **"Every successful financial model begins not with mathematics, but with an observation about reality."**

### 1. Why Do We Need Another Volatility Model?

The history of quantitative finance is a continuous effort to answer one fundamental question:

**How should uncertainty be priced?**

Every derivative contract derives its value from uncertainty. Without uncertainty → no optionality. Without optionality → no option premium.

In modern markets, this uncertainty is captured by a single but powerful object: **volatility** ($\sigma$).

Volatility influences:
- Risk management
- Derivative pricing
- Portfolio allocation
- Capital requirements
- Hedging costs
- Tail exposure

It is the market’s primary measure of fear and uncertainty.

Yet volatility remains one of the hardest phenomena to model accurately.

---

### 2. The Black-Scholes Revolution

The modern era of derivatives began with the **Black-Scholes-Merton** framework (1973).

The model assumes asset prices follow geometric Brownian motion:

$$
dS_t = \mu S_t \, dt + \sigma S_t \, dW_t
$$

where:
- $S_t$ = asset price
- $\mu$ = expected return
- $\sigma$ = **constant** volatility
- $W_t$ = Brownian motion

This breakthrough delivered a closed-form solution for European options and revolutionized financial economics.

However, its success also exposed its limitations.

---

### 3. The Constant Volatility Assumption

Black-Scholes assumes volatility is constant over time:

$$
\sigma_t = \sigma \quad \text{(for all } t\text{)}
$$

This implies uncertainty behaves the same during:
- Financial crises
- Stable bull markets
- Economic expansions
- Recessions
- Elections
- Wars
- Central bank announcements

**Reality contradicts this.** Volatility is highly dynamic.

---

### 4. The Emergence of Implied Volatility

Market data shows options imply a **volatility surface**, not a single number:

$$
\sigma = \sigma(K, T)
$$

where $K$ is strike and $T$ is maturity.

Volatility is **dynamic**, not constant.

---

### 5. The Volatility Smile

Empirical data reveals the famous **volatility smile**:


       Implied Volatility
              /\
             /  \
            /    \
-----------/------\-----------
         Strike Price


Deep in-the-money and out-of-the-money options carry higher implied volatility → indicating **heavier tails** than lognormal distribution assumes.

---

### 6. The Volatility Skew

Equity markets show strong asymmetry — the **volatility skew**:


Implied Volatility
   \
    \
     \
      \
       \
        \


Out-of-the-money puts trade at much higher implied vols than calls, reflecting fear of downside crashes.

---

### 7. Heavy-Tailed Returns

Black-Scholes assumes normal returns. Reality shows:

- Excess kurtosis
- Heavy tails
- Extreme events

$$
P(|X| > x) \quad \text{decays much slower than Gaussian}
$$

Events like 1987 Black Monday, 2008 Crisis, and 2020 COVID crash occur far more frequently than predicted.

---

### 8. Volatility Clustering

One of the strongest empirical facts:

**High volatility → High future volatility**  
**Low volatility → Low future volatility**

This persistence is a form of **market memory**.

---

### 9. The Leverage Effect

Negative returns increase future volatility more than positive returns of same size.

Mathematically:

$$
\text{Corr}(dS_t, dv_t) < 0
$$

This drives the volatility skew.

---

### 10. The Rise of Stochastic Volatility Models

Solution: Make volatility itself stochastic.

$$
dS_t = \mu S_t \, dt + \sqrt{v_t} S_t \, dW_t
$$

where $v_t$ follows its own stochastic process.

---

### 11. The Success of the Heston Model

The most famous stochastic volatility model:

$$
dv_t = \kappa(\theta - v_t) \, dt + \xi \sqrt{v_t} \, dZ_t
$$

It generates smiles, skews, mean reversion, and remains **affine** (tractable).

---

### 12. The Remaining Problem

Heston (and most classical models) use **only one variance factor**.


Market Information
        ↓
   Single Variance
        ↓
 Future Volatility
`

**Reality is multi-layered.**

---

### 13. Markets Possess Multiple Memories

Markets remember shocks across different time horizons:

- Minutes → High-frequency traders
- Days → Portfolio managers
- Weeks → Institutions
- Months → Structural changes

---

### 14. Multi-Horizon Volatility Persistence

A better view:

Short-Term Memory
        +
Medium-Term Memory
        +
Long-Term Memory


Each decays at different speeds.

---

### 15. Central Hypothesis of This Research

**Volatility should be modeled as the superposition of multiple memory processes.**

$$
v_t = \omega + \sum_{i=1}^{m} \alpha_i U_t^{(i)}
$$

where each $U_t^{(i)}$ represents a distinct memory horizon.

---

### 16. Why Affine Structure Matters

We preserve **affine structure** so the model remains computationally tractable despite added realism.

This enables efficient pricing, calibration, and sensitivity analysis via Riccati equations and Fourier methods.

---

### 17. Connecting Forecasting to Pricing

Volatility Forecast
          ↓
     Memory State
          ↓
Characteristic Function
          ↓
    Fair Option Value
          ↓
   Market Comparison
          ↓
    Mispricing Signal


---

### 18. Motivation for Indian Market Extension

Indian markets have unique features:
- Weekly expiries
- High open-interest concentration
- Put-call ratio signals
- RBI announcements
- Union Budget events
- Election volatility shocks

These are incorporated directly into the volatility dynamics.

---

## Conclusion

Financial markets do not have **one memory** — they have **many memories** operating simultaneously.

Classical models capture only fragments of this reality.

The goal of this framework is to build a mathematically rigorous, affine, multi-factor memory-driven model that respects real market behavior while remaining practical for pricing, calibration, and systematic mispricing detection.

---
