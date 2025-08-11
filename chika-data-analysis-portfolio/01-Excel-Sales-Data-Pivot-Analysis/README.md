Sales Data Pivot Analysis (Excel)
From raw rows to insight — a clear arc from question to answer.

Overview
A compact sales dataset was shaped into a pivot-driven view of performance.
The goal: reveal which regions contribute most to total sales and make the result instantly scannable with a simple column chart and slicers.

Dataset
Columns (tidy table):

Date

Salesperson

Region

Product

Units Sold

Unit Price

Total Sales = Units Sold * Unit Price (or Final Sales if a discount column exists)

Business Questions
Which region generates the highest total sales?

How do totals change when I filter by Salesperson or Product?

Are there obvious gaps or peaks worth investigating?

Method (Excel)
Clean column names and confirm numeric types for Units Sold, Unit Price, Total Sales.

Add/verify Total Sales formula if missing.

Insert → PivotTable on the sales table.

Rows: Region

Values: Sum of Total Sales

(Optional) Filters/Slicers: Salesperson, Product

Insert → Column Chart from the pivot (rename to “Total Sales by Region”).

Format the chart and add slicers for quick, interactive views.

Key Findings (from this workbook)
North leads with 3,150 in total sales.

South follows with 3,000.

East trails at 990.

Grand Total: 7,140.
(Use slicers to see how this shifts by Salesperson and Product.)

Files & Structure
bash
Copy
Edit
01-Excel-Sales-Data-Pivot-Analysis/
├─ data/                      # sample/anonymised data (optional)
├─ workbooks/                 # Excel workbook(s)
├─ outputs/
│  └─ screenshots/            # images of charts/tables
└─ README.md                  # this file
Put your Excel file here: workbooks/ASSIGNMENT 1. CHIKA CELESTINE IROEGBULEM.xlsx

Add your chart image here: outputs/screenshots/total-sales-by-region.png

How to View
Open workbooks/*.xlsx and go to the pivotchart sheet.

Use the Region and Salesperson slicers to explore.

For a quick glance without downloading, see images in outputs/screenshots/.

Skills Demonstrated
Pivot tables, charting, basic data cleaning, aggregation logic, business interpretation.
