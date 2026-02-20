# Trader Sentiment Analysis

Analyzing Hyperliquid on-chain perpetual trading behavior against the Crypto Fear & Greed Index.  
A full pipeline covering data preparation, statistical analysis, trader segmentation, behavioral clustering, and actionable trading rules.

---

## 📌 Project Overview

This project investigates whether crypto market sentiment (measured by the Fear & Greed Index) meaningfully affects trader performance and behavior on **Hyperliquid**, a decentralized perpetuals exchange.

### Questions Answered

1. Does PnL / win rate / drawdown differ between Fear vs Greed days?
2. Do traders change leverage, frequency, or long/short bias with sentiment?
3. Which trader segments profit most in each sentiment regime?
4. What actionable rules can traders follow based on sentiment signals?

---

## 📁 Datasets

| Dataset | Description | Source |
|---------|------------|--------|
| `fear_greed_index.csv` | Daily Fear & Greed scores (0–100) + classification | alternative.me |
| `historical_data.csv` | Hyperliquid on-chain trade history (211K+ rows, 32 traders, 16 columns) | Hyperliquid Exchange |

⚠️ Data files are **not committed** to this repository (size/privacy reasons).

---

## ⚙️ Setup & How to Run

### 1️⃣ Install Required Libraries

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn

## 2️⃣ Add Dataset Files

Place the following files in the project directory:

- `fear_greed_index.csv`
- `historical_data.csv`

---

## 3️⃣ Run the Notebook

Open:


Run all cells sequentially.

---

# 🔬 Analysis Pipeline

---

## Part A — Data Preparation

- Load both datasets with full EDA (shape, dtypes, nulls, duplicates)
- Convert Unix millisecond timestamps → UTC dates
- Filter to perpetual-only trade directions
- Engineer key metrics per trader per day

### Engineered Metrics

| Metric | Description |
|--------|------------|
| `daily_pnl` | Sum of closed PnL per account per day |
| `win_rate` | % of winning (PnL > 0) trades |
| `avg_leverage` | Leverage proxy = Size USD / (Start Position × Exec Price) |
| `n_trades` | Number of trades per day |
| `ls_ratio` | Long count / Short count |
| `pnl_cv` | Coefficient of variation of daily PnL (consistency) |
| `max_drawdown` | Rolling cumulative max-drawdown proxy |

---

## Part B — Analysis

### B1 — Performance by Sentiment

- Mean / median daily PnL, win rate, drawdown by Fear / Neutral / Greed
- Mann-Whitney U tests with effect sizes (rank-biserial r)

---

### B2 — Behavioral Changes

- Leverage differences across regimes
- Trade frequency shifts
- Position size variation
- Long/Short bias changes
- Statistical testing for all comparisons

---

### B3 — Trader Segmentation (3 Segments)

| Segment | Method | Labels |
|---------|--------|--------|
| Leverage | Tercile split on avg leverage proxy | Low / Mid / High |
| Frequency | Tercile split on trades per day | Infrequent / Moderate / Frequent |
| Consistency | Tercile split on PnL coefficient of variation | Consistent / Moderate / Inconsistent |

---

# 📊 Visualizations (10 Figures)

- fig1 — Fear & Greed Index full history timeline  
- fig2 — Daily PnL distributions by sentiment  
- fig3 — Win rate & drawdown by sentiment  
- fig4 — Behavior metrics (2×2 grid)  
- fig5 — Segment × Sentiment PnL heatmaps  
- fig6 — Leverage distribution: Fear vs Greed overlay  
- fig7 — Top-10 traders + win rate vs PnL scatter  
- fig8 — Daily aggregate PnL overlaid with F&G score  
- fig9 — K-Means elbow curve + cluster scatter  
- fig10 — Gradient Boosting feature importances  

---

# 🤖 Bonus — ML Components

## K-Means Behavioral Clustering

- Features: avg leverage, trades/day, win rate, position size, PnL CV
- StandardScaler normalization
- Elbow-curve selection
- 4 behavioral archetypes identified

---

## Profitability Prediction Model

- Target: Is today's trader PnL positive?
- Algorithm: Gradient Boosting (GBM)
- Validation: Leave-One-Date-Out Cross Validation (prevents data leakage)
- Features:
  - Trade frequency
  - Leverage
  - Win rate
  - Position size
  - Long/Short ratio
  - Fear & Greed score

---

# 📈 Key Findings

- Fear days show statistically higher median daily PnL than Greed days (p < 0.001, effect size r ≈ -0.58) — potential contrarian edge.
- Traders use significantly higher leverage on Greed days (p < 0.01).
- Trade frequency increases significantly on Fear days (p < 0.001).
- Long/Short ratio increases during Greed regimes — stronger long bias.
- Consistent traders (low PnL CV) outperform across all sentiment regimes.

---

# 🧠 Strategy Implications

- Reduce leverage exposure during Greed regimes where risk-taking behavior spikes.
- Consider contrarian positioning during Fear regimes.
- Prioritize low-variance (consistent) traders for capital allocation.
- Monitor leverage expansion as a sentiment-driven risk signal.

---

# 🤝 Contributing

Pull requests are welcome.  
For major changes, please open an issue first to discuss proposed improvements.
