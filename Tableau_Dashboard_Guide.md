# Tableau Dashboard Add-On

## What was added

This project now includes Tableau-ready data files and a dashboard build guide.

Use these files in Tableau:

- `tableau_ready/merged_orders_tableau.csv`
- `tableau_ready/sales_target_tableau.csv`
- `tableau_ready/category_summary_tableau.csv`
- `tableau_ready/state_summary_tableau.csv`
- `tableau_ready/city_summary_tableau.csv`

A combined Excel source is also included:

- `Tableau_Data_Source.xlsx`

## Recommended Tableau dashboard

Dashboard name: **Sales and Profitability Dashboard**

Build these views:

1. KPI cards: Total Sales, Total Profit, Profit Margin, Orders
2. Sales by Category: `Category` vs `SUM(Amount)`
3. Profit Margin by Category: `Category` vs `SUM(Profit) / SUM(Amount)`
4. Top 5 States by Orders: `State` vs `COUNTD(Order ID)`, filtered to top 5
5. State Profitability Map: State colored by `SUM(Profit)` and sized by `SUM(Amount)`
6. Furniture Target Trend: Month vs `SUM(Target)` filtered to Furniture

## Tableau calculated fields

```text
Profit Margin = SUM([Profit]) / SUM([Amount])
```

```text
Average Profit per Order = SUM([Profit]) / COUNTD([Order ID])
```

```text
Sales per Order = SUM([Amount]) / COUNTD([Order ID])
```

```text
Furniture MoM Target Change =
(SUM([Target]) - LOOKUP(SUM([Target]), -1)) / LOOKUP(SUM([Target]), -1)
```

## How to explain this professionally

Excel Power Query was used to merge and prepare the data. PivotTables were used to validate category and regional summaries. Tableau was added for interactive visualization, including category performance, regional profitability, and Furniture target trends.
