# SEC Filing Financial Analyzer

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TadK99/sec-filing-analyzer/blob/main/SEC_Filing_Financial_Analyzer.ipynb)

An automated equity-research tool that pulls structured **XBRL financial
data directly from the SEC EDGAR API** for any public company, cleans it,
and computes standard fundamental ratios — instead of manually digging
through 10-K/10-Q PDFs.

## What it does

1. Resolves stock tickers to SEC CIK numbers
2. Pulls each company's full XBRL filing history from SEC EDGAR (free, no API key)
3. Extracts revenue, net income, assets, equity, and other line items —
   handling the fact that different companies tag identical concepts under
   different XBRL tags
4. Deduplicates restated/comparative figures across filings
5. Computes margins, ROE, ROA, leverage, and liquidity ratios
6. Compares multiple companies side-by-side and tracks trends over time

## Why this matters

Every public company's financials are publicly available and standardized
via XBRL — but extracting them by hand, company by company, filing by
filing, is exactly the kind of repetitive work that should be automated.
This is the same structured-data layer that terminal vendors like Bloomberg
and FactSet are themselves built on top of.

## Sample output

| Revenue Trend | Ratio Comparison |
|---|---|
| ![revenue](outputs/revenue_trend.png) | ![ratios](outputs/ratio_comparison.png) |

## Tech stack

`Python` · `requests` (SEC EDGAR API) · `pandas` · `NumPy` · `matplotlib` / `seaborn`

## Run it yourself

**Option 1 — Colab (recommended):**
Click the badge above. **Before running:** edit `CONFIG["user_agent"]` in the
config cell to your real name + email — SEC requires this and will return
`403 Forbidden` without it.

**Option 2 — Local:**
```bash
git clone https://github.com/TadK99/sec-filing-analyzer.git
cd sec-filing-analyzer
pip install -r requirements.txt
jupyter notebook SEC_Filing_Financial_Analyzer.ipynb
```

## Configuration

Edit the `CONFIG` dict at the top of the notebook to change the companies
analyzed, the lookback window, or filing types (10-K vs 10-Q) — no engine
code needs to change.

## Project structure

```
sec-filing-analyzer/
├── SEC_Filing_Financial_Analyzer.ipynb
├── README.md
├── requirements.txt
└── outputs/
    ├── ratios_comparison_latest.csv
    ├── data_coverage.csv
    ├── revenue_trend.png
    ├── margin_trend.png
    └── ratio_comparison.png
```

## Possible extensions

- Add 10-Q quarterly data for more granular trend lines
- NLP sentiment analysis on the MD&A / Risk Factors text sections
- Automated peer-group / sector benchmarking
- Merge in live price data to add valuation ratios (P/E, EV/EBITDA)
- Streamlit front-end for one-click ticker lookups

## License

MIT
