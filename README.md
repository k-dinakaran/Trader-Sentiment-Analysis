# Trader Sentiment Analysis

## Objective
Analyze how trader performance and behavior change across Fear vs Greed sentiment regimes and derive actionable strategy insights.

---

## Methodology
- Cleaned and aligned datasets at daily level.
- Engineered key metrics:
  - Daily PnL per trader
  - Win rate
  - Trade frequency
  - Leverage distribution
  - Long/Short ratio
- Compared performance between Fear and Greed regimes.
- Segmented traders by leverage, frequency, and consistency.

---

## Key Insights
1. Performance differs between Fear and Greed market conditions.
2. High-leverage traders show higher volatility during Fear regimes.
3. Trader behavior (frequency and position bias) shifts based on sentiment.

---

## Strategy Recommendations
1. Reduce leverage exposure during Fear regimes for high-risk traders.
2. Increase trade frequency selectively during Greed regimes for consistent performers.

---

## Setup

Install required libraries:

pip install pandas numpy matplotlib seaborn scipy scikit-learn

---

## How to Run

1. Place the following files in the project directory:
   - fear_greed_index.csv
   - historical_data.csv

2. Open `trader_sentiment_analysis.ipynb`

3. Run all cells sequentially.
