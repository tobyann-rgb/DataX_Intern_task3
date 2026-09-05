# DataX_Intern_task3
# Task 3: Interactive Dashboard Design — Executive Performance Cockpit

## Executive Summary
This project delivers an end-to-end business intelligence solution developed for corporate decision-makers. Using transaction records from the Superstore dataset, 
the dashboard pairs top-line financial indicators with deep-dive regional and product-line visibility. The analysis diagnoses critical profit leakage, 
demonstrating that while overall revenue demonstrates robust growth and Q4 seasonality, unrestrained promotional markdowns (≥ 30%) in select Central and Eastern states severely destroy operating margin.

---

## Tools, Environment & Architecture
* **Dashboard Engine:** Microsoft Power BI Desktop
* **Data Processing & Deduplication:** Python (`pandas`, `numpy`) within Kaggle Notebooks
* **Presentation Deck:** Microsoft PowerPoint (`.pptx` / `.pdf`)
* **Dataset:** Cleaned & Aggregated Superstore Sales & Financial Records (`superstore_cleaned.csv`)

---

## Data Preparation & Modeling Pipeline
1. **Schema & Date Normalization:** Sanitized raw header strings to lowercase snake_case; parsed `order_date` and `ship_date` into standard datetime formats to derive order-to-dispatch transit times.
2. **Missing Value Imputation:** Handled geographic values, zero-padded `postal_code` to 5-digit strings, and validated regional mappings.
3. **Line-Item De-duplication & Aggregation:** 
   * Isolated and purged redundant entry clones.
   * Aggregated genuine multi-item order purchases (`order_id` + `product_id`) by summing `sales`, `quantity`, and `profit` while maintaining constant promotional rates (`discount`).
4. **DAX Measures Engineered:**
   * `Total Sales = SUM(superstore_cleaned[sales])`
   * `Total Profit = SUM(superstore_cleaned[profit])`
   * `Profit Margin = DIVIDE([Total Profit], [Total Sales], 0)` (Formatted as `%`)

---

## Dashboard Architecture & Interactive Features
* **Executive Summary Cards:** Instant high-level readouts for **Total Sales ($2.30M)**, **Total Profit ($286.4K)**, **Blended Margin (12.5%)**, and **Total Volume Sold (37.8K)**.
* **Dynamic Slicers (Multi-Select):** Slicing controls for `Region` (West, East, Central, South), `Category`, and `Segment`.
* **Dual-Axis Seasonality Line Chart:** Tracks monthly sales alongside profit, capturing baseline revenue trends and Q4 peaks (September through December).
* **Sub-Category Profitability Bar Breakdown:** Clustered horizontal ranking contrasting profitable drivers (Copiers, Phones, Envelopes) against chronic margin drains (Tables, Bookcases).

---

## 🔍 Key Strategic Insights
* **The 20% Discount Cliff:** Transactions discounted between 0% and 20% generate strong net margins. Any discount exceeding 30% wipes out net profit across almost all categories,
  culminating in single-order losses as severe as -$6,600 on 70%-off hardware.
* **Regional Disparity:** The South maintains disciplined discounting and positive profitability despite lower volume; the Central (Texas) and East (Ohio, Pennsylvania) regions
  drive the vast majority of company net losses due to default markdown policies.
* **Volume Fallacy:** High unit volume in consumables (Staples, Binders) provides steady operational turnover, but fails to compensate for unmitigated hardware discounting.

---

## Business Recommendations
1. **Institute Hard Markdown Ceilings:** Implement system approval locks on discounts > 20% across Central and Eastern sales branches.
2. **Repackage Loss Leaders:** Discontinue standalone markdowns on Tables and Bookcases; transition to bundled packages paired with high-margin Technology lines.
3. **Realign Sales Incentives:** Tie sales commission structures to net contribution margin rather than gross sales volume.
4. **Q4 Operational Alignment:** Pre-allocate logistics capacity in August to meet peak holiday order surges efficiently.

---

## Repository Deliverables
* `superstore_cleaned.csv` — Cleaned and aggregated source data.
* `superstore_dashboard.pbix` — Interactive Power BI workbook.

* `task3_presentation.pptx` / `task3_presentation.pdf` — 4-slide executive stakeholder deck.
* `dashboard_screenshot.png` — High-resolution view of the Power BI interface.
