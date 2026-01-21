# 📊 Value at Risk (VaR) & Expected Shortfall (ES)

This project explores **three standard approaches** to calculating **Value at Risk (VaR)** and **Expected Shortfall (ES)** for a financial portfolio using Python. These risk metrics are central to portfolio management, regulatory compliance, and downside-risk assessment.

---

## 🔍 What Are VaR and ES?

### **Value at Risk (VaR)**
VaR estimates the **maximum expected loss** over a given time horizon at a specified confidence level.

> **Example:**  
> If the 95% daily VaR is $10,000, there is a 95% probability that the portfolio will **not** lose more than $10,000 in one day.

---

### **Expected Shortfall (ES)**
Expected Shortfall (also called Conditional VaR) measures the **average loss given that the VaR threshold has been breached**.

ES captures **tail risk**, making it more informative than VaR during extreme market events.

---

## 🧮 Methods Implemented

This project implements and compares three commonly used VaR/ES methodologies:

### 1️⃣ Empirical (Historical) Method
- Uses historical returns directly  
- No distributional assumptions  
- VaR is computed using empirical quantiles  
- ES is the mean of returns beyond the VaR cutoff  

**Pros:** Faithful to historical behavior  
**Cons:** Limited by historical data and regime changes  

---

### 2️⃣ Normal Estimation Method
- Assumes portfolio returns are normally distributed  
- Uses analytical formulas based on mean and standard deviation  
- Fast and computationally efficient  

**Pros:** Simple and fast  
**Cons:** Underestimates tail risk when returns exhibit fat tails  

---

### 3️⃣ Monte Carlo Simulation
- Simulates thousands of future return paths  
- Preserves asset correlations using covariance and Cholesky decomposition  
- Computes VaR/ES from simulated outcomes  

**Pros:** Flexible, forward-looking, excellent for stress testing  
**Cons:** Computationally intensive and assumption-dependent  

---

## ⏱ Time Horizon

- All calculations are performed on a **single-day horizon**  
- Multi-day VaR/ES is intentionally excluded, as it is less common in professional risk practice  

---

## 📦 Project Structure

### Key Libraries Used
```python
yfinance
pandas
numpy
scipy
matplotlib
seaborn
```

## ⚙️ Portfolio Construction

Portfolios are defined using asset weights that sum to 1.

### Example:
```python
portfolio_weights = {
    "SPY": 0.25,
    "IWM": 0.10,
    "EFA": 0.05,
    "TLT": 0.15,
    "IEF": 0.05,
    "VBTIX": 0.10,
    "ABNFX": 0.10,
    "FXE": 0.25,
    "FXY": 0.20
}
```

## 📈 Data Generation

- Historical closing prices are pulled via `yfinance`
- Lookback period: **~2 years**
- Returns are calculated as **log returns**

## 📉 Empirical VaR & ES Calculation

The empirical (historical) approach follows these steps:

1. Normalize portfolio weights  
2. Compute weighted portfolio returns  
3. Calculate VaR using the empirical quantile  
4. Compute ES as the average of returns beyond VaR  
5. Convert return-based metrics into **dollar losses**

### Example Output
```python
VaR (95%):  5.87%
ES  (95%):  8.74%
VaR ($):    $56,997
ES  ($):    $91,306
```
## 📊 Portfolio Value & Loss Visualization

- Portfolio value is constructed via cumulative log returns  
- Start and end portfolio values are annotated  
- Loss events beyond VaR are isolated and counted  
- Histogram of returns is plotted alongside:
  - Fitted normal distribution  
  - Empirical VaR cutoff  
  - Normal-based VaR cutoff  

This allows for a **visual comparison of tail behavior** between empirical and normal assumptions.

## 📌 Key Takeaways

- **Empirical VaR** is most faithful to observed market behavior  
- **Normal VaR** is fast but risks underestimating extreme losses  
- **Monte Carlo VaR** is forward-looking and ideal for scenario analysis  

While each method has it's benefits and drawbacks, calculating all three and using the average can be a good way
to reduce errors and confirm that each method is returning resonable outputs.

---

## 📊 Method Comparison

| Method | Strengths | Weaknesses |
|------|----------|------------|
| Empirical | No assumptions, data-driven | Limited by historical regimes |
| Normal | Fast, intuitive | Underestimates tail risk |
| Monte Carlo | Flexible, forward-looking | Computationally expensive |

## 📚 References

- https://www.youtube.com/watch?v=6-dhdMDiYWQ  
- https://medium.com/analytics-vidhya/monte-carlo-simulations-for-predicting-stock-prices-python-a64f53585662  
- https://www.forrs.de/en/news/var-vs-es  

