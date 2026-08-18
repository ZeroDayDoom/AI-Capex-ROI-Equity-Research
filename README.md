# Microsoft (MSFT) AI Capex ROI — DCF & Equity Research

A simplified discounted cash flow model and equity research report testing whether Microsoft's
current share price is justified by its AI infrastructure spending, built on real Q4 FY2026 earnings
data from Microsoft and Amazon.

**Finding:** Under base-case assumptions, the model implies a fair value of **~$337/share** against
a current price of **~$500** — roughly **32% downside**. Even a bull-case scenario (faster margin
expansion, quicker capex normalization) implies **~$399**, still below market. The current price only
clears the model in its most optimistic scenario (8.0% WACC + 4.5% terminal growth).

📄 [**Read the full report**](report/MSFT_AI_Capex_ROI_Equity_Research_Report.pdf)
📊 [**Open the model**](model/MSFT_AI_Capex_ROI_Model.xlsx)

![Capex vs Revenue Growth](figures/chart1_capex_vs_revenue_growth.png)
![Sensitivity Heatmap](figures/chart2_sensitivity_heatmap.png)

---

## Why this project

Every hyperscaler earnings call in 2026 has circled the same question: is AI infrastructure capex
generating returns, or running ahead of monetization? Microsoft's FY2026 capex grew **79.6% YoY**
while revenue grew **17.8%** — this project builds a real (if simplified) valuation framework to test
whether the market is already pricing in a favorable resolution of that gap.

## Methodology

- **Base year:** FY2026A actuals (revenue, operating income, capex — all as reported)
- **Forecast window:** FY2027E–FY2031E, unlevered free cash flow
- **Revenue growth:** decelerates from 15% to 7% across the forecast
- **Operating margin:** dips in FY2027 as capex weighs on margins, recovers to 47% by FY2031
- **Capex intensity:** normalizes from 34.9% of revenue (FY2026A peak) toward a 20% long-run level
- **Discounting:** 9.0% WACC, 3.5% terminal growth (Gordon Growth)
- **Cross-check:** benchmarked against Amazon/AWS on capex intensity, cloud margin, and growth

Full assumption-by-assumption sourcing is in the report (Section 3.1) and in the Excel model's
`Assumptions` tab (every hardcoded input has an adjacent source citation).

## Key assumptions & limitations

- This is a **company-level DCF, not a segment-level one** — Microsoft doesn't disclose Azure's
  standalone operating margin, so the model can't isolate cloud/AI profitability the way Amazon's
  AWS segment reporting allows.
- FY2027E–FY2031E growth, margin, and capex-intensity figures are **my own projections**, not
  company guidance (Microsoft gave only one quarter of forward guidance).
- WACC and terminal growth are standard analyst assumptions, not derived from a formal beta/CAPM
  calculation — see the sensitivity table for how much the output depends on them.
- Net working capital changes and stock-based compensation dilution are assumed away for simplicity.

## Repo structure

```
├── report/
│   ├── MSFT_AI_Capex_ROI_Equity_Research_Report.pdf   # Full 5-page report
│   └── report.tex                                     # LaTeX source
├── model/
│   └── MSFT_AI_Capex_ROI_Model.xlsx                   # Formula-driven DCF (0 errors)
├── figures/
│   ├── chart1_capex_vs_revenue_growth.png
│   └── chart2_sensitivity_heatmap.png
├── src/
│   ├── build_model.py                                 # Builds the Excel model (openpyxl)
│   └── make_charts.py                                 # Generates both charts (matplotlib)
└── README.md
```

## Data sources

- Microsoft Corp., Q4 FY2026 earnings release & call transcript (July 29, 2026)
- Microsoft Corp., FY2025 Form 10-K and Annual Report (SEC EDGAR)
- Microsoft Corp., Q1 & Q3 FY2026 earnings releases (SEC EDGAR, Form 8-K exhibits)
- Amazon.com Inc., Q2 2026 earnings release & call transcript (July 30, 2026)
- Market data (price, market cap, P/E, EV/EBITDA, ROIC): FinanceCharts, GuruFocus, StockAnalysis.com,
  CompaniesMarketCap (week of Aug 11–18, 2026)

All FY2026A/Q2 2026 figures used as model inputs are real reported numbers. Forecast-period figures
(FY2027E onward) are this analyst's own projections built on top of that base — see *Limitations*
above.

## Running it yourself

```bash
pip install openpyxl matplotlib
python src/build_model.py      # outputs model/MSFT_AI_Capex_ROI_Model.xlsx
python src/make_charts.py      # outputs figures/*.pdf
```

## Disclaimer

This is a practice equity research exercise for portfolio purposes. It is not investment advice and
is not a research product of any broker-dealer. Forward-looking projections and the resulting
valuation are the author's own analysis and do not represent guidance from Microsoft or Amazon
management.
