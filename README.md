# 📊 Factor Model Portfolio Optimizer

> A quantitative portfolio construction tool built on the **Fama-French 3-Factor Model**, 
> deployed as a fully interactive web application on the Nifty 50 universe.

🔗 **[Launch Live App](https://portfolio-construction---factor-model-95qos8gfhft3fkcqnqfius.streamlit.app/)**

---

## 🧠 What is this?

This tool helps you build a **factor-driven equity portfolio** from the Nifty 50 universe.
Instead of picking stocks based on intuition, you define *how much market risk, size exposure,
and value tilt* you want — and the optimizer finds the best portfolio that satisfies those targets.

The entire workflow — from exploring factor trends to running a backtest and analyzing results —
lives inside a single interactive Streamlit app.

---

## ⚙️ How the Optimization Works (High Level)

The optimizer uses **Mixed-Integer Linear Programming (MILP)** to construct a portfolio that:

- 🎯 Hits your **target factor exposures** (Market, Size, Value) within a defined tolerance
- 📦 Respects a **maximum number of stocks** you want to hold
- ⚖️ Caps **individual position sizes** so no single stock dominates
- 🔁 Limits **portfolio turnover** at each rebalance to control transaction costs
- 🏭 Enforces **sector-level constraints** — min/max stocks per sector, or full sector exclusion

Betas are estimated using **rolling OLS regression** on the in-sample lookback window.
The portfolio is then evaluated **out-of-sample** and rebalanced whenever factor exposures
drift beyond your tolerance bands.

---

## 🖥️ App Features

### 📐 Beta Explorer
Before running anything, understand the factor landscape:
- Bar charts of monthly **MF, SMB, HML** returns over your lookback window
- Factor statistics table — annualized return, volatility, Sharpe
- **Achievable beta range calculator** — tells you exactly which target betas are
  feasible given your position constraints, before you waste time on an infeasible backtest

### 🏭 Sector Dynamics
A full sector health dashboard as of any date you choose:

| Metric | What it tells you |
|--------|------------------|
| 📈 12M Return | How the sector performed over the past year |
| 📉 3M Return | Recent performance |
| ⚡ Momentum | Accelerating if recent > longer-term trend |
| 🌊 Ann. Volatility | How choppy the sector has been |
| ✅ Positive Months | How consistently it delivered positive returns |
| 🔢 MF Beta | How sensitive the sector is to broad market moves |

Plus **cumulative return trend charts** for every sector side by side — small, clean,
colour-coded green/red so you can scan across all sectors in seconds.

### 📊 Run Backtest
Configure everything in the sidebar and hit one button:
- Choose your **as-of date and lookback period**
- Set **target betas and tolerances** for Market, SMB, and HML
- Toggle **turnover cap** and **sector constraints**
- Watch the portfolio get built and rebalanced month by month

### 📈 Results
- **Portfolio vs Nifty 50** value chart over the entire backtest period
- Monthly returns bar chart side by side
- Full **rebalancing log** — see exactly what the portfolio held and what factor
  exposures it had at every rebalance date
- **Composition table** — weights per stock across all periods

### 🔍 Risk Analysis
Run a **sensitivity sweep** across multiple risk aversion values in one click.
Compare how aggressive vs conservative parameterizations performed on the same period.

---

## 🎮 How to Use the App

**Step 1** — Set your **as-of date** and **lookback period** in the sidebar

**Step 2** — Visit **Beta Explorer** to see what factor environment you're working in
and check that your target betas are achievable

**Step 3** — Visit **Sector Dynamics** to understand which sectors are trending,
accelerating, or worth excluding from your portfolio

**Step 4** — Set your **target betas, constraints, and sector limits** in the sidebar

**Step 5** — Go to **Run Backtest** and click ▶️

**Step 6** — Analyze your results in the **Results** and **Risk Analysis** tabs

---

## 🏗️ Built With

| Tool | Purpose |
|------|---------|
| 🐍 Python | Core language |
| 📊 Streamlit | Interactive web app |
| 🔢 PuLP / CBC | MILP optimization solver |
| 🐼 Pandas & NumPy | Data processing |
| 📉 Matplotlib | Charts and visualizations |
| 🔬 SciPy | Statistical regression |

---

## 📌 Key Design Decisions

- **In-sample / out-of-sample split** — betas are estimated on historical data,
  portfolio is evaluated on unseen future periods. No lookahead bias.
- **Breach-triggered rebalancing** — portfolio only rebalances when factor exposures
  drift outside tolerance, not on a fixed calendar. Reduces unnecessary turnover.
- **Sector constraints via MILP** — sector limits are hard constraints in the optimizer,
  not post-hoc filters. The optimizer respects them while maximizing returns.
- **Equal-weighted sector benchmarks** — Sector Dynamics uses equal-weighted averages
  so large-cap stocks don't dominate the sector signal.

---

## 🌐 Live App

👉 **[https://portfolio-construction---factor-model-95qos8gfhft3fkcqnqfius.streamlit.app/](https://portfolio-construction---factor-model-95qos8gfhft3fkcqnqfius.streamlit.app/)**

---

*Built on the Nifty 50 universe | Fama-French 3-Factor Model | March 2026*

