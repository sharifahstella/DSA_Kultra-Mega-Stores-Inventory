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
![Line graph](https://github.com/sharifahstella/DSA_Kultra-Mega-Stores-Inventory/blob/main/top3.PNG) 

Therefore West ,Ontario and Parie top 3 regions respectively in sales leading to the most seen regions profitably
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
![Line graph](https://github.com/sharifahstella/DSA_Kultra-Mega-Stores-Inventory/blob/main/bottom3.PNG) 

However the bottom 3 regions that include Nunavit,Northwest Territories and Yukon call for the most attention to improve on the sales in the regions.

- Total sales of appliances in Ontario

```
SELECT
    SUM(Sales) AS TotalSalesOfAppliances
FROM 
    [dbo].[KMS Sql Case Study]
WHERE 
    Product_Category = 'Appliances'
    AND Region = 'Ontario';

```
![Line graph](https://github.com/sharifahstella/DSA_Kultra-Mega-Stores-Inventory/blob/main/null.PNG)

Therefore there was no total sales of appliances in Ontario which also calls for the most seen region that has to increase on the sales in the region of ontario.

- Recommendations to increase revenue from the bottom 10 customers

```
SELECT TOP 10
    Customer_Segment,
    Customer_Name,
    SUM(Sales) AS TotalSales
FROM 
    [dbo].[KMS Sql Case Study]
GROUP BY 
    Customer_Segment,
    Customer_Name
ORDER BY 
    TotalSales ASC;

```
![Line graph](https://github.com/sharifahstella/DSA_Kultra-Mega-Stores-Inventory/blob/main/cate2.PNG)  

Recommendations:
- 1. Personalized Engagement: Assign account managers to follow up and understand why spend is low.
- 2. Targeted Promotions: Offer exclusive discounts or loyalty rewards.
- 3. Cross-Selling: Recommend related products based on prior purchases.
- 4. Feedback Collection: Survey customers to learn about unmet needs.
- 5. Streamlined Ordering: Simplify reorder processes.
 
- Shipping method with the highest shipping cost

```
SELECT TOP 1
    Ship_Mode,
    COUNT(Shipping_Cost) AS TotalShippingCost
FROM 
    [dbo].[KMS Sql Case Study]
GROUP BY 
    Ship_Mode
ORDER BY 
    TotalShippingCost DESC;

```
![Line graph](https://github.com/sharifahstella/DSA_Kultra-Mega-Stores-Inventory/blob/main/ship.PNG)

Therefore Regular Air had the highest shipping cost

###Summary of Insights
- ✅ Categories and regions driving most revenue are critical for growth.
- ✅ Low-performing regions and customers offer opportunities for targeted initiatives.
- ✅ Shipping methods should be reviewed for cost efficiency.

## Case Scenario II — Analysis & SQL Queries

- most valuable customers, and what products or services do they typically purchase

```
SELECT TOP 5
    Customer_Segment,
    Customer_Name,
    SUM(Sales) AS TotalSales
FROM 
    [dbo].[KMS Sql Case Study]
GROUP BY 
    Customer_Segment, Customer_Name
ORDER BY 
    TotalSales DESC;


SELECT 
    Customer_Segment,
    Customer_Name,
    Product_Category,
    SUM(Sales) AS CategorySales
FROM 
    [dbo].[KMS Sql Case Study]
WHERE 
    Customer_Segment IN (
        SELECT TOP 5 Customer_Segment
        FROM [dbo].[KMS Sql Case Study]
        GROUP BY Customer_Segment
        ORDER BY SUM(Sales) DESC
        
    )
GROUP BY 
    Customer_Segment, Customer_Name, Product_Category
ORDER BY 
    Customer_Segment, CategorySales DESC;

```

![image](https://github.com/user-attachments/assets/965f0c41-e690-458b-8257-8115a927e7ef)

![image](https://github.com/user-attachments/assets/74432272-b004-422c-8be8-7ca9dd81b092)

- small business customer with the highest sales

```
SELECT TOP 1 
    Customer_Segment,
    Customer_Name,
    SUM(Sales) AS TotalSales
FROM 
    [dbo].[KMS Sql Case Study]
WHERE 
    Customer_Segment = 'Small Business'
GROUP BY 
    Customer_Segment, Customer_Name
ORDER BY 
    TotalSales DESC;

```
![image](https://github.com/user-attachments/assets/76412398-e9ab-4056-8d45-a769827f3068)

The small bussiness customer is Dennis Kane to secure repeat business.

- Corporate Customer That placed the most number of orders in 2009 – 2012

```
SELECT TOP 1
    Customer_Segment,
    Customer_Name,
    COUNT(Order_ID) AS OrderCount
FROM 
    [dbo].[KMS Sql Case Study]
WHERE 
    Customer_Segment = 'Corporate'
    AND Order_Date BETWEEN '2009-01-01' AND '2012-12-31'
GROUP BY 
    Customer_Segment, Customer_Name
ORDER BY 
    OrderCount DESC;

```
![image](https://github.com/user-attachments/assets/0dbb5f63-c59d-49d5-b063-e7d99c4e4298)

Adam Hart was the corprate customer that placed a number of orders therefore may be a priority for volume-based incentives or preferred service agreements.

- consumer customer that was the most profitable one

```
SELECT TOP 1 
    Customer_Segment,
    Customer_Name,
    COUNT(Profit) AS TotalProfit
FROM 
    [dbo].[KMS Sql Case Study]
WHERE 
    Customer_Segment = 'Consumer'
GROUP BY 
    Customer_Segment, Customer_Name
ORDER BY 
    TotalProfit DESC;

```
![image](https://github.com/user-attachments/assets/c9bc15e6-3248-45f8-8289-14582651fe4f)

Christy Brittain was the most profitable customer that insight support strategies to grow profits in the Consumer segment.

- Which customer returned items, and what segment do they belong to?

```
SELECT DISTINCT
    o.[Customer_Name],
    o.[Customer_Segment]
FROM
      [dbo].[KMS Sql Case Study] o
INNER JOIN
    Order_Status s ON o.[Order_ID] = s.[Order_ID]
WHERE
    s.[Status] = 'Returned'
ORDER BY
    o.[Customer_Segment], o.[Customer_Name];

```
![image](https://github.com/user-attachments/assets/bf0176ef-abe9-443a-959f-78a87667b6a8)

- Did the company appropriately spend shipping costs based on Order Priority?

I analyzed shipping behavior by priority and shipping mode.

```
SELECT
    o.[Order_Priority],
    o.[Ship_Mode],
    COUNT(o.[Order_ID]) AS OrderCount,
    COUNT(o.[Shipping_Cost]) AS TotalShippingCost
FROM
    [dbo].[KMS Sql Case Study] o
GROUP BY
    o.[Order_Priority], o.[Ship_Mode]
ORDER BY
    o.[Order_Priority], o.[Ship_Mode];
```

![image](https://github.com/user-attachments/assets/1e0cee33-14e8-4e4b-9f4d-4786d9ca5d10)

### Summary of Recommendations
If you observe that Low or Medium priority orders often use Express Air, this indicates unnecessary shipping cost.
KMS should implement a shipping policy:
- Use Express Air only for Critical/High priority orders
- Use Delivery Truck for Medium/Low orders to reduce costs
- Regularly review shipping behavior to align with order urgency


