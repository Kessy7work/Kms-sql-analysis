# Kms-sql-analysis
SQL-based analysis of Kultra Mega Stores inventory and sales data, focusing on sales trends, customer insights, and shipping costs.
Summary of Cleaning Performed:
Column names standardized (no spaces or symbols)

Text fields cleaned and capitalized consistently

Currency symbols and commas removed from numeric fields

Converted Sales, Profit, and ShippingCost to numeric

Dates (OrderDate, ShipDate) converted to proper date format

Dropped any completely empty rows

STEP-BY-STEP USING SQL:

Step 1: Load the Dataset into a SQL Database

Step 2: Write SQL Queries for Each Scenario

Case Scenario I:
1. Product category with highest sales:

SELECT Category, SUM(Sales) AS TotalSales
FROM Orders
GROUP BY Category
ORDER BY TotalSales DESC
LIMIT 1;

2. Top/Bottom 3 regions in sales:

SELECT Region, SUM(Sales) AS TotalSales
FROM Orders
GROUP BY Region
ORDER BY TotalSales DESC
LIMIT 3; -- For Top 3

-- Reverse ORDER BY ASC for Bottom 3

3. Total sales of appliances in Ontario:

SELECT SUM(Sales)
FROM Orders
WHERE Category = 'Appliances' AND Region = 'Ontario';

4. Bottom 10 customers (Sales) advice:

SELECT CustomerName, SUM(Sales) AS TotalSales
FROM Orders
GROUP BY CustomerName
ORDER BY TotalSales ASC
LIMIT 10;

Analyze their order frequency and recommend upselling or retention strategies.

5. Shipping method with highest cost:
SELECT ShipMode, SUM(ShippingCost) AS TotalCost
FROM Orders
GROUP BY ShipMode
ORDER BY TotalCost DESC
LIMIT 1;
---
Case Scenario II:
6. Most valuable customers + purchases:

SELECT CustomerName, SUM(Sales) AS TotalSales
FROM Orders
GROUP BY CustomerName
ORDER BY TotalSales DESC
LIMIT 5;

7. Top small business customer:

SELECT CustomerName, SUM(Sales) AS TotalSales
FROM Orders
WHERE Segment = 'Small Business'
GROUP BY CustomerName
ORDER BY TotalSales DESC
LIMIT 1;

8. Most orders by corporate customer:

SELECT CustomerName, COUNT(*) AS OrderCount
FROM Orders
WHERE Segment = 'Corporate'
GROUP BY CustomerName
ORDER BY OrderCount DESC
LIMIT 1;

9. Most profitable consumer customer:

SELECT CustomerName, SUM(Profit) AS TotalProfit
FROM Orders
WHERE Segment = 'Consumer'
GROUP BY CustomerName
ORDER BY TotalProfit DESC
LIMIT 1;

10. Returned items + segment:

SELECT DISTINCT CustomerName, Segment
FROM Returns R
JOIN Orders O ON R.OrderID = O.OrderID;

11. Was shipping cost aligned to priority?

Group by OrderPriority and ShipMode, calculate total shipping cost per group.
