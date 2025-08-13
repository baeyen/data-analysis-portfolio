## 🧾 Project Overview

This project builds a **Power BI Dashboard** that tracks real-time inventory and supply chain metrics.  
It integrates data from multiple sources to provide clear visibility into stock levels, restocking trends, and supplier delivery performance.

---

## 🧠 Business Objectives

- Identify **products below reorder level**
- Track **inbound vs outbound movement** of inventory
- Monitor **supplier lead time** and **on-time delivery rates**
- Surface **inventory turnover** and **stock value** trends
- Flag **items not restocked in 30+ days**

---

## 🧰 Data Sources

- `Inventory_Levels`: Stock quantities, reorder thresholds, last restock dates  
- `Products`: Product name, category, unit cost, supplier info  
- `Suppliers`: Delivery performance, lead time in days  
- `Inventory_Transactions`: Inbound/Outbound stock movement

---

## 🔧 Key DAX Measures

- `TotalInbound`  
- `TotalOutbound`  
- `TotalStockValue`  
- `ReorderCount`  
- `AverageLeadTime`  
- `TurnoverRate`  
- `DaysSinceRestock`  
- `BelowReorder` (calculated column)

---

## 📈 Visuals & KPIs

- **Cards**: Total Stock Value, Reorder Count, Avg Lead Time  
- **Table**: Products Below Reorder  
- **Bar Chart**: Inventory Value by Product Category  
- **Matrix**: Supplier On-Time Performance  
- **Line Chart**: Inbound vs Outbound Over Time  
- **Pie Chart**: Stock Value by Warehouse  
- **Slicers**: Filter by Category, Supplier, Reorder Status

---

## 📂 Folder Contents

```

06-PowerBI-Inventory-SupplyChain-Dashboard/
├─ Inventory\_SupplyChain\_Dashboard.xlsx
├─ Inventory Movement Restocking Insights live data.pptx
├─ Inventory Movement Restocking Insights image.pptx
├─ My Inventory\_SupplyChain\_Project\_Summary.docx
├─ My PowerBI Project Step By Step Summary.docx
├─ Screenshot 2025-08-13 043720.png
├─ Screenshot 2025-08-13 043920.png
├─ power bi table tool.png
└─ power bi layot.png

```

---

## ✅ Project Highlights

📌 *Key Insight:*  
Over 25% of products were flagged for reorder, with several not restocked in over 30 days.  
Suppliers with high lead times also showed low on-time delivery rates, impacting fulfilment.

---

## 🛠 Tools Used

- **Power BI Desktop**  
- **DAX** for measures and calculated columns  
- **Excel** as source data  
- **PowerPoint** for presentation output  
- **PNG/PPTX** for visuals and executive summary

---

## 💼 Skills Demonstrated

- Data modeling (star schema, relationship building)  
- DAX for dynamic KPI calculations  
- Dashboard design and layout  
- Supply chain metrics analysis  
- Business storytelling with data
