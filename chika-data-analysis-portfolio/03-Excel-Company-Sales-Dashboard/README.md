# 03-Excel-Company-Sales-Dashboard

*A tidy workbook that answers three fast questions: what sold, when it moved, and where to look next.*

## Purpose

Turn raw transactions into quick, visual answers:

* **Which products drive total sales?** (column chart)
* **How is demand moving day-to-day?** (line chart)
* **What are the average sales by product/period?**

## Files

```
03-Excel-Company-Sales-Dashboard/
├─ workbooks/
│  └─ ASSIGNMENT 3. CHIKA CELESTINE IROEGBULEM.xlsx
├─ outputs/
│  └─ screenshots/
│     ├─ Colum sales by product.png
│     └─ Daily sales trend .png
└─ README.md
```

## Dataset (columns)

Date · Product · Region (if available) · Units Sold · Unit Price · Discount % (if any) · **Total Sales** (= Units \* Price \* (1 − Discount)).

## What I did (Excel)

1. Cleaned types (dates, numbers) and added **Total Sales** if missing.
2. Built a **PivotTable** for **Total Sales by Product** → **Clustered Column** chart.
3. Summarized **Total Sales by Date** → **Line** chart for daily trend.
4. Added an **AVERAGE SALES** sheet using `AVERAGEIFS` for product/day averages.

## Key takeaways (from this workbook)

* One product clearly **leads total sales**; others trail by a wide margin.
* The **daily trend** shows noticeable spikes—useful for spotting promo days or stockouts.
* Average sales highlight **consistency vs. volatility** across products.

## How to view

1. Open **`workbooks/ASSIGNMENT 3. CHIKA CELESTINE IROEGBULEM.xlsx`**.
2. Sheets: **Pivot Table**, **COLUM** (column chart), **LINE CHART**, **AVERAGE SALES**.
3. For a quick glance, see images in **`outputs/screenshots/`**.

## Skills & tools

**Excel:** PivotTables, SUMIFS/AVERAGEIFS, column & line charts, light data cleaning, KPI summarization.

