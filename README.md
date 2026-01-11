# BIX Business Performance Analytics Dashboard 

<!-- Technology badges -->
[![Microsoft Excel](https://img.shields.io/badge/Microsoft%20Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)](https://github.com/nafisalzamee-lab/BIX-Business-Performance-Dashboard/blob/main/BIX%20Business%20Dashboard.xlsm)

<!-- Action buttons (rounder style) -->
[![Watch on YouTube](https://img.shields.io/badge/Watch%20on-YouTube-red?style=flat&logo=youtube&logoColor=white)](https://youtu.be/-GmB_grXbdo)
[![Connect on LinkedIn](https://img.shields.io/badge/Connect%20with%20me-LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/md-nafis-al-zamee-a88a9024b)
[![Download & Explore Dashboard](https://img.shields.io/badge/Download%20%26%20Play-Excel%20Dashboard-217346?style=flat&logo=microsoft-excel&logoColor=white)](https://github.com/nafisalzamee-lab/BIX-Business-Performance-Dashboard/raw/main/BIX%20Business%20Dashboard.xlsm)
[![Download Excel File](https://img.shields.io/badge/Download-Excel%20File-217346?style=flat&logo=microsoft-excel&logoColor=white)](https://github.com/nafisalzamee-lab/BIX-Business-Performance-Dashboard/raw/main/BIX%20Business%20Dashboard.xlsm)

---

<!-- Clickable YouTube thumbnail -->
[![Retail Sales Data Analysis with Excel](https://img.youtube.com/vi/-GmB_grXbdo/maxresdefault.jpg)](https://youtu.be/-GmB_grXbdo)

  
## Project Overview
This project features a **dynamic, interactive Excel dashboard** designed to analyze retail sales performance across stores, time periods, and customer segments. Transforming raw transactional data into actionable insights, the solution relies on a **normalized data model** in **Power Pivot** that interconnects a 20,000+ row fact table with specific customer, product, store, and custom date dimensions. Built entirely within Microsoft Excel using **Power Query** for data extraction and advanced **DAX measures** for calculation, the dashboard visualizes critical KPIs—including revenue, profit margins, targets, and refund trends—to support data-driven decision-making.

---
## Problem Statement  
The reail company **BIX** required an interactive dashboard to consolidate and analyze transactional data for **revenue tracking**, **profit optimization**, **customer segmentation**, and **operational KPIs** across stores, timeframes, and demographics—but lacked a scalable Excel solution.   

---

## Project Objectives

* **Data Transformation & Modeling:** Normalizing and modeling raw transactional data (capable of handling up to 10M+ rows) to ensure seamless performance and stability without lag.
* **Multi-View Architecture:** Developing **three interconnected dashboards**—Store Performance, Time Frame Analysis, and Profit View—to provide a holistic view of the business.
* **Dynamic Analysis & Segmentation:** Enabling granular slicing by time, store, product, and salesperson, alongside customer demographic segmentation (age, gender), to identify **growth opportunities** and **underperforming segments**.
* **Visual Performance Tracking:** Implementing dynamic KPIs with visual storytelling elements (conditional formatting, icons, arrows) to compare actuals vs. targets.
* **Key Metric Monitoring:** Tracking and visualizing high-impact metrics, specifically monitoring **Revenue Growth (46%)**, **Profit Margins (42.8%)**, and **Refund Rates (8%)** to drive data-led decision-making.
  
**Technologies Used:**  
- **Microsoft Excel 2024**: Power Query (ETL), Power Pivot (modeling), DAX (measures).  
- **Visualization**: Charts, conditional formatting, icons/shapes (Flaticon), Zebra BI add-in.  
- **Automation**: VBA macros (slicer toggle), form controls (group boxes/option buttons).  

---

## Data Set Details  
- **Size**: 20,000+ rows in fact table (transactions); total ~25,000 rows across 5 tables.  
- **Tables**:
  | Table | Columns | Key Fields |
  |-------|---------|------------|
  | **Fact (Transactions)** | 9 | TransactionID, CustomerID, ProductID, StoreID, SalespersonID, Date, QuantitySold, ReturnQuantity  
  | **Customers** | 5 | CustomerID, FirstName, LastName, DOB, Gender  
  | **Products** | 4 | ProductID, ProductName, SalesPrice, CostPrice  
  | **Salespersons** | 3 | SalespersonID, FirstName, LastName  
  | **Stores** | 3 | StoreID, StoreName, Location  
  | **Date** (Custom) | 12 | Date, Year, Month, Quarter, Weekday, Weekend, etc.  
- **Time Period**: Multi-year dataset with quarterly/monthly granularity.  
---

## Key Analyses Performed
1. **Revenue vs Target Variance**: By Store/Month/Quarter (absolute + % with up/down indicators).   
2. **Profitability Metrics**: Margin %, Cost of Goods Sold, MoM growth.   
3. **Return & Refund Analysis**: Total Refund, Refund Rate (8% overall), Return Quantity %.   
4. **Customer Segmentation**: Age groups (0-20, 21-30, etc.), Gender profit %, Top/Bottom 5 customers..   
5. **Time Intelligence**: Weekend/Weekday revenue %, Quarter trends, # Products Sold (distinct).   
6. **Product Performance**: Top products by Profit/Quantity, overall # Products/Transactions.
7. **Store Performance**: Revenue/profit by location with variance % and top/bottom rankings.
---

## key Steps 


---

### Data Cleaning & Preparation (Power Query)  
<table>
  <tr>
    <td>
    <td style="text-align: center;">
      <em>Data cleaning & preparation in power query</em><br />
      <img src="images/data cleaning & preparation in power query.png" alt="data cleaning & preparation in power query" width="500" height="1000" /></td>
    <td>
    <td style="text-align: center;">
      <em>Date table creation in power query</em><br />
      <img src="images/date table creation in power query.png" alt="date table creation in power query.png" width="500" height="400" /></td>
  </tr>
</table>
I Structured ETL pipeline to clean and transform raw CSV data into a relational model. I implemented the following steps sequentially:

1. **Source Import**: Loaded 5 CSV files (transactions, customers, products, salespersons, stores) via **Get Data > From Text/CSV**.then clicked transform data to enter power query.  
2. **Header Promotion**: Promoted first row to column headers across all queries.  
3. **Data Type Changes**:Power query auto-detected and set types (e.g., Date to Date, QuantitySold/ReturnQuantity to Whole Number, IDs to Text).  
4. **Name Merging**: Combined FirstName + " " + LastName into **FullName** columns for customers and salespersons.  
5. **Age Derivation**: Added **Age** column: $$Age = \frac{TODAY() - DOB}{365.25}$$ (rounded to nearest whole number).  
6. **Duplicate Removal**: Eliminated rows based on unique **TransactionID** in fact table.  
7. **Date Dimension Creation**: Generated custom calendar table from min/max dates:
   - Extracted **Year**, **Month Name**, **Month Number**, **Quarter**, **Weekday**, **Weekend** flag.
   - Added sorting columns (e.g., MonthSort = 1-12).
<table>
  <tr><td style="text-align: center;">
      <em>Load Optimization</em><br />
    <td><img src="images/only connection 1.png" alt="Queries set to **Connection Only**" width="300" height="300" /></td>
  </tr>
</table>

8. **Load Optimization**: Queries set to **Connection Only** (except calculations table) for Power Pivot efficiency.  

> I used Power Query to handle the heavy lifting of data transformation before loading it into Power Pivot.  

 

### Establishing  Power Pivot Relationships (Data modeling)  
Used **Star Schema** design in Power Pivot for efficient querying and slicing.  

### Model Structure  
- **Fact Table**: Transactions (20K+ rows) as central hub.  
- **Dimension Tables**: Customers, Products, Salespersons, Stores, Date (one-to-many from fact).  
<table>
  <tr>
    <td style="text-align:  center;">
      <em>power pivot data model</em><br />
      <img src="images/pivot data model.png" alt="pivot data model" width="400" height="300" />
    </td>
    <td style="text-align: center;">
      <em>dataset in power pivot</em><br />
      <img src="images/power pivot data.png" alt="power pivot data" width="400" height="300" />
    </td>
  </tr>
</table>

### Relationships Established  
1. **Fact[CustomerID] → Customers[CustomerID]** (Many:1, single direction).  
2. **Fact[ProductID] → Products[ProductID]** (Many:1).  
3. **Fact[StoreID] → Stores[StoreID]** (Many:1).  
4. **Fact[SalespersonID] → Salespersons[SalespersonID]** (Many:1).  
5. **Fact[Date] → Date[Date]** (Many:1, active for time intelligence).  

**Additional Table**:I created a blank "Calculations" table to house all DAX measures (no relationships needed).  

| Relationship | Cardinality | Cross-Filter | Purpose |
|--------------|-------------|--------------|---------|
| Fact → Customers | Many:1 | Single | Customer segmentation  
| Fact → Products | Many:1 | Single | Product profitability  
| Fact → Date | Many:1 | Both | Time-based slicing  

**DAX Integration**: Measures reference related tables via **RELATED()** and **USERELATIONSHIP()** for context-aware calculations.
 

### Creating DAX Measures  
**Core Calculations** (stored in blank "calculations" table):  
<table>
  <tr>
    <td style="text-align:  center;">
      <em>Dax measures in the separate table </em><br />
      <img src="images/all measures.png" alt="all measures" width="400" height="300" />
    </td>
  </tr>
</table>

| Measure | Formula | Purpose |
|---------|---------|---------|
| **Total Revenue** | $$SUMX(FactTable, FactTable[QuantitySold] \times RELATED(ProductTable[SalesPrice]))$$   | Calculates total sales revenue by multiplying quantity sold with sales price across transactions.  
| **COGS** | $$SUMX(FactTable, FactTable[QuantitySold] \times RELATED(ProductTable[CostPrice]))$$   | Computes total cost of goods sold using quantity and cost price.  
| **Profit Margin** | $$[Total Revenue] - [COGS]$$   | Determines gross profit by subtracting COGS from revenue.  
| **Profit %** | $$DIVIDE([Profit Margin], [Total Revenue])$$   | Calculates profit margin as percentage of revenue.  
| **# Transactions** | $$COUNTROWS(FactTable)$$   | Counts total number of transactions.  
| **Total Refund** | $$SUMX(FactTable, FactTable[ReturnQuantity] \times RELATED(ProductTable[SalesPrice]))$$   | Sums refund value based on returned quantity and sales price.  
| **Refund Rate** | $$DIVIDE([Total Refund], [Total Revenue])$$   | Measures refund rate as percentage of total revenue.  
| **# Products Sold** | $$DISTINCTCOUNT(FactTable[ProductID])$$   | Counts unique products sold (excludes unsold inventory).   
| **# Customers** | $$DISTINCTCOUNT(FactTable[CustomerID])$$   | Counts unique customers with purchase history.  
| **Return Rate** | $$DIVIDE(SUM(FactTable[ReturnQuantity]), SUM(FactTable[QuantitySold]))$$   | Calculates ratio of returned items to total sold.  
| **Average Customer Age** | $$AVERAGE(Customers[Age])$$   | Computes average age of purchasing customers.   

**Notes**:  
Custom formats used: e.g., $$[<=1000000]\$0.0,,"M";[<=1000]\$0.0,"K";\$0.0$$ for abbreviated millions/Ks.  

<table>
  <tr>
    <td style="text-align:  center;">
      <em>Custom format</em><br />
      <img src="images/value 1.png" alt="value 1" width="400" height="300" />
    </td>
  </tr>
</table>

---
## Pivot Table Creation & Implementation  

I developed **12+ interconnected PivotTables** as the analytical foundation of the dashboard, leveraging the **Power Pivot data model** to enable dynamic cross-table analysis without complex formulas.   

### Implementation Workflow  

#### **1. Foundation Setup**  
For each dashboard section, I inserted PivotTables directly from the data model (Insert → PivotTable → From Data Model), which automatically inherited all 6 tables and their relationships.   I  placed source PivotTables in different sheets(e.g. analysis 1, analysis 2) to maintain clean dashboard visuals.  

#### **2. Some of the Dashboard-Specific PivotTables**  

**Store  Dashboard** :  
| PivotTable | Rows | Values | Purpose |
|------------|------|--------|---------|
| Store Revenue | StoreName | Total Revenue, Target | Source for revenue bars  
| Store Variance | StoreName | Variance % | Dynamic variance labels  
<table>
  <tr>
    <td style="text-align:  center;">
      <em>store KPI  table</em><br />
      <img src="images/store pivot 1.png" alt="store pivot 1" width="400" height="300" />
    </td>
    <td style="text-align: center;">
      <em>store revenue table</em><br />
      <img src="images/store pivot 2.png" alt="store pivot 2" width="400" height="300" />
    </td>
  </tr>
</table>

**Time Frame Dashboard** :  
| PivotTable | Rows/Columns | Values | Purpose |
|------------|--------------|--------|---------|
| Monthly Trends | Month (Columns) | Total Revenue | Line chart with markers  
| Quarter Analysis | Quarter | Revenue, Average | Benchmark comparison  
| Weekday Split | Weekday | Revenue % of Total | Waffle chart source  
<table>
  <tr>
    <td style="text-align:  center;">
      <em>Monthly Trends</em><br />
      <img src="images/time pivot 1.png" alt="time pivot 1" width="400" height="300" />
    </td>
    <td style="text-align: center;">
      <em>Weekday Split</em><br />
      <img src="images/time pivot 2.png" alt="time pivot 2" width="400" height="300" />
    </td>
    <td style="text-align: center;">
      <em>Quarter Analysis</em><br />
      <img src="images/time pivot 3.png" alt="time pivot 3" width="400" height="300" />
    </td>
  </tr>
</table>

**Profit View Dashboard** :  
| PivotTable | Rows | Values | Purpose |
|------------|------|--------|---------|
| Customer Ranking | Customer Name (Top 5) | Profit Margin | Switchable top/bottom bars  
| Age Demographics | Age Group | Profit %, Avg Age | Demographic analysis  
| Product Performance | Product Name (Top 5) | Profit/Quantity | Category breakdown  
<table>
  <tr>
    <td style="text-align:  center;">
      <em>Monthly profit trends with variance analysis pivot tables</em><br />
      <img src="images/profit pivot 1.png" alt="profit pivot 1" width="400" height="300" />
    </td>
    <td style="text-align: center;">
      <em>customer ranking</em><br />
      <img src="images/profit pivot 2.png" alt="profit pivot 2" width="400" height="300" />
    </td>
    <td style="text-align:  center;">
      <em>age demographics</em><br />
      <img src="images/profit pivot 3.png" alt="profit pivot 3" width="400" height="300" />
    </td>
    <td style="text-align: center;">
      <em>profit by gender </em><br />
      <img src="images/profit pivot 4.png" alt="profit pivot 4" width="400" height="300" />
    </td>
  </tr>
  <tr>
    <td style="text-align:  center;">
      <em>top product categories pivot table</em><br />
      <img src="images/profit pivot 5.png" alt="profit pivot 5" width="400" height="300" />
    </td>
    <td style="text-align: center;">
      <em>operattional leakge pivot table</em><br />
      <img src="images/profit pivot 6.png" alt="profit pivot 6" width="400" height="300" />
    </td>
    <td style="text-align: center;">
      <em>product performance</em><br />
      <img src="images/profit pivot 7.png" alt="profit pivot 7" width="400" height="300" />
    </td>
  </tr>
</table>

#### **3. Advanced Value Settings**  
I configured each measure through Value Field Settings with custom calculations and formatting.   For variance analysis, I used "Show Values As → % Difference From" to calculate month-over-month changes.   Number formats were customized to display abbreviated values (e.g., $5.4M instead of $5,400,000).  
<table>
  <tr>
    <td style="text-align:  center;">
      <em>value setting (show value as) </em><br />
      <img src="images/value 2.png" alt="value 2" width="400" height="300" />
    </td>
  </tr>
</table>

#### **4. Layout Optimization**  
I standardized all PivotTables with compact layout, removed subtotals and grand totals, and disabled banded rows for cleaner visuals.   Each PivotTable was named descriptively in the backend pivot table list (e.g., "pt_StoreRevenue") for easy reference in VBA macros.  


#### **5. Interactive Slicer System**  
I created slicers for Month, Category, and Gender dimensions to enable dynamic filtering.   Each slicer was styled with white fill and bold selection for professional appearance.   Using Report Connections, I synchronized all slicers across the 12+ PivotTables and charts, ensuring one-click filtering across the entire dashboard.   I also implemented a VBA macro to toggle slicer visibility for presentation mode.  


#### **6. PivotChart Integration**  
From each PivotTable, I created corresponding PivotCharts (Insert → PivotChart → Clustered Column).   I enhanced charts with data labels sourced from helper columns using formulas like =TEXT([@Variance],"0.0%"), added targets on secondary axes, and applied gradient fills with the Zebra add-in.    The charts automatically refresh when users interact with slicers, providing instant visual feedback.  
<table>
  <tr>
    <td style="text-align:  center;">
      <em>Created pivot charts for dashboard</em><br />
      <img src="images/pivot chart 1.png" alt="pivot chart 1.png" width="400" height="300" />
    </td>
  </tr>
</table>

**Key Achievement**: The data model relationships enabled one slicer to filter the fact table and all dimension tables simultaneously, eliminating the need for  VLOOKUP formulas.

---

## Dashboard Visualizations  

<img src="images/store view db.png" alt="Store Dashboard — Store view (Image 1)" width="800" />

### Store Dashboard 
- **Zebra BI Combo Chart**: Revenue vs Target bars by Store + variance % (up/down arrows).
- **Dynamic KPIs**: Total Revenue, Target, Variance (IF/TEXT for ±12% ↑ with emojis).
- **Month Slicer**: 4-column, custom styled (bottom border on selected).

<img src="images/time frame db.png" alt="Time Frame Dashboard — Time Frame view (Image 2)" width="800" />

### Time Frame Dashboard   
- **Trend Chart**: Smoothed Revenue/Target lines + MoM variance.
- **Waffle Charts**: Weekend/Weekday revenue % (10x10 grids).
- **Quarter Combo**:  Columns + lines + % diff, highlights above average.   
- **Variance waterfall** (invert if negative, conditional colors).

<img src="images/profit view.png" alt="Profit View Dashboard — Profit View (Image 3)" width="800" />

### Profit View Dashboard  
- **Customer Switcher**: Top/Bottom 5 via Option Buttons (Profit/Revenue).
- **Age Buckets**: Column chart (0-20, 21-30, etc.) + average age.
- **Gender Waffle**: Icon-based (square/male, circle/female).
- **Product KPIs**: Return Rate, # Products, Top Products toggle.
- **Dynamic captions** (TEXTJOIN + IF for context like "Top 5 Profitable Products: 100/600 Customers").

***Design Elements***: 
- **Gradient shapes**: Used the 31-140-179 RGB theme for a cohesive visual identity.
- **Icons**: Flaticon PNG icons recolored to match the dashboard’s gradient theme.
- **Navigation**: Interactive navigation hyperlinks used for moving between dashboard views.
- **Toggle VBA**: AI‑enhanced VBA macro used to toggle slicers on and off for dynamic filtering.
---
## Design & UX Principles  
- **Color Consistency**: Blue gradient theme (RGB 31-140-179), white/grey backgrounds for readability.  
- **Hierarchy**: Bold KPIs top-center, slicers left, charts right; navigation tabs above.   
- **Interactivity**: One-click filters, hover effects, no-scroll layout (fit to screen).  
- **Accessibility**: High contrast, alt-text icons, logical tab order.  
- **Minimalism**: Hide unused elements, dynamic titles/captions for context.  
---
## Key Features:
- **Dynamic KPIs**: Total revenue ($$\$5.4M$$), COGS, profit margin (42.8%), refund rate (8%), and targets with variance indicators (e.g., +46% growth).   
- **Multi-tab Views**: Store analysis, time frame trends, profit views with customer/product breakdowns.   
- **Interactive Controls**: Slicers (month, category), option buttons (top/bottom 5), combo box, and hide/show filters via VBA macros.
<table>
  <tr>
    <td style="text-align:  center;">
      <em>waffle chart</em><br />
      <img src="images/waffle chart.png" alt="waffle chart" width="400" height="300" />
    </td>
    <td style="text-align: center;">
      <em>zebra BI chart</em><br />
      <img src="images/zebra BI chart.png" alt="zebra BI chart" width="400" height="300" />
    </td>
    <td style="text-align:  center;">
      <em>gradient chart</em><br />
      <img src="images/gradient chart.png" alt="gradient chart" width="400" height="300" />
    </td>
    <td style="text-align: center;">
      <em>assigning VBA macro</em><br />
      <img src="images/assigning VBA macro.png" alt="assigning VBA macro" width="400" height="300" />
    </td>
  </tr>
  <tr>
    <td style="text-align:  center;">
      <em>multi tab view</em><br />
      <img src="images/multi tab view.png" alt="multi tab view" width="400" height="300" />
    </td>
    <td style="text-align: center;">
      <em>combo box</em><br />
      <img src="images/combo box.png" alt="combo box" width="400" height="300" />
    </td>
    <td style="text-align:  center;">
      <em>interactive caption 1</em><br />
      <img src="images/interactive caption 1.png" alt="interactive caption 1" width="400" height="300" />
    </td>
    <td style="text-align: center;">
      <em>interactive caption 2</em><br />
      <img src="images/interactive caption 2.png" alt="interactive caption 2" width="400" height="300" />
    </td>
  </tr>
</table>
  <table>
  <tr>
    <td style="text-align:  center;">
      <em>interaactive slicer (store name)</em><br />
      <img src="images/interaactive slicer 2.png" alt="interaactive slicer 2" width="400" height="300" />
    </td>
    <td style="text-align: center;">
      <em>interactive slicer (month  & product category)</em><br />
      <img src="images/interactive slicer 1.png" alt="interactive slicer 1" width="400" height="300" />
    </td>
  </tr>
</table>

- **Custom Visuals**: Waffle charts (weekday revenue split), gradient-filled trends, zebra add-in bars, and conditional formatting with icons/arrows.   
- **Data Model**: Star schema with 1:many relationships (fact → dimensions).  
- **DAX Measures**: 10+ custom metrics (e.g., Profit % = $$DIVIDE([Profit], [Revenue])$$, formatted as %).     
- **Advanced Charts**: Waffle grids (SEQUENCE/conditional formatting), gradient trends, zebra bars (add-in), pie for categories.   
- **Dynamic Elements**: Captions (TEXTJOIN/IF), variance labels ($$TEXT(variance,"+0.0\% \u2191")$$).
- **Navigation**: Hyperlinked buttons between 3 dashboards; paste-as-picture for locked KPIs.    

---

## Key Insights & Business Value  

**BIX slightly outperformed its goal, delivering $5.4M revenue vs a $5.3M target (+3.7% variance) while maintaining a 42.18% profit margin.**

- **Profit structure:** COGS totals $3.1M, resulting in $2.3M profit (profit margin value).

### 1. Revenue & Time-Based Trends
- **Weekday Dominance:** Revenue is disproportionately concentrated on weekdays (**86%**) versus weekends (**14%**), indicating a massive opportunity to boost Saturday/Sunday engagement.
- **Seasonal Volatility:** Performance fluctuates significantly, with strong peaks in **August (+12.5%)** and **November (+11.9%)**, contrasted by dips in **July (-5.0%)** and **December (-3.4%)**.
- **Quarterly Stability:** Despite monthly swings, quarterly revenue remains consistent, hovering near the **$1.36M average** across all four quarters.

### 2. Store Performance Variance
- Store performance reveals a massive 55.7% execution gap between top locations like Lee-Myers (+31.1%) and underperformers like Novak PLC (-24.6%), indicating that revenue variance is driven by ***specific operational inconsistencies rather than market-wide issues***.

### 3. Customer & Product Profitability
- **Demographic Focus:** Profitability is driven by older demographics, with the **51+ age group** contributing the most profit (≈ $554K), followed by the **41–50 group** (≈ $504K). Gender contribution is effectively balanced (51.5% Male vs. 48.5% Female).
- **Category Hierarchy:** **Soft Drinks** are the primary profit engine ($718K), generating nearly double the profit of the next best category, **Sports Drinks** ($417K).
- **Operational Leakage:** A high **return rate of 8.03%** and **refund rate of 8.05%** indicates potential quality control or customer satisfaction issues that are eroding margins.

---
  
**Skills Demonstrated**: *Data cleaning ,Data preparation, Data modeling,Power Pivot, Dashboarding, Power Query ETL, DAX , Advanced Charting (waffle/gradients), Form controls/VBA, Custom Formatting, Data Story telling*. 

---

## Project Outcome  
- **Business Impact**: Identified top stores/customers (e.g., 41-50 age group), optimized inventory (low-return products), tracked 46% growth vs. targets.   
- **Scalable Solution**: Handles large datasets dynamically; exportable to Power BI if needed.      

---
## Download & Play with the Dashboard

You can view and run the full Dashboard by downloading the excel file here:  
[Download & Open the Dashboard](https://github.com/nafisalzamee-lab/BIX-Business-Performance-Dashboard/raw/main/BIX%20Business%20Dashboard.xlsm)

*Need Help??*
[![Connect with me on LinkedIn](https://img.shields.io/badge/Connect%20with%20me-LinkedIn-blue?logo=linkedin)](https://www.linkedin.com/in/md-nafis-al-zamee-a88a9024b)


