# Sales and Profitability Analysis Project

## Project Overview

This project analyzes sales, profitability, target achievement, and regional performance using Excel and Tableau. The work is divided into two main parts:

- Excel analysis using Power Query-style data preparation, PivotTable-style summaries, and formulas
- Tableau dashboard setup for visual storytelling and interactive reporting

The original dataset contains three sheets:

- `List of Orders`
- `Order Details`
- `Sales Target`

## Objective

The objective of this project is to understand:

- Which product categories generate the highest sales
- Which categories are most and least profitable
- How Furniture sales targets change month-over-month
- Which states have the highest order count
- Which regions or cities need improvement
- How the final insights can be visualized in Tableau

## Excel Workflow

### 1. Data Preparation

The first step was to merge `Order Details` with `List of Orders` using `Order ID` as the common key.

This was necessary because:

- `Order Details` contains `Amount`, `Profit`, `Quantity`, `Category`, and `Sub-Category`
- `List of Orders` contains `Order Date`, `State`, `City`, and `CustomerName`

After merging, the final analysis table includes all required fields in one place.

Recommended Excel method:

```text
Power Query → Merge Queries → Match on Order ID → Expand required columns
```

Expanded columns:

- `Order Date`
- `State`
- `City`
- `CustomerName`

## Excel Analysis

### Part 1: Sales and Profitability Analysis

Using the merged table, category-level analysis was created.

Metrics calculated:

- Total Sales
- Total Profit
- Distinct Order Count
- Average Profit per Order
- Profit Margin

Formulas used:

```text
Average Profit per Order = Total Profit / Distinct Order Count
```

```text
Profit Margin = Total Profit / Total Sales
```

Key results:

| Category | Total Sales | Total Profit | Avg Profit / Order | Profit Margin |
|---|---:|---:|---:|---:|
| Electronics | 165,267 | 10,494 | 51.44 | 6.35% |
| Clothing | 139,054 | 11,163 | 28.40 | 8.03% |
| Furniture | 127,181 | 2,298 | 12.35 | 1.81% |

Insights:

- Electronics has the highest total sales.
- Clothing has the strongest profitability because it has the highest profit margin.
- Furniture is the weakest category because its profit margin is very low.
- The Tables sub-category is a major reason for Furniture underperformance.

### Part 2: Target Achievement Analysis

The `Sales Target` sheet was used to analyze Furniture targets month-over-month.

Steps:

1. Filter `Category` to `Furniture`
2. Sort by `Month of Order Date`
3. Calculate month-over-month percentage change

Formula:

```text
MoM % Change = (Current Month Target - Previous Month Target) / Previous Month Target
```

Important result:

```text
April 2025 target dropped by 11.86%
```

Insight:

Furniture targets are mostly stable, but April 2025 shows a major drop. This may indicate seasonality, weaker expected performance, or a correction in target planning.

Recommended strategy:

- Use rolling actual sales trends
- Consider seasonality
- Review low-margin Furniture sub-categories
- Set targets based on both sales and profitability, not only revenue

### Part 3: Regional Performance Insights

The merged table was used to analyze regional performance because state and city details come from `List of Orders`, while sales and profit come from `Order Details`.

Top 5 states by order count:

| State | Orders | Total Sales | Total Profit | Avg Profit / Order | Profit Margin |
|---|---:|---:|---:|---:|---:|
| Madhya Pradesh | 101 | 105,140 | 5,551 | 54.96 | 5.28% |
| Maharashtra | 90 | 95,348 | 6,176 | 68.62 | 6.48% |
| Rajasthan | 32 | 21,149 | 1,257 | 39.28 | 5.94% |
| Gujarat | 27 | 21,058 | 465 | 17.22 | 2.21% |
| Punjab | 25 | 16,786 | -609 | -24.36 | -3.63% |

Insights:

- Madhya Pradesh has the highest order count.
- Maharashtra has stronger profitability than Madhya Pradesh despite fewer orders.
- Punjab is a concern because it is in the top 5 by order count but has negative profit.
- Gujarat also needs attention because its profit margin is low.

Priority improvement areas:

- Punjab / Chandigarh
- Gujarat / Ahmedabad
- Rajasthan / Jaipur
- Andhra Pradesh / Hyderabad
- Tamil Nadu / Chennai

## Why These Methods Were Used

| Task | Method Used | Reason |
|---|---|---|
| Merge order and sales data | Power Query | Clean, repeatable, refreshable method |
| Summarize category and state performance | PivotTables | Best for grouped totals and counts |
| Calculate profit margin | Formula | Custom ratio calculation |
| Calculate average profit per order | Formula | Avoids misleading row-level averages |
| Calculate month-over-month change | Formula | Compares each month with the previous month |
| Visualize insights | Tableau | Better for dashboarding and storytelling |

## Tableau Dashboard

Tableau was added to turn the Excel analysis into a visual dashboard.

Main Tableau data source:

```text
Tableau_Data_Source.xlsx
```

Recommended sheet to start with:

```text
Merged Orders
```

Other useful sheets:

- `Sales Target`
- `Category Summary`
- `State Summary`
- `City Summary`

## Tableau Dashboard Layout

Dashboard name:

```text
Sales and Profitability Dashboard
```

Recommended layout:

### Top Row: KPI Cards

- Total Sales
- Total Profit
- Total Orders
- Profit Margin

### Middle Row: Category Performance

- Sales by Category
- Profit Margin by Category

### Bottom Row: Regional Performance

- Top 5 States by Orders
- State Profitability Map

### Additional View

- Furniture Target Trend

## Tableau Charts To Build

### 1. Sales by Category

Fields:

- `Category` → Columns
- `Amount` → Rows

Aggregation:

```text
SUM(Amount)
```

Purpose:

Shows which category has the highest sales.

### 2. Profit Margin by Category

Calculated field:

```text
Profit Margin = SUM([Profit]) / SUM([Amount])
```

Fields:

- `Category` → Columns
- `Profit Margin` → Rows

Format:

```text
Percentage
```

Purpose:

Shows which category is most profitable.

### 3. Top 5 States by Orders

Fields:

- `State` → Rows
- `Order ID` → Columns

Aggregation:

```text
COUNTD(Order ID)
```

Filter:

```text
Top 5 by Count Distinct of Order ID
```

Purpose:

Shows the states with the highest number of unique orders.

### 4. State Profitability Map

Fields:

- `State` → Map location
- `Amount` → Size
- `Profit` → Color

Aggregations:

```text
SUM(Amount)
SUM(Profit)
```

Purpose:

Shows regional sales concentration and profitability differences.

### 5. Furniture Target Trend

Use the `Sales Target` sheet.

Fields:

- `Month of Order Date` → Columns
- `Target` → Rows
- `Category` → Filter → Furniture

Mark type:

```text
Line
```

Purpose:

Shows monthly target movement for Furniture.

## Tableau Calculated Fields

### Profit Margin

```text
SUM([Profit]) / SUM([Amount])
```

### Average Profit per Order

```text
SUM([Profit]) / COUNTD([Order ID])
```

### Sales per Order

```text
SUM([Amount]) / COUNTD([Order ID])
```

### Furniture MoM Target Change

```text
(SUM([Target]) - LOOKUP(SUM([Target]), -1)) / LOOKUP(SUM([Target]), -1)
```

## Final Dashboard Insights

- Electronics leads in total sales.
- Clothing has the best profitability margin.
- Furniture underperforms due to low margin, especially because of Tables.
- April 2025 shows the largest Furniture target fluctuation.
- Madhya Pradesh has the highest order count.
- Maharashtra is stronger in profitability among the top states.
- Punjab requires attention because it has high order volume but negative profit.

## Final Project Description

This project uses Excel and Tableau to analyze sales, profitability, target achievement, and regional performance. Excel was used for data preparation, merging, validation, PivotTable summaries, and formula-based calculations. Tableau was used to create a visual dashboard highlighting category performance, Furniture target trends, and regional profitability insights.

## Files Included

- `The Bridge Assignment 1.xlsx` - Original dataset
- `Professional_Sales_Profitability_Project_with_Tableau.xlsx` - Final Excel project with Tableau planning sheets
- `Tableau_Data_Source.xlsx` - Tableau-ready data source
- `Tableau_Ready_Files.zip` - Packaged Tableau-ready files
- `Tableau_Dashboard_Guide.md` - Tableau dashboard setup guide
- `README_Sales_Profitability_Project.md` - Full project README

