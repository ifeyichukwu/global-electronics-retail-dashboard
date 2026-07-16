# Global Electronics Retailer — Power BI Dashboard

An end-to-end Power BI project analyzing sales performance for a global 
electronics retailer, covering revenue trends, product category performance, 
and regional breakdown across 2016–2021.

## Business Question
Which product categories and regions drive the most revenue, and where is 
performance changing over time?

## Data Source
[Maven Analytics — Global Electronics Retailer dataset](https://mavenanalytics.io/data-playground)
5 related tables: Sales, Products, Customers, Stores, Exchange Rates

## Tools Used
- Power BI Desktop (Power Query, Data Modeling, DAX)
- Star schema data modeling

## What's in the Dashboard
- KPI cards: Average Order Value, Total Orders, Total Revenue
- Revenue by Category
- Revenue by Continent
- Revenue trend by Year/Quarter/Month

## Key Findings
- Computers and Home Appliances drive the largest share of category revenue
- North America and Europe together account for the majority of revenue, 
  with Australia trailing
- An apparent sharp revenue "decline" in 2021 was investigated and found to 
  be a partial-year data cutoff (data ends Feb 20, 2021), not an actual 
  business decline — flagged directly on the dashboard rather than left 
  to mislead a viewer

## Data Quality Issues Found & Fixed
Real-world data rarely arrives clean. A few issues surfaced and were resolved 
during this build:

**1. Postal code type mismatch**
Power Query auto-converted the Zip Code column to Whole Number. Alphanumeric 
postal codes (e.g. Canadian format `V6B 1A1`) failed to convert, throwing 
errors on every affected row. Fixed by setting the column to Text at the 
original type-conversion step, rather than patching it downstream.

**2. Date locale mismatch**
Source dates were in `MM/dd/yyyy` format, but Power Query's default type 
conversion assumed `dd/MM/yyyy`, causing every date where the day exceeded 12 
to error out — and silently misreading the rest. Fixed using Power Query's 
"Change Type using Locale" option, explicitly set to English (United States).

**3. Currency-date granularity**
Currency Code alone wasn't a valid relationship key between Sales and 
Exchange Rates, since exchange rates change daily and the same currency 
appears across multiple dates. Built a composite key 
(`Currency & "_" & Date`) in both tables to create a unique, accurate join.

## Files
- `global-electronics-dashboard.pbix` — full Power BI file
- `/screenshots` — dashboard preview images

## Author
Gospel Arinze
[LinkedIn](https://linkedin.com/in/gospel-arinze-55590424a) | 
[Portfolio](https://datascienceportfol.io/gospelarinze2022)
