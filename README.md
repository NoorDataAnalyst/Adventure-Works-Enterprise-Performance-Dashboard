#  Adventure Works 2020 Enterprise Performance Dashboard

[![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=microsoftpowerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Data Analytics](https://img.shields.io/badge/Data_Analytics-Minions-blue?style=for-the-badge&logo=analytics&logoColor=white)](https://github.com/)
[![DAX](https://img.shields.io/badge/DAX-Data_Modeling-orange?style=for-the-badge)](https://learn.microsoft.com/en-us/dax/)

An end-to-end enterprise business intelligence solutions engine built in **Power BI Desktop**. This project ingests, models, and visualizes over **60,398 rows of raw retail data** across 9 distinct dimension and fact tables (from July 2016 to July 2019), converting historical records into interactive, actionable business intelligence for executive leadership.

---

##  Executive Project Highlights
* **Total Revenue:** `$29.36M` 
* **Total Net Profit:** `$12.08M` 
* **Healthy Profit Margin:** `41.15%` 
* **Total Transactions:** `28K Orders` 
* **Budget Forecasting Accuracy:** `98.38% Overall Budget Attainment` 

---

##  Data Architecture & Modeling (Star/Snowflake Schema)
The data model was built from raw Excel sheets using clean Relational Database design principles. It features a high-performance star schema centered around the primary fact table (`Sales`), fully optimized with directional cross-filtering.

###  Ingested Tables & Transformations:
1. **Sales (Fact Table):** Contains transactional details, quantities, prices, costs, and key assignments.
2. **Products (Dimension):** Granular product catalog including costs, list prices, color, size, and classification.
3. **dimProductCategory & dimProductSubCategory (Dimension):** Snowflaked layers providing analytical categorization.
4. **Customers (Dimension):** Demographic markers including gender, income, marital status, and occupations.
5. **Territory (Dimension):** Geographic mapping across 3 continental groups (North America, Europe, Pacific).
6. **Calendar (Dimension):** Custom date table explicitly marked as the **Date Table** for core time-intelligence calculations.
7. **Budget & BudgetPeriod (Fact/Dimension):** Stores category-level financial goals.

###  Data Cleaning Steps (Power Query):
* Eliminated blank records from the `Territory` table (Row 11).
* Normalized demographic codes into fully human-readable labels (`M` $\rightarrow$ `Male` / `F` $\rightarrow$ `Female` & `M` $\rightarrow$ `Married` / `S` $\rightarrow$ `Single`) to keep visual charts clean and highly intuitive for business managers.

---

##  Custom DAX Calculations
A comprehensive suite of **10 distinct custom DAX measures** was authored from scratch to track real-time commercial performance instead of relying on default implicit fields:

| Measure Name | DAX Expression | Purpose |
| :--- | :--- | :--- |
| **Total Revenue** | `Total Revenue = SUM(Sales[SalesAmount])` | Baseline income generation metric. |
| **Total Profit** | `Total Profit = SUM(Sales[SalesAmount]) - SUM(Sales[TotalProductCost])` | Net operational profit across products. |
| **Profit Margin %** | `Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0) * 100` | Operational efficiency & pricing power gauge. |
| **Total Orders** | `Total Orders = DISTINCTCOUNT(Sales[SalesOrderNumber])` | Strict absolute sales transactional volume. |
| **Avg Order Value** | `Avg Order Value = DIVIDE([Total Revenue], [Total Orders], 0)` | Mean value spent per customer order. |
| **Budget Total** | `Budget Total = SUM(Budget[Budget])` | Historical targets aggregated across categories. |
| **Budget Attainment %** | `Budget Attainment % = DIVIDE([Total Revenue], [Budget Total], 0) * 100` | Percentage metric tracking target milestones. |
| **YTD Revenue** | `YTD Revenue = TOTALYTD(SUM(Sales[SalesAmount]), Calendar[Date])` | Year-to-Date running performance indicator. |
| **Prev Year Revenue**| `Prev Year Revenue = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR(Calendar[Date]))` | Historical baseline for Year-over-Year evaluation. |
| **YoY Growth %** | `YoY Growth % = DIVIDE([Total Revenue] - [Prev Year Revenue], [Prev Year Revenue], 0) * 100`| Normalized percentage indicating growth speed. |

---

##  Dashboard Layout & Insight Matrix
The application is structured into **5 dedicated, interactive report pages** featuring global synchronization slicers (`Year`, `Product Category`, and `Country`) allowing cross-filtering drill downs.

###  Page 1: Sales Overview (Executive Summary)
* **Visuals 1–4 (KPI Cards):** Display `Total Revenue ($29.36M)`, `Total Profit ($12.08M)`, `Profit Margin (41.15%)`, and `Total Orders (28K)` for macro health reporting.
* **Visual 5 (Line Chart - Monthly Revenue Trend):** Tracks historical trends. Uncovers sharp **seasonality peaks every June** and immediate winter baseline dips (Jan–Feb).
* **Visual 6 & 7 (Bar & Donut - Category Performance / Mix):** Highlights structural concentration risk; **Bikes drive 96.46% ($28.32M)** of sales mix, indicating dependency.

###  Page 2: Product Analysis (Portfolio & Operations)
* **Visual 8 & 9 (Bar Charts - Top & Bottom 10 Products):** Isolates high-performing SKU stars (e.g., *Mountain-200 Series*) from lagging liabilities to inform warehouse updates.
* **Visual 10 (Clustered Column - Revenue by SubCategory):** Provides deep visibility into Road, Mountain, and Touring variations.
* **Visual 11 (Column Chart - Profit Margin by Category):** Confirms that while *Accessories* bring low gross revenue, they have outstanding standalone margin metrics.
* **Visual 12 (Scatter Plot - Price vs. Quantity Sold):** Visualizes product pricing elasticity.
* **Visual 13 (Stacked Bar - Revenue by Product Color):** Shows clear preferences for *Black* and *Silver* models to direct supply-chain purchasing choices.

###  Page 3: Customer Insights (Target Demographics)
* **Visual 14 & 15 (Bar & Column - Revenue by Occupation & Income Bracket):** Proves that *Professionals* and *Management* segments make up the primary high-spending consumer group.
* **Visual 16 & 17 (Donut Charts - Sales by Gender & Marital Status):** Evaluates behavioral variations between single/married and male/female buyers.
* **Visual 18 (Bar Chart - Revenue by Cars Owned):** Links household transit habits directly to high-end bicycle purchases.

###  Page 4: Territory Performance (Global Footprint)
* **Visual 19 (Map Visual - Revenue by Country):** Displays geographic revenue across international boundaries.
* **Visual 20 & 21 (Column & Bar - Revenue by Region & Continental Group):** Profiles balanced distribution across continents—`North America ($11M)`, `Europe ($9M)`, and `Pacific ($9M)`.

###  Page 5: Budget vs. Actuals (Financial Auditing)
* **Visual 22 (Clustered Column - Actual vs. Budget by Month):** Highlights execution alignment where the company met or exceeded targets.
* **Visual 23 (KPI Card - Budget Attainment %):** Confirms an overall target achievement rate of **98.38%**.
* **Visual 24 (Bar Chart - Actual vs. Budget by Category):** Shows performance alignment across different categories.
* **Visual 25 (Line Chart - Cumulative Revenue vs. Budget Over Time):** Plots actual running revenue directly against budgeted milestones to keep leadership updated on structural goals.

---

##  Key Strategic Recommendations for Management
1. **Deploy Cross-Selling Bundles:** Since Bikes control over 96% of revenue, implement automated *"Frequently Bought Together"* accessory bundles (helmets, locks, pumps) at checkout to capture margins from the 28K orders.
2. **Mitigate Seasonal Volatility:** Scale up manufacturing and optimize warehouse supply chains during the winter troughs (Jan-Feb) to protect inventory availability before the massive summer demand peak hits in June.
3. **Optimize Inventory Allotment:** Focus manufacturing on dominant color variants (*Black/Silver*) and consider liquidating or restructuring low-performing SKUs identified on Page 2 to reclaim trapped working capital.

---

##  Repository Structure
```repo
├── Adventure Works 2020.xlsx - Sales.csv       
├── FA24-BBD-069_NoorulainZahid_PowerBi.pbix    # Final Interactive Power BI Engine File
├── FA24-BBD-069_NoorulainZahid_PowerBi.pdf     # Static Multi-Page Dashboard Export
└── README.md                                   # Project Documentation & Insights Overview
