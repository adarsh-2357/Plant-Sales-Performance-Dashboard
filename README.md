# Plant Sales Performance Dashboard

## Overview
The Plant Sales Performance Dashboard is an interactive Power BI report designed to analyze sales, quantity sold, and gross profit performance across customers, product categories, and geographic regions. The dashboard provides a clear view of business performance using Year-to-Date (YTD) and Previous Year-to-Date (PYTD) comparisons, customer profitability analysis, and product-level insights.

This project demonstrates the use of Power BI for data modeling, DAX calculations, business KPI creation, and multi-visual analytical storytelling. It reflects essential skills for data analyst and BI developer roles.

---

## Dataset Description
The dataset used for this dashboard contains multiple tables, including:

### Sales Table
- Product_ID  
- Account_ID  
- Sales_US  
- COGS_US  
- Quantity  
- Date_Time  

### Account Table
- Account_ID  
- Account Name  
- Country  
- Postal Code  
- Latitude  
- Longitude  
- Address fields  

### Product Table
- Product_ID  
- Product Type (Indoor, Outdoor, Landscape)  
- Product Group  
- Product Family  
- Product Size  
- Product Name  

### Date Table
- Year  
- Quarter  
- Month  
- Month_Name  
- Date  

These tables were connected using a star-schema model to build relationships and drive the analytical structure of the dashboard.

---

## Key Features
- Multi-page Power BI dashboard with drilldown capabilities.
- Segmentation by country, product type, customer account, and time period.
- Year-To-Date (YTD) and Previous Year-To-Date (PYTD) comparison metrics.
- Trend analysis for sales and quantity across months and quarters.
- Customer profitability classification using scatter charts.
- Product category-wise contribution analysis.

---

## KPIs Included
The following business KPIs were created using DAX:

- Sales YTD  
- Sales PYTD  
- Quantity Sold YTD  
- Gross Profit Percentage (GP%)  
- Monthly Increase/Decrease in Quantity  
- Customer Value vs Margin performance  
- Product Type-wise contribution metrics  
- Quarter-wise sales and quantity KPIs  

These KPIs support real-time performance monitoring and help identify high-impact areas of the business.

---

## Data Model
A star-schema data model was created using:

- Fact Table: Sales  
- Dimension Tables: Account, Product, Date  

Relationships:
- Sales[Product_ID] → Product[Product_ID]  
- Sales[Account_ID] → Account[Account_ID]  
- Sales[Date_Time] → Date[Date]  

This structure ensures efficient DAX calculations and accurate aggregations across time and category slices.

---

## DAX Measures Used
Below are some of the DAX measures implemented:

```dax
Sales_Total = SUM(Sales[Sales_US])
Quantity_Total = SUM(Sales[Quantity])
COGS_Total = SUM(Sales[COGS_US])

Sales_YTD = TOTALYTD([Sales_Total], 'Date'[Date])
Quantity_YTD = TOTALYTD([Quantity_Total], 'Date'[Date])

Sales_PYTD = CALCULATE([Sales_YTD], SAMEPERIODLASTYEAR('Date'[Date]))

Gross_Profit = [Sales_Total] - [COGS_Total]
Gross_Profit_Percentage = DIVIDE([Gross_Profit], [Sales_Total], 0)

Value_YTD = [Sales_YTD]

Average_Order_Value = DIVIDE([Sales_Total], DISTINCTCOUNT(Sales[Account_ID]), 0)

YOY_Sales_Growth = DIVIDE([Sales_YTD] - [Sales_PYTD], [Sales_PYTD], 0)

```

## Visuals Included

- The dashboard includes the following visuals:
- KPI cards for Sales YTD, Quantity YTD, and Gross Profit %.
- Bar charts for YTD vs PYTD comparisons.
- Line charts for month-wise trends.
- Treemap showing country-wise performance.
- Scatter chart for customer profitability segmentation (Value YTD vs GP%).
- Waterfall chart to illustrate monthly variance.
- Slicers for quarter, product type, country, and year.
- Additional category-level charts for indoor, outdoor, and landscape product types.

## Insights Summary

- Key observations derived from the dashboard:
- Distinct seasonal trends were identified in both quantity sold and sales revenue.
- Gross Profit Percentage maintained consistent performance across the analyzed period.
- Certain countries and customer accounts contributed disproportionately to total sales, providing clear targets for business optimization.
- Product types (Indoor, Outdoor, Landscape) displayed different growth patterns, highlighting category-specific demand behavior.
- Customer profitability scatter analysis revealed high-value but low-margin accounts worth deeper investigation.

## How to Use
- Download the PBIX file from this repository.
- Open it using Power BI Desktop (Windows).
- Interact with slicers and visuals to explore different segments of the data.
- Review DAX formulas in the "Modeling" tab for learning or customization.
