# Superstore Sales & Profitability Dashboard (Power BI)

An interactive one-page dashboard analysing four years of retail sales (2023–2026) to show where growth is profitable and where it isn't.

## Business questions
1. Is the business growing, and is it growing profitably?
2. Which categories, products and regions drive profit?
3. Where is revenue high but profit low?

## Key findings
- Revenue grew 30% in 2025 and 21% in 2026; margin held around 13%.
- Technology and Office Supplies earn about 17% margin; Furniture earns 2.6%.
- Tables (-8.5%) and Bookcases (-3.1%) are loss-making overall.
- Central region margin is 7.9% vs 15% in the West.
- Order lines discounted above 20% lost about $136K in total.

## Tools and techniques
- **Power Query:** type fixes, derived Cost column, merge of Returns data
- **Data model:** star schema with Orders fact table and a Calendar date table
- **DAX:** revenue, profit, margin, orders, average order value, year-over-year growth
- **Visuals:** KPI cards, combo trend chart, category and region charts, Top 10 products, slicers with cross-filtering

## Key DAX measures
```DAX
Total Revenue = SUM(Orders[Sales])
Total Profit = SUM(Orders[Profit])
Total Cost = SUM(Orders[Cost])
Profit Margin % = DIVIDE([Total Profit], [Total Revenue])
Total Orders = DISTINCTCOUNT(Orders[Order ID])
Avg Order Value = DIVIDE([Total Revenue], [Total Orders])
Revenue PY = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR('Calendar'[Date]))
YoY Growth % = IF(HASONEVALUE('Calendar'[Year]),
    DIVIDE([Total Revenue] - [Revenue PY], [Revenue PY]))
```

## Files
- `dashboard/Superstore Dashboard.pbix`: the Power BI file (open with Power BI Desktop)
- `data/sample_-_superstore.xls`: source data (Superstore sample dataset)

## Notes
The discount finding shows an association, not proof of cause.
