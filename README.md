# Costco Business Analysis (2019–2025)

> **Disclaimer – Training Project**
> This project was built **for practice and learning purposes only**, to develop data analysis and dashboarding skills.
> The datasets are **illustrative and approximate**. They are **not official Costco figures**, have not been verified
> against Costco's financial filings, and may contain inaccuracies or inconsistencies (see [Data Limitations](#data-limitations)).
> Do **not** use these numbers for investment, business, or academic decisions.

---

## 1. Purpose

The goal of this project is to practice the full analysis workflow on a small, realistic business dataset:

1. Load and inspect multiple related tables
2. Build a simple data model and DAX measures in Power BI
3. Design a one-page KPI dashboard
4. Extract business insights from trends, ratios, and segments
5. Critically evaluate data quality and the limits of what the data can support

---

## 2. Project Files

| File | Description |
|---|---|
| `Costco_dashboard.pbix` | Power BI dashboard (1 page, 10 visuals) |
| `costco_memberships.csv` | Yearly membership counts, executive share, and renewal rates (2019–2025) |
| `costco_demographics.csv` | Shopper profile: income, gender, generation, average visits |
| `costco_sales_categories.csv` | Qualitative importance rating for each product category |
| `costco_financials_and_stores` *(embedded in the .pbix)* | Yearly revenue, membership income, store count, e-commerce growth |

### Data dictionary

**costco_financials_and_stores** (embedded)
- `Year`, `Revenue_Billion_USD`, `Membership_Income_Billion_USD`, `Stores_Worldwide`, `Ecommerce_Growth_%`

**costco_memberships**
- `Year`, `Paid_Members_Millions`, `Executive_Members_Millions`, `Exec_Percent`, `Renewal_US_CA_%`, `Renewal_World_%`

**costco_demographics**
- `Segment`, `Percent_of_Shoppers` (one row, "Avg visits per year", is a count rather than a percentage)

**costco_sales_categories**
- `Category`, `Sales_Importance` (Very High → Low-Medium), `Notes`

---

## 3. Data Model & Measures

The model has four tables. The main relationship connects the yearly tables on `Year`; the demographics and category tables are standalone lookups.

| Measure | Logic |
|---|---|
| `Total Revenue` | Sum of `Revenue_Billion_USD` |
| `Total Membership Income` | Sum of `Membership_Income_Billion_USD` |
| `Revenue YoY %` | Current year vs. previous year revenue |
| `Total Members` | Sum of `Paid_Members_Millions` |
| `Members YoY %` | Current year vs. previous year members |
| `Avg Exec %` | Average of `Exec_Percent` |
| `Importance_Score_Num` | Maps the text rating to a score (Very High = 5 … Medium = 2, otherwise 1) |
| `Category Rank` | Ranks categories by importance score |

### Dashboard layout

- **KPI cards:** Revenue, Membership Income, Members, Stores
- **Combo chart:** Stores worldwide (columns) vs. e-commerce growth (line), by year
- **Line chart:** Membership income vs. executive members, by year
- **Bar chart:** Executive membership share, by year
- **Column chart:** Category importance score
- **Donut + bar chart:** Shopper demographic segments

---

## 4. Analysis & Key Findings

### 4.1 Revenue growth is strong, with one slowdown

Revenue rose from **$152.7B (2019)** to **$269.9B (2025)**, about **+77%** overall, or roughly **10% CAGR**.

| Year | Revenue ($B) | YoY growth |
|---|---|---|
| 2019 | 152.7 | – |
| 2020 | 166.8 | +9.2% |
| 2021 | 195.9 | +17.4% |
| 2022 | 226.9 | +15.8% |
| 2023 | 242.3 | +6.8% |
| 2024 | 249.6 | +3.0% |
| 2025 | 269.9 | +8.1% |

**Insight:** Growth peaked in 2021–2022 (a period of pandemic-driven demand and inflation), slowed sharply in 2024, and recovered in 2025.

### 4.2 The membership model is the core of the business

| Metric | 2019 | 2025 | Change |
|---|---|---|---|
| Members (millions) | 98.5 | 145.0 | +47% |
| Membership income ($B) | 3.35 | 5.30 | +58% |
| Income per member | ~$34 | ~$37 | +8% |
| Renewal rate (US & Canada) | 90.0% | 92.3% | +2.3 pts |
| Renewal rate (World) | 88.0% | 89.8% | +1.8 pts |

**Insights:**
- Membership income grew faster than the member count, which points to fee increases and/or a richer membership mix.
- Renewal rates are consistently high and improving slowly, which signals strong loyalty and predictable recurring revenue.
- Membership income is only about **2%** of revenue (2.2% in 2019, 2.0% in 2025), but it is a stable, high-margin stream that supports low product markups.

### 4.3 Expansion and store productivity

- Stores grew from **785 to 923** (+138, about +18%).
- Revenue per store rose from about **$195M to $292M** (**+50%**).

**Insight:** Growth is not driven only by opening new warehouses. Each warehouse is also selling significantly more, which suggests higher traffic, larger baskets, and/or price inflation.

### 4.4 E-commerce growth is volatile

| Year | 2019 | 2020 | 2021 | 2022 | 2023 | 2024 | 2025 |
|---|---|---|---|---|---|---|---|
| E-commerce growth | 21% | 50% | 44% | 10% | 6% | 15% | 18% |

**Insight:** The pandemic caused a sharp spike in 2020–2021, followed by normalization in 2022–2023 and a moderate re-acceleration in 2024–2025.

### 4.5 Product categories

- **Fresh Foods** is rated the most important category, followed by **Kirkland Signature Grocery** and **Household Essentials**.
- Higher-frequency, essential categories (food, household, baby and pet) rank above discretionary ones (electronics, home and garden, seasonal).

**Insight:** Traffic is driven by repeat-purchase necessities, while discretionary categories add basket size and seasonal spikes.

### 4.6 Customer profile

| Segment | Share of shoppers |
|---|---|
| Household income above $125K | 36% |
| Household income $40K–$125K | 46% |
| Household income below $40K | 18% |
| Female / Male | 72% / 28% |
| Gen X & Boomers | 55% |
| Millennials | 35% |
| Gen Z | 10% |
| Average visits per year | 32 |

**Insights:**
- About **82%** of shoppers have household income above $40K, so the base is middle to upper-middle income.
- The base skews female and older, and Gen Z is under-represented, which is a possible long-term growth opportunity.
- About 32 visits per year (roughly once every 11 days) shows a strong habit-driven shopping pattern.

### 4.7 Summary: the business flywheel

> Low margins on products → strong value perception → high renewal and member growth → stable membership income → funds further expansion and lower prices.

---

## 5. Data Limitations

Because this is a **training dataset**, treat the results as directional only:

- **Not official data.** Figures are approximate and unverified against Costco's filings.
- **Executive member figures are inconsistent for 2024–2025.** The member count drops from 55M to 36M and 38.7M, while `Exec_Percent` rises to 45% and 47.8%. The two columns cannot both be correct (36 ÷ 132 ≈ 27%, not 45%).
- **`Paid_Members` definition is unclear.** The values may include all cardholders (e.g., add-on cards) rather than only paid memberships.
- **Category data is qualitative.** `Sales_Importance` is a rating, not actual sales. The numeric score is an arbitrary mapping and should not be read as a real ranking of revenue.
- **Demographics are a single snapshot.** There is no time dimension, and each group (income, gender, generation) is a separate distribution that should not be combined into one chart.
- **No profitability data.** There is no net income, margin, or cost data, so conclusions about profit are inferences only.
- **Small sample.** Seven yearly data points are enough to spot trends but not to build reliable forecasts.

### Dashboard notes

- KPI cards currently aggregate **all years** (e.g., summing members across years). For "latest value" KPIs, filter to 2025 or add a year slicer.
- The demographics donut mixes separate distributions and a non-percentage row; separate visuals per group would be clearer.

---

## 6. Suggested Next Steps

- Add a **year slicer** and switch KPI cards to the latest year with YoY deltas
- Split the demographics visuals by group (income, gender, generation)
- Replace the qualitative category rating with real sales-by-category data
- Validate the dataset against official annual reports and correct the executive-member figures
- Add profitability metrics (net income, operating margin) to connect growth to earnings
- Try simple forecasting (e.g., a linear trend on revenue and members) as a modeling exercise

---

## 7. Tools

- **Power BI Desktop:** data model, DAX measures, dashboard
- **Python (pandas):** data inspection and verification of calculated metrics
