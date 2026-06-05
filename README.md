# E-Commerce Orders — SQL Querying & Data Exploration

For Task 3 of my internship, I queried an e-commerce sales database using SQL Server Management Studio. I practised SELECT, WHERE, ORDER BY, and GROUP BY statements alongside aggregation functions — COUNT, SUM, and AVG — to extract and summarise meaningful insights from the dataset.

---

##  Table of Contents
- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Queries Performed](#queries-performed)
- [Screenshots](#screenshots)
- [Tools Used](#tools-used)
- [Key Takeaways](#key-takeaways)

---

##  Project Overview

This project covers the SQL querying and data exploration phase of an e-commerce sales dataset, completed as Task 3 of my data analytics internship. The cleaned dataset from Task 1 was imported into SQL Server Management Studio (SSMS) where a series of structured queries were written and executed to retrieve, filter, sort, group, and aggregate data across multiple columns.

---

##  Dataset

The dataset is the cleaned e-commerce orders table from Task 1, imported into SQL Server as `[e-commerce sales data]`. It contains 1,200 records across 13 columns including `OrderID`, `Product`, `Quantity`, `UnitPrice`, `TotalPrice`, `Date`, `OrderStatus`, `PaymentMethod`, `ReferralSource`, `CouponCode`, and `ItemsInCart`.

---

##  Queries Performed

### 1. SELECT Statements
Retrieved all records and specific columns from the dataset:
```sql
SELECT * FROM [e-commerce sales data]

SELECT OrderID, Product, Quantity, Date, OrderStatus, ReferralSource, TotalPrice
FROM [e-commerce sales data]

SELECT TOP 10 * FROM [e-commerce sales data]
```

### 2. WHERE Clause — Filtering Records
Filtered records based on specific conditions:
```sql
-- Orders with Shipped status
SELECT * FROM [e-commerce sales data]
WHERE OrderStatus = 'Shipped'

-- Orders with TotalPrice above 1000
SELECT OrderID, Product, TotalPrice
FROM [e-commerce sales data]
WHERE TotalPrice > 1000

-- Credit Card orders that were Cancelled
SELECT * FROM [e-commerce sales data]
WHERE PaymentMethod = 'Credit Card' AND OrderStatus = 'Cancelled'

-- Orders from Instagram or Facebook
SELECT * FROM [e-commerce sales data]
WHERE ReferralSource = 'Instagram' OR ReferralSource = 'Facebook'
```

### 3. ORDER BY — Sorting Records
Sorted records in ascending and descending order:
```sql
-- Highest to lowest TotalPrice
SELECT OrderID, Product, TotalPrice
FROM [e-commerce sales data]
ORDER BY TotalPrice DESC

-- Lowest to highest TotalPrice
SELECT OrderID, Product, TotalPrice
FROM [e-commerce sales data]
ORDER BY TotalPrice ASC

-- Products in alphabetical order
SELECT * FROM [e-commerce sales data]
ORDER BY Product ASC
```

### 4. GROUP BY — Aggregating Data
Grouped records to summarise data by category:
```sql
-- Total orders per product
SELECT Product, COUNT(*) AS TotalOrders
FROM [e-commerce sales data]
GROUP BY Product

-- Number of orders per order status
SELECT OrderStatus, COUNT(*) AS NumberOfOrders
FROM [e-commerce sales data]
GROUP BY OrderStatus

-- Total revenue per product
SELECT Product, SUM(TotalPrice) AS TotalRevenue
FROM [e-commerce sales data]
GROUP BY Product
ORDER BY TotalRevenue DESC

-- Total quantity sold per product
SELECT Product, SUM(Quantity) AS TotalQuantitySold
FROM [e-commerce sales data]
GROUP BY Product

-- Average order value per payment method
SELECT PaymentMethod, AVG(TotalPrice) AS AvgOrderValue
FROM [e-commerce sales data]
GROUP BY PaymentMethod

-- Average quantity per referral source
SELECT ReferralSource, AVG(Quantity) AS AvgQuantity
FROM [e-commerce sales data]
GROUP BY ReferralSource

-- Revenue per product for Shipped orders only
SELECT Product, SUM(TotalPrice) AS Revenue
FROM [e-commerce sales data]
WHERE OrderStatus = 'Shipped'
GROUP BY Product
ORDER BY Revenue DESC

-- Orders and total revenue per referral source
SELECT ReferralSource, COUNT(*) AS Orders, SUM(TotalPrice) AS TotalRevenue
FROM [e-commerce sales data]
GROUP BY ReferralSource
ORDER BY Orders DESC

-- Coupon code usage and revenue generated
SELECT CouponCode, COUNT(*) AS TimesUsed, SUM(TotalPrice) AS Revenue
FROM [e-commerce sales data]
GROUP BY CouponCode
ORDER BY Revenue DESC
```

---

##  Screenshots

### SELECT & WHERE Statements
![SELECT and WHERE](sql-queries-select-where.png)

### WHERE with Results
![WHERE Results](sql-queries-where-results.png)

### ORDER BY & GROUP BY
![ORDER BY and GROUP BY](sql-queries-orderby-groupby.png)

### Aggregations
![Aggregations](sql-queries-aggregations.png)

---

##  Tools Used

- Microsoft SQL Server Management Studio (SSMS)
- SQL Server 17.0

---

##  Key Takeaways

- SQL is a powerful tool for slicing and filtering large datasets quickly without altering the original data.
- Combining `WHERE` with `GROUP BY` allows for more targeted aggregations — for example, calculating revenue only for shipped orders.
- `ORDER BY` paired with aggregation functions like `SUM` makes it easy to rank products or categories by performance.
- Coupon code and referral source analysis through SQL can directly inform marketing and sales strategy decisions.
- Writing and executing queries in SSMS reinforced the importance of clean, well-structured data — bad data types or inconsistent values would have broken several of these queries.

