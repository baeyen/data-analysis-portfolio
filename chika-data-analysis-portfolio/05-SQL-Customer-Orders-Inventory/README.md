# 05-SQL-Customer-Orders-Inventory (SQL Server)

*A brisk walk through real tables: what sold, who buys, what’s late, what’s low.*

## Purpose
Join **Customers, Orders, Order_Details, Products, Deliveries** in SQL Server to answer:
- Which **products drive revenue**?
- Who are our **most active / highest-value customers**?
- Where are **stock risks**?
- What’s our **delivery performance** and **undelivered** backlog?

## Data model (Northwind clone)
Tables imported from Excel → SQL Server:
- **Customers-sql**(CustomerID, CustomerName, Email, JoinDate, …)
- **Products-sql**(ProductID, ProductName, StockLevel, UnitPrice, …)
- **Orders-sql**(OrderID, CustomerID, OrderDate, …)
- **Order_Details-sql**(OrderID, ProductID, Quantity, UnitPrice)
- **Deliveries-sql**(OrderID, ProductID, DeliveryDate, ShippedQty)

## How to run
- SQL Server + SSMS. Use the **Northwind** database.
- Run scripts in `/sql` top → bottom. Export results you want as CSV to `/sample_outputs`.

## Queries (highlights)

**1) Missing customer emails (data quality)**
```sql
SELECT * 
FROM [dbo].[Customers-sql]
WHERE Email IS NULL;
````

**2) Duplicate customer names (potential dupes)**

```sql
SELECT CustomerName, COUNT(*) AS DuplicateCount
FROM [dbo].[Customers-sql]
GROUP BY CustomerName
HAVING COUNT(*) > 1;
```

**3) Low stock (reorder watchlist)**

```sql
SELECT ProductName, StockLevel
FROM [dbo].[Products-sql]
WHERE StockLevel < 20;
```

**4) Delivery performance by month (Avg delivery days)**

```sql
SELECT 
  FORMAT(d.DeliveryDate,'yyyy-MM') AS DeliveryMonth,
  AVG(DATEDIFF(DAY, o.OrderDate, d.DeliveryDate)) AS AvgDeliveryDays
FROM [dbo].[Orders-sql] o
JOIN [dbo].[Deliveries-sql] d ON o.OrderID = d.OrderID
WHERE d.DeliveryDate IS NOT NULL
GROUP BY FORMAT(d.DeliveryDate,'yyyy-MM');
```

**5) Revenue by product (best sellers)**

```sql
SELECT 
  p.ProductName,
  SUM(od.Quantity * od.UnitPrice) AS TotalRevenue
FROM [dbo].[Order_Details-sql] od
JOIN [dbo].[Products-sql] p ON od.ProductID = p.ProductID
GROUP BY p.ProductName
ORDER BY TotalRevenue DESC;
```

**6) Orders per customer (activity)**

```sql
SELECT 
  c.CustomerName,
  COUNT(o.OrderID) AS OrderCount
FROM [dbo].[Customers-sql] c
JOIN [dbo].[Orders-sql] o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerName
ORDER BY OrderCount DESC;
```

**7) Customer segmentation (by total spend)**

```sql
SELECT 
  o.CustomerID,
  c.CustomerName,
  SUM(od.Quantity * od.UnitPrice) AS TotalSpent,
  CASE 
    WHEN SUM(od.Quantity * od.UnitPrice) > 1000 THEN 'High'
    WHEN SUM(od.Quantity * od.UnitPrice) BETWEEN 500 AND 1000 THEN 'Medium'
    ELSE 'Low'
  END AS CustomerSegment
FROM [dbo].[Orders-sql] o
JOIN [dbo].[Order_Details-sql] od ON o.OrderID = od.OrderID
JOIN [dbo].[Customers-sql] c ON o.CustomerID = c.CustomerID
GROUP BY o.CustomerID, c.CustomerName
ORDER BY TotalSpent DESC;
```

**8) Undelivered orders (pending)**

```sql
SELECT 
  o.OrderID,
  c.CustomerName,
  p.ProductName
FROM [dbo].[Orders-sql] o
JOIN [dbo].[Order_Details-sql] od ON o.OrderID = od.OrderID
JOIN [dbo].[Products-sql] p ON od.ProductID = p.ProductID
JOIN [dbo].[Customers-sql] c ON o.CustomerID = c.CustomerID
LEFT JOIN [dbo].[Deliveries-sql] d ON o.OrderID = d.OrderID
WHERE d.DeliveryDate IS NULL;
```

05-SQL-Customer-Orders-Inventory/

├─ workbooks/

│  └─ Customer_Orders_Inventory_Project.xlsx

├─ docs/

│  └─ SQL_Project_Report_Customer_Orders.docx

├─ outputs/

│  └─ screenshots/

│     ├─ missing-emails.jpg

│     ├─ duplicate-names.jpg

│     ├─ low-stock.png

│     ├─ delivery-performance-by-month.jpg

│     ├─ revenue-by-product.jpg

│     ├─ orders-per-customer.jpg

│     ├─ customer-segmentation.jpg

│     ├─ customer-segmentation.jpg (2)

│     └─ undelivered-orders.jpg

└─ README.md


## What stands out (from sample runs)

* **Top revenue products** (example): `Product_7`, `Product_2`, `Product_3`.
* **Most active customer(s)** appear at the top of *Orders per Customer*.
* **Average delivery days** vary month to month → a signal to compare with stock/promo timing.
* **Pending/undelivered** query surfaces orders needing attention.

## Skills & tools

**T-SQL (SSMS):** joins, aggregates, date functions, CASE segmentation.
**Ops thinking:** inventory risk, delivery latency, customer value.
