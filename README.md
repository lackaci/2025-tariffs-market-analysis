# US–China Stock Indexes During Trade Tensions (2025)

A quantitative analysis of how U.S. and Chinese equity markets, currency, commodities,
and volatility indexes responded to the 2025 tariff escalation between the U.S. and China.

## Overview

This project normalizes and compares seven market indicators around the timeline of 2025
tariff announcements, then computes a correlation matrix to identify which assets moved
together (or against each other) during the trade war.

**Assets analyzed:**
- COFCO Tunhe Sugar Co. Ltd (Chinese commodity proxy)
- USD/CNY exchange rate
- Davis Commodities (Singapore-based, NASDAQ-listed)
- S&P 500
- Shanghai Composite
- CBOE Volatility Index (VIX)
- Hong Kong ETF (3037)

## Key Findings

- Commodity proxies underperformed and did **not** hedge equity downside as expected.
- The VIX and the Hong Kong index showed the strongest inverse relationship (r ≈ -0.94),
  suggesting Hong Kong equities are highly sensitive to global risk sentiment.
- The S&P 500 and Shanghai Composite were only weakly correlated (r ≈ 0.24), reflecting
  largely independent regional drivers during the trade tensions.

Full write-up, charts, and correlation heatmap are in [`notebooks/analysis.ipynb`](notebooks/analysis.ipynb).

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
range and place them in `data/`, or point `file_paths` in the notebook to your own copies.

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

- [AP News – Trump tariffs timeline](https://apnews.com/article/tariffs-timeline-trade-war-trump-canada-mexico-china-a9d714eea677488ef9397547d838dbd0)
- [Investing.com – market news & historical data](https://www.investing.com/news/economy-news/us-futures-dip-trump-on-china-opec-output-in-focus--whats-moving-markets-4021219)

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.
