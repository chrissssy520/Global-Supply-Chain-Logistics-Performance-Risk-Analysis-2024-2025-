# Global Supply Chain — Logistics Performance & Risk Analysis (2024–2025)

A practice end-to-end data analytics project focused on identifying logistics performance trends and operational risks using a global supply chain dataset. This covers the full workflow from raw data cleaning to a published interactive dashboard.

**Dashboard:** https://public.tableau.com/app/profile/christian.aler3008/viz/Global_supply_chain/Dashboard1

---

## Objective

Analyze year-over-year (2024 vs 2025) logistics performance to identify declining trends, cost pressures, and operational risks across global shipping routes, transport modes, and origin-destination pairs.

---

## Dataset

- **Source:** [Global Supply Chain Disruption & Resilience — Kaggle](https://www.kaggle.com/datasets/bertnardomariouskono/global-supply-chain-disruption-and-resilience)
- **Size:** 10,000 rows, 30 fields
- **Period covered:** 2024–2025
- **Key fields:** Order ID, Order Date, Origin Country, Destination Country, Transport Mode, Route, Base Lead Time Days, Actual Lead Time Days, Delay Days, Shipping Cost, Weight, Inflation Rate, Geopolitical Risk

---

## Tools Used

| Tool | Purpose |
|---|---|
| Excel + Power Query | Data cleaning and data modeling |
| Tableau Public | Visualization and dashboard |

---

## Step 1 — Data Cleaning (Excel + Power Query)

The dataset was cleaned entirely in Excel using Power Query. Power Query was chosen over Python or SQL because the dataset is under 1 million rows, making it a practical and efficient tool for this scale.

Cleaning steps performed:

- Removed duplicate rows based on Order ID
- Standardized column names — removed spaces, applied consistent casing
- Corrected data types — dates formatted as Date, numeric fields as Decimal or Whole Number
- Trimmed leading and trailing whitespace on text columns (Origin, Destination, Route, Transport Mode)
- Handled null and blank values — flagged and removed rows with missing Order ID or Order Date as they are critical keys
- Validated numeric ranges — checked that Delay Days are non-negative and Lead Time values are logical
- Standardized categorical values — ensured consistent labels across Transport Mode and Route fields to avoid duplicates caused by casing differences

---

## Step 2 — Data Modeling (Power Query)

After cleaning, the dataset was split into a fact table and a dimension table to follow basic data modeling principles. This reduces redundancy, keeps the data structured, and improves performance in Tableau.

**fact_table** — transactional and measurable data per order:
- Order ID (primary key)
- Order Date
- Base Lead Time Days
- Actual Lead Time Days
- Delay Days
- Shipping Cost
- Weight (kg)
- On Time flag

**dimension_table** — descriptive attributes per order:
- Order ID (foreign key)
- Origin Country
- Destination Country
- Transport Mode
- Route
- Geopolitical Risk
- Inflation Rate

Both tables were created inside Power Query using the duplicate and remove columns approach, then loaded as separate sheets in the same Excel workbook.

---

## Step 3 — Visualization (Tableau Public)

The cleaned Excel file was connected to Tableau Public. The fact and dimension tables were joined on Order ID inside Tableau's data source view.

**Calculated fields created:**
- On Time Rate % — percentage of orders delivered within base lead time
- Lead Time Variance — difference between actual and base lead time
- Cost per KG — shipping cost divided by weight
- YoY comparison fields for all KPIs using year-based calculated fields

**Dashboard features:**
- Select Year parameter (2024 / 2025) to toggle between years
- YoY % change indicators with red/green color coding per KPI
- Narrative insight callout per chart explaining what the data means
- OTD drill-down via Navigation action — navigates to a breakdown sheet showing on time rate by route and transport mode
- Download button for PDF export

---

## Key Findings (2025 vs 2024)

| Metric | 2025 Value | YoY Change |
|---|---|---|
| Total Orders | 4,892 | -3.45% |
| On Time Rate | 87.00% | -0.19% |
| Lead Time Variance | 1.206 | +0.02 |
| Shipping Cost | $56,030,982 | -3.4% |
| Cost per KG | $2.26 | +1.21% |
| Inflation Rate | 3.5% | +0.03% |
| Geopolitical Risk | 49.70% | +0.02% |
| Avg Weight per Order | 5,045 kg | +0.48% |

**Notable insights:**

- Orders and on time rate are both declining while cost per kg, inflation, and geopolitical risk are rising — indicating increasing operational pressure that could further strain margins if left unaddressed
- China is the dominant origin country at 33.18% of shipments with no strong secondary leader
- The United States is the top destination at 33.18%, with remaining markets closely matched indicating no strong secondary hub
- Sea freight accounts for 82.67% of transport — heavy reliance on a single mode increases vulnerability to port and weather disruptions
- The Suez Canal is the most used route at 34.06% — high concentration on a historically disruption-prone route warrants contingency planning

---

## Project Structure

```
global-supply-chain/
│
├── global_analysis_final.xlsx     # Cleaned data with fact and dimension tables
├── README.md                      # Project documentation
```

---

## Notes

This is a practice project built to develop skills in end-to-end data analytics — data cleaning, data modeling, and business intelligence visualization. The dataset is synthetic and intended for learning purposes.
