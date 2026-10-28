E-commerce Sales & Customer Insights
A data analytics portfolio project that uses SQL Server for data profiling, data cleaning, validation, and business analysis, with Power BI planned for interactive reporting. The project explores order performance, product and category sales, customer purchasing behavior, and order-status trends.
Project status: SQL data preparation and analysis are being developed. Update the dashboard screenshots, final findings, and any metric values after validating the results against your own cleaned database.

Table of Contents
- Project Overview
- Business Problem
- Project Objectives
- Tools and Technologies
- Dataset and Tables
- Data Cleaning and Quality Checks
- Analysis Performed
- Key Business Questions
- Planned Power BI Dashboard
- Business Insights and Recommendations
- Project Workflow
- How to Run the Project
- Data Model
- Important Data Considerations
- Repository Structure
- Skills Demonstrated
- Future Improvements
Project Overview
E-commerce businesses need to understand what drives sales, which products and categories perform well, how customers purchase, and where orders are being cancelled or returned. This project turns raw e-commerce CSV data into validated, analysis-ready tables and business-focused reporting.

The workflow is designed to be reproducible:
1. Import the source CSV files into SQL Server.
2. Profile the tables and inspect their structure.
3. Identify duplicates, missing values, inconsistent formats, invalid relationships, and suspicious values.
4. Preserve the source data and prepare cleaned working tables.
5. Validate the cleaned data with row counts and quality checks.
6. Use SQL queries to answer business questions.
7. Connect the validated data to Power BI and build an interactive dashboard.
Business Problem
The business lacks a single, validated view of sales performance, product contribution, customer purchasing behavior, and order outcomes. Without this view, decision-makers may struggle to identify high-performing products, understand sales changes over time, recognize repeat-purchase behavior, and monitor cancellation or return patterns.

Problem statement:
How can e-commerce transaction data be cleaned and analyzed to measure sales performance, identify valuable products and customers, and monitor order outcomes so that the business can make better data-driven decisions?
Project Objectives
- Assess the completeness, consistency, and reliability of the four source tables.
- Detect and investigate duplicate records and duplicate business keys.
- Identify missing values and invalid or suspicious values.
- Standardize text fields such as product categories.
- Validate primary-key and foreign-key relationships.
- Calculate sales and order KPIs using SQL.
- Analyze monthly trends, category performance, top products, and customer behavior.
- Present the results in a clear, interactive Power BI dashboard.
Tools and Technologies
Tool	Purpose
SQL Server	Store relational tables and perform cleaning, validation, and analysis
SQL Server Management Studio (SSMS)	Run SQL scripts and inspect results
Power BI Desktop	Build the planned interactive dashboard
Power Query	Optional final shaping of report-specific fields
GitHub	Version control and project presentation


Dataset and Tables
The project uses four imported CSV datasets:
Table	Role	Typical analysis
customers	Customer details	Customer counts and customer-to-order relationships
orders	Order-level records	Order dates, statuses, order counts, and order outcomes
order_items	Products purchased within orders	Quantity, item price, item-level sales, and product contribution
products	Product details	Product names, categories, and list prices


Important: Confirm the exact column names and data types in your SQL Server database before running queries. The queries and metric definitions should match the actual schema and documented business rules.
Data Cleaning and Quality Checks
Cleaning is performed in SQL Server so that the logic can be reviewed, repeated, and validated. The original imported tables should be retained as source copies; perform changes on clearly named working or cleaned tables.
1. Table profiling
- Count rows in each table.
- Inspect column names, SQL data types, and nullability.
- Review sample records.
- Check date ranges and order-status distributions.
2. Duplicate detection
- Check for exact duplicate rows.
- Check whether order_id appears more than once in orders.
- Check duplicate customer and product identifiers.
- Check repeated (order_id, product_id) combinations in order_items.
Duplicate-looking records should be investigated before deletion. Multiple rows for the same order can be legitimate in some schemas, and repeated order-product combinations may be valid if the source represents separate line items.
3. Missing-value checks
- Identify null identifiers, dates, quantities, and prices.
- Count missing discount codes separately, because a discount code may legitimately be absent when no discount was applied.
- Quantify how many sales records have a missing unit price.
Do not automatically replace missing prices with zero. Zero would imply a known zero-price sale and can understate revenue. Investigate the source or exclude affected records from price-based metrics while reporting the limitation.
4. Data types and formatting
- Verify that identifiers use compatible data types across related tables.
- Ensure order dates are stored as date/datetime values.
- Ensure quantity, unit price, discount, and list price use suitable numeric types.
- Trim leading/trailing spaces in text columns.
- Standardize category labels where differences are only casing or whitespace, while retaining the original values if auditability is needed.
5. Relationship and integrity checks
- Find orders that do not match a customer.
- Find order items without a matching order.
- Find order items without a matching product.
- Confirm that primary keys and foreign keys exist and are enabled.
- Validate that key columns are non-null before creating primary keys.
6. Outlier and business-rule checks
- Flag zero or negative quantities and prices for investigation.
- Compare item prices with product list prices.
- Investigate unusually high quantities or values.
- Do not automatically treat a transaction price above the current list price as an error: prices may change over time, and the datasets may contain historical pricing or different price definitions.
7. Post-cleaning validation
After every major cleaning step:
- Compare source and cleaned row counts.
- Re-run duplicate and null checks.
- Re-run orphan-record checks.
- Confirm key constraints.
- Record the number of rows changed, removed, corrected, or retained for investigation.
Analysis Performed
The SQL analysis is organized into business-focused sections.
Sales and order performance
- Total order count and order counts by status.
- Completed-order sales based on order-item quantity and unit price.
- Average order value (AOV).
- Monthly sales and month-over-month change.
- Cancellation and return rates, overall and by month.
Product and category performance
- Sales and units sold by product.
- Sales by category.
- Top 10 products by sales.
- Category share of total sales.
- Number of distinct orders containing each product or category.
Customer behavior
- Number of customers who placed orders.
- Top customers by completed-order sales.
- Completed-order frequency by customer.
- One-time versus repeat purchasers.
- Customer purchasing contribution, where the available fields support it.
Data-quality impact
- Missing-price record counts.
- Orphan records and duplicate-key checks.
- Differences between transaction prices and current product list prices.
- Validation of the data used in each KPI.
Key Business Questions
1. How many orders were placed, completed, cancelled, or returned?
2. What are the total completed-order sales and average order value?
3. How do sales change month over month?
4. Which product categories generate the most sales?
5. Which 10 products contribute the most sales?
6. Which customers contribute the most completed-order sales?
7. What share of purchasing customers place more than one completed order?
8. How do cancellation and return rates change over time?
9. Are missing prices or invalid relationships affecting the reliability of the analysis?
10. Which categories or products should be reviewed for growth opportunities?
Planned Power BI Dashboard
The intended dashboard is a single-page executive overview with clear KPIs, simple comparisons, and interactive filters.
KPI cards
- Completed Sales
- Total Orders
- Average Order Value
- Purchasing Customers
Visuals
- Monthly Sales Trend: line chart of completed sales by month.
- Sales by Category: bar chart comparing category sales.
- Top 10 Products by Sales: horizontal bar chart.
- Cancellation and Return Trend: line chart showing the rates by month.
- Category Performance Matrix: category by month, with sales values and conditional formatting.
Slicers
- Order date
- Product category
- Order status, if useful and consistent with the chosen KPI definitions
Dashboard design principles
- Keep the layout clean and readable.
- Use consistent formatting for currency, percentages, and dates.
- Sort monthly labels chronologically rather than alphabetically.
- Give every KPI a clear definition.
- Use tooltips for extra context instead of crowding the page.
- Validate each Power BI KPI against a corresponding SQL query.
Business Insights and Recommendations
The following are analysis areas, not confirmed findings. Populate this section with actual results after running the final SQL queries and validating the Power BI measures.
Insight 1 — Monthly sales performance
Evidence to add: strongest and weakest sales months, monthly sales values, and month-over-month percentage change.
Possible action: investigate seasonal patterns, campaigns, stock availability, and changes in product mix during stronger or weaker months.
Insight 2 — Product and category contribution
Evidence to add: leading categories, top 10 products, and each category's share of completed sales.
Possible action: review inventory and merchandising for high-contribution products and assess whether low-contribution categories need promotion, assortment changes, or further investigation.
Insight 3 — Cancellation and return patterns
Evidence to add: overall rates, monthly trends, and any meaningful differences by category or product where the data supports the comparison.
Possible action: investigate possible causes such as delivery issues, product descriptions, customer expectations, or stock problems. Treat these as hypotheses until additional evidence confirms them.
Project Workflow
1. Import: Load the four CSV files into SQL Server.
2. Profile: Inspect schemas, row counts, sample rows, and value distributions.
3. Clean: Resolve verified duplicate records, standardize formats, and handle missing or invalid values using documented rules.
4. Validate: Recheck data quality and relational integrity.
5. Analyze: Run SQL queries for sales, products, categories, customers, and order outcomes.
6. Visualize: Connect Power BI to the cleaned tables or analysis views and create the dashboard.
7. Communicate: Record three evidence-based insights, recommendations, and metric definitions.
How to Run the Project
Requirements
- SQL Server and SQL Server Management Studio (SSMS)
- The four source CSV files
- Power BI Desktop for the reporting stage
Steps
1. Create or select the project database in SQL Server.
2. Import the four CSV files as relational tables.
3. Confirm table names and column names using Object Explorer or INFORMATION_SCHEMA.COLUMNS.
4. Keep the imported source tables unchanged and create cleaned working tables or a documented cleaning layer.
5. Run profiling and data-quality checks before applying changes.
6. Apply only verified corrections; keep a record of any rows removed or changed.
7. Run post-cleaning validation queries.
8. Execute the analysis queries and save the results needed for the report.
9. In Power BI Desktop, choose Get Data → SQL Server, enter the server and database, and select the validated tables or views.
10. Build the dashboard and compare its KPI values with SQL results.
Data Model
The expected logical relationships are:
- customers 1 → many orders
- orders 1 → many order_items
- products 1 → many order_items
Conceptual relationship diagram:
customers
    |
    | 1-to-many
    v
  orders
    |
    | 1-to-many
    v
order_items
    ^
    | many-to-1
    |
 products
Create these relationships only after verifying that the referenced key columns are unique and non-null where required, and that no orphan records remain. Use the actual key names from your database.
Important Data Considerations
- Define sales consistently: a common starting point is quantity * unit_price at order-item level. If discounts, taxes, shipping, refunds, or returns are represented separately, decide whether the KPI is gross sales, net sales, or completed-order item sales.
- Define order status rules: use the exact status values in the dataset. Do not assume that status labels or business meaning are consistent without checking them.
- Avoid double-counting orders: joining order-level and item-level tables can repeat order fields for each item. Aggregate at the correct grain before calculating order-level metrics such as AOV.
- Missing unit prices: report their impact and document how they are treated in sales calculations.
- Current versus historical prices: a product's current list price may not equal its transaction price at the time of purchase.
- Duplicates: remove only records confirmed to be accidental duplicates; do not delete valid transactions solely because some fields match.
- Reproducibility: retain the source data and document the cleaning rules so the analysis can be audited and repeated.
Repository Structure
A suggested GitHub structure is:
e-commerce-sales-customer-insights/
├── README.md
├── data/
│   └── README.md                 # Dataset description; avoid committing private data
├── sql/
│   ├── 01_data_profiling.sql
│   ├── 02_data_cleaning.sql
│   ├── 03_data_validation.sql
│   └── 04_business_analysis.sql
├── powerbi/
│   ├── ecommerce_dashboard.pbix
│   └── screenshots/
└── docs/
    └── data_dictionary.md
Adapt the file names to match your actual scripts. Do not commit credentials, connection strings containing passwords, or sensitive customer information. Check the dataset's license and sharing terms before publishing the raw CSV files.
Skills Demonstrated
- SQL Server and SSMS
- Data profiling and data cleaning
- Duplicate and missing-value analysis
- Data type and text standardization
- Primary-key / foreign-key validation
- Joins, aggregations, CTEs, and window functions
- KPI design and business metric validation
- Sales trend, product, category, and customer analysis
- Power BI dashboard design and data storytelling
- Documentation and reproducible analysis
Future Improvements
- Add a formal data dictionary with definitions and allowed values.
- Create reusable SQL views for dashboard-ready metrics.
- Add a calendar/date dimension for reliable time intelligence.
- Add a documented sales definition covering discounts, tax, shipping, refunds, and returns.
- Automate data-quality checks and record validation results.
- Add dashboard screenshots and final, numeric insights.
- Compare product and category performance over consistent time periods.
- Add customer cohort or retention analysis if the available data supports it.
Final Note
This README describes the intended project workflow and analysis scope. Before publishing, replace the planned dashboard status and insight placeholders with your actual validated results, confirm the exact schema and status values, and add a screenshot of the completed Power BI dashboard.
