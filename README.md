# LITA_CapstoneProject_Documentation

### Project Title: Sales Performance Analysis for a Retail Store 


[Project Overview](#project-overview)

[Data Sources](#data-sources)

[Tools Used](#tools-used)

[Data Cleaning and Preparations](#data-leaning-and-preparations)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Data Visualization](#data-visualization)

### Project Overview

```
This project is tasked with analyzing the sales performance of a retail store.
The Data Analysis of this project aims to explore sales data to uncover key insights such as top-selling products, regional performance, and monthly sales trends to produce an interactive Power BI dashboard that highlights these findings and
to make reasonable decisions which then enable us to tell compelling stories around our data from the insight gotten and to know the best performance from our data.
```

### Data Source

```
The primary source of Data used here is Data Sale.csv and this is an open source data that can be freely downloaded from an open source online such as Capstone or FRED or kaggle or any other repository site.
```

### Tools Used

```
- Microsoft Excel 
    1. For Data Cleaning [Download Here](https://www.microsoft.com)
    2. For Data Analysis
    3. For Data Visualization
       
- SQL - Structured Query language for Quering of Data
- Microsft Power Bi Desktop
- GitHub for Portifolio Building
```

### Data Cleaning and Preparations

```
In the initial phase of the data cleaning and preparations, I perform the following actions;
1. Data Loading and Inspection
2. Handling missing variables
3. Removing duplicates
4. Data cleaning and formatting
```

### Exploratory Data Analysis

```
EDA involved the exploring of the Data to answer some questions about the Data such as;
- What is the total sales by product?
- What is the total sales by region?
- What is the total sales by month?
- What is the average sales per product?
- What is the total revenue by region?
- What is the total units of products sold?
```
### Data Analysis


Microsoft Excel
```
[LITASalesData_Solution.xlsx](https://github.com/user-attachments/files/17653856/LITASalesData_Solution.xlsx)

```


SQL

This is where we include some basic lines of code or queries during analysis;

  ```SQL
create DATABASE LITAPROJECT; 
SELECT * FROM [dbo].[LITASalesData]

--- The total sales for each product category ---
SELECT Product, SUM(totalsales) AS ProductTotalSales
FROM [dbo].[LITASalesData]
GROUP BY Product
ORDER BY ProductTotalSales 

--- The number of sales transactions in each region ---
SELECT Region, SUM (TotalSales) AS SalesTransaction 
FROM [dbo].[LITASalesData] GROUP BY Region
ORDER BY SalesTransaction 

--- The highest-selling product by total sales value--
SELECT TOP(1) Product, MAX(totalsales) AS TotalProductSold,
sum(totalsales) AS  TotalHighestSellingProduct
FROM [dbo].[LITASalesData]
GROUP BY Product 
ORDER BY TotalProductSold DESC

---  Total revenue per product---
SELECT Product, sum(totalsales) AS TotalRevenue FROM [dbo].[LITASalesData]
GROUP BY Product 
ORDER BY TotalRevenue 

---  Monthly sales totals for the current year ----
SELECT YEAR(OrderDate) AS CurrentYear, MONTH(OrderDate) AS MonthlySales, 
SUM(totalsales) AS Monthly_Sales_Total
FROM [dbo].[LITASalesData]
GROUP BY YEAR(OrderDate), MONTH(OrderDate)
ORDER BY YEAR(OrderDate) DESC;

--- 6. The top 5 customers by total purchase amount ---
SELECT TOP (5) CustomerId, SUM(totalsales) AS TotalPurchase 
FROM [dbo].[LITASalesData]
GROUP BY CustomerId
ORDER BY TotalPurchase

 --- Percentage of total sales contributed by each region ---
WITH RegionSales AS
SELECT Region, SUM(Quantity * UnitPrice) AS TotalSales FROM [dbo].[LITASalesData]
GROUP BY Region),
TotalSales AS (
SELECT SUM(TotalSales) AS GrandTotal FROM RegionSales)
SELECT RS.Region, RS.TotalSales,
(RS.TotalSales * 100.0/TS.GrandTotal) AS SalesPercentage
FROM RegionSales RS, TotalSales TS;

--- Products with no sales in the last quarter---
SELECT DISTINCT Product FROM [dbo].[LITASalesData]
WHERE Product NOT IN (SELECT Product FROM [dbo].[LITASalesData]
  WHERE OrderDate >= DATEADD(QUARTER, -1, GETDATE())
  )

  ```

### Data Visualization 

```Img

![SalesData](https://github.com/user-attachments/assets/8dc0c8aa-0e24-46fd-95a9-25184b1bbf2a)

![SalesData](https://github.com/user-attachments/assets/1b6810a1-345b-4dc9-b9f4-95e2c9da79dd)

 ```

