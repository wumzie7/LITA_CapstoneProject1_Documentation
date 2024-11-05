# LITA_CapsoneProject_Documentation

### Sales Performance Analysis for a Retail Store 

### Project Overview

```
This project is tasked with analyzing the sales performance of a retail store.
The Data Analysis of this project aims to explore sales data to uncover key insights such as top-selling products, regional performance, and monthly sales trends. The goal is to produce an interactive Power BI dashboard that highlights these findings.
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
- What is the overall sales trend?
- Which product are top sellers?
- What is the total sales by product?
- What is the total sales by region?
- What is the total sales by month?
- What is the average sales per product?
- What is the total revenue by region?
- What is the total units of products sold?
```

This is where we include some basic lines of code or queries or even som of the DAX expressions used during analysis;

  ```SQL
  Create database LITAPROJECT; 
select * from [dbo].[LITASalesData]

--- 1. retrieve the total sales for each product category ---
select Product, sum(totalsales) as ProductTotalSales
from [dbo].[LITASalesData]
group by Product
order by ProductTotalSales 

--- 2. find the number of sales transactions in each region ---
select Region, sum (TotalSales) as SalesTransaction 
from  [dbo].[LITASalesData]group by Region
order by SalesTransaction 

--- 3. find the highest-selling product by total sales value--
select top(1) Product, max(totalsales) as TotalProductSold,
sum(totalsales) as  TotalHighestSellingProduct
from [dbo].[LITASalesData]
group by Product 
order by TotalProductSold desc

--- 4. calculate total revenue per product---
select Product, sum(totalsales) as TotalRevenue from [dbo].[LITASalesData]
group by Product 
order by TotalRevenue 

--- 5. calculate monthly sales totals for the current year ----
select Year(OrderDate) As CurrentYear, Month(OrderDate) As MonthlySales, 
Sum(totalsales) As Monthly_Sales_Total
From [dbo].[LITASalesData]
Group by Year(OrderDate), Month(OrderDate)
order by Year(OrderDate) desc;

--- 6. find the top 5 customers by total purchase amount ---
select top (5) CustomerId, sum(totalsales) As TotalPurchase 
from [dbo].[LITASalesData]
Group by CustomerId
order by TotalPurchase

 --- 7. calculate the percentage of total sales contributed by each region ---
with RegionSales as 
select Region, sum(Quantity * UnitPrice) as TotalSales from [dbo].[LITASalesData]
group by Region),
TotalSales as (
select sum(TotalSales) as GrandTotal from RegionSales)
select RS.Region, RS.TotalSales,
(RS.TotalSales * 100.0/TS.GrandTotal) as SalesPercentage
from RegionSales RS, TotalSales TS;

--- 8. identify products with no sales in the last quarter---
select distinct Product from [dbo].[LITASalesData]
where Product not in (select Product from [dbo].[LITASalesData]
  where OrderDate >= dateadd(quarter, -1, getdate())
  )
  ```

