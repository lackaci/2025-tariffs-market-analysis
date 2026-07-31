# US–China Stock Indexes During Trade Tensions (2025)

A quantitative analysis of how U.S. and Chinese equity markets, currency, commodities,
and volatility indexes responded to the 2025 tariff escalation between the U.S. and China.

## Overview

This project normalizes seven market indicators around the timeline of 2025 tariff
announcements, then compares them using **two correlation methods side by side**:
correlation on normalized price levels (captures whether assets trended together over
the whole episode) and correlation on daily log returns (the statistically rigorous
version, free of shared long-term drift). Reading the two together — rather than
picking one — surfaces which relationships are real and which were shared-drift
artifacts.

**Assets analyzed:**
- COFCO Tunhe Sugar Co. Ltd (Chinese commodity proxy)
- USD/CNY exchange rate
- Davis Commodities (Singapore-based, NASDAQ-listed)
- S&P 500
- Shanghai Composite
- CBOE Volatility Index (VIX)
- Hong Kong ETF (3037)

## Key Findings

- **Hong Kong's index and the VIX** show the strongest, most consistent relationship in
  the dataset (r ≈ -0.94 on price levels, -0.72 on returns) — a real, mechanistically
  plausible link, since Hong Kong equities are highly exposed to global risk sentiment.
- **Commodity proxies did not reliably hedge equity downside.** Davis Commodities'
  relationship with the VIX holds up directionally (-0.86 → -0.65) but weaker than it
  first appeared, and it moved *with*, not against, broader risk-off equity selloffs.
- **Several "striking" price-level correlations turned out to be statistical
  illusions.** COFCO Tunhe & VIX showed a near-perfect 0.90 correlation on price levels
  that collapsed to -0.05 on returns — a textbook case of two unrelated series merely
  drifting in the same direction, with no real economic link between a Chinese sugar
  producer and a U.S. volatility index.
- **S&P 500 and Shanghai Composite** were weakly linked by either method (0.40 on
  levels, 0.08 on returns), supporting genuine diversification value between U.S. and
  Chinese equities.

Full write-up, methodology discussion, and correlation heatmaps are in
[`notebooks/analysis.ipynb`](notebooks/analysis.ipynb).

## Project Structure

```
.
├── data/                # Input CSV price histories (not included, see below)
├── notebooks/
│   └── analysis.ipynb   # Main analysis notebook
├── requirements.txt
└── README.md
```

## Data

The notebook expects the following CSV files (exported from Investing.com) inside `data/`:

- `COFCO Tunhe Sugar Stock Price History.csv`
- `USD_CNY Historical Data.csv`
- `Davis Commodities Stock Price History.csv`
- `S&P 500 Historical Data.csv`
- `Shanghai Composite Historical Data.csv`
- `CBOE Volatility Index Historical Data.csv`
- `3037 ETF Stock Price History.csv`

These raw data files are not committed to this repository. Download the corresponding
historical price data from [Investing.com](https://www.investing.com) for the same date
range and place them in `data/`, or update `FILE_PATHS` at the top of the notebook to
point to your own copies.

## Methodology Note

The notebook deliberately computes correlation two ways rather than picking one:

- **Price-level correlation**, on the normalized (base-100) series, answers "did these
  assets trend together over the whole episode?" — useful for the regime-level story.
- **Log-return correlation**, on day-to-day percent changes, answers "do these assets
  actually move together on a given day?" — the more statistically sound measure, since
  price levels are non-stationary and can produce inflated or outright spurious
  correlations between series that simply drift in the same direction over time.

Where the two agree, the relationship is treated as real; where they diverge sharply,
the price-level number is treated with caution unless a plausible economic mechanism
supports it. See the notebook's "Correlation Insights" section for the full comparison
table and reasoning per asset pair.

## Setup

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/analysis.ipynb
```

## Sources

**Data & timeline:**
- [AP News – Trump tariffs timeline](https://apnews.com/article/tariffs-timeline-trade-war-trump-canada-mexico-china-a9d714eea677488ef9397547d838dbd0)
- [Investing.com – market news & historical data](https://www.investing.com/news/economy-news/us-futures-dip-trump-on-china-opec-output-in-focus--whats-moving-markets-4021219)

**Methodology (price levels vs. returns for correlation):**
- Yule, G. (1926). *Why Do We Sometimes Get Nonsense Correlations Between Time-Series?* Journal of the Royal Statistical Society.
- Granger, C. & Newbold, P. (1974). *Spurious Regressions in Econometrics.* Journal of Econometrics.
- [AMINDIS – Correlations: Index Prices vs Index Returns](https://www.amindis.com/knowledge/correlations-index-prices-vs-index-returns)
- [Understanding Financial Time Series: A Statistical Deep Dive](https://medium.com/@carlo.baroni.89/understanding-financial-time-series-a-statistical-deep-dive-cd4ea99d299c)

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.
