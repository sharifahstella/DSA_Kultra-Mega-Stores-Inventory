# DSA_Kultra-Mega-Stores-Inventory
# Company Overview
Kultra Mega Stores (KMS), headquartered in Lagos, specializes in office supplies and furniture. Its customer base includes:
- Individual consumers
- Small businesses (retail)
- Large corporate clients (wholesale)
  
This project supports the Abuja division by analyzing historical order data (2009–2012) to provide actionable insights.


 Dataset
Source: Excel file with orders from 2009–2012
Imported Table: KMS Case Study
Key Fields:
- Order_ID
- Order_Date
- Customer_Name
- Customer_Segment
- Region
- Product_Category
- Product_Sub_Category
- Product_Name
- Quantity
- Sales
- Profit
- Shipping_Cost
- Ship_Mode
- Order_Priority
- Returned

## Case Scenario I — Analysis & SQL Queries

- Which product category had the highest sales?

```
SELECT TOP 1
    Product_Category,
    SUM(Sales) AS TotalSales
FROM 
    [dbo].[KMS Sql Case Study]
GROUP BY 
    Product_Category
ORDER BY 
    TotalSales DESC;

```
Technology having the highest sales 

 ![Line graph](https://github.com/sharifahstella/DSA_Kultra-Mega-Stores-Inventory/blob/main/cate.PNG) 

- Top 3 and Bottom 3 regions in terms of sales

```
SELECT TOP 3
    Region,
    SUM(Sales) AS TotalSales
FROM 
    [dbo].[KMS Sql Case Study]
GROUP BY 
    Region
ORDER BY 
    TotalSales DESC;

```
![Line graph](https://github.com/sharifahstella/DSA_Kultra-Mega-Stores-Inventory/blob/main/cate.PNG) 

There fore with 
```
SELECT TOP 3
    Region,
    SUM(Sales) AS TotalSales
FROM 
    [dbo].[KMS Sql Case Study]
GROUP BY 
    Region
ORDER BY 
    TotalSales ASC;

```
![Line graph](https://github.com/sharifahstella/DSA_Kultra-Mega-Stores-Inventory/blob/main/cate.PNG) 
