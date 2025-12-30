# SUPERSTORE-SALES-ANALYSIS-USING-SQL-FOR-ANALYSIS-AND-POWER-BI-FOR-VISUALIZATION
An excel file showing transactional records from a retail superstore, capturing customer, order, shipment and location details and more. The goal of this analysis is to explore sales and profit patterns, understand customer and shipping behavior, and generate actionable insights that support data-driven business and operational decisions.

![Dashboard](https://github.com/user-attachments/assets/b0164e12-6563-4190-a563-70d45cf48617)


## Table of Contents
-	Project Overview
  
-	Project Scope
  
-	Project Objectives
  
-	Expected Outcomes
  
-	Document Purpose
  
-	Use Case
  
-	Data Source
  
-	Data Cleaning and Preprocessing
  
-	Data Analysis and Insights
  
-	Data Visualization
  
- Recommendations
  
-	Conclusion
  
## Project Overview
This project involves the analysis of a Superstore sales dataset containing detailed information about customer orders, shipment modes, geographic locations, product categories, sales, and profit. The objective of the project is to develop an interactive dashboard that highlights sales performance, identifies revenue drivers, evaluates profitability, and uncovers operational inefficiencies.
The insights generated from this analysis are designed to help business stakeholders make data-driven decisions around pricing, discount strategies, inventory management, and customer targeting.

## Project Scope
The scope of this project includes:
-	Analyzing historical sales and profit performance
  
-	Evaluating customer purchasing behavior and segment contribution
  
-	Assessing shipping mode preferences
  
-	Identifying top-performing and underperforming product sub-categories
  
-	Examining the relationship between discount levels and profitability

##  Project Objectives
The key objectives of this analysis are to:
1.	Analyze overall business performance using revenue, profit, and transaction metrics
2.	Identify sales trends and seasonal patterns
3.	Evaluate customer segments and their revenue contribution
4.	Assess shipping mode preferences and cost implications
5.	Identify profitable and underperforming product sub-categories
6.	Provide actionable recommendations to improve profitability and efficiency

## Expected Outcomes
The analysis aims to deliver:
•	Total sales, profit, and transaction insights
•	Monthly sales trend analysis
•	Customer segment performance evaluation
•	Shipping mode usage patterns
•	Product sub-category performance insights
•	Discount vs profit analysis
•	Strategic recommendations for optimization

## Document Purpose
This report presents a comprehensive analysis of Superstore sales data, highlighting key performance indicators, operational challenges, and revenue opportunities. It serves as a decision-support document for management, helping guide pricing strategies, marketing efforts, and inventory planning.

## Use Case
Stakeholders benefiting from the Analysis
**1. Executive Management**
-	Strategic planning using revenue and profit insights
  
-	Identification of growth opportunities
  
**2. Sales and Marketing Teams**
-	Customer segment targeting
  
-	Discount and promotional optimization
  
**3. Operations and Logistics Teams**
-	Shipping mode optimization
  
-	Cost efficiency improvements
  
**4. Finance Teams**
- Profitability tracking
-	Forecasting and budgeting support

## Data Source
The dataset used in this project is a Superstore sales dataset sourced from Kaggle Website designed for analytical practice. It is presented in an Excel file with 104,856 rows and 19 columns respectively. The dataset includes key attributes essential for a comprehensive analysis such as;

## Field Description
The dataset contains transactional and customer-related information, where each row represents an order line. The key columns used in this analysis include:

-	Row ID – Unique identifier for each row
  
-	Order ID – Unique identifier for each order
  
-	Order Date – Date the order was placed
  
-	Ship Date – Date the order was shipped
  
-	Ship Mode – Shipping method used
  
-	Customer ID – Unique identifier for each customer
  
-	Segment – Customer segment (Consumer, Corporate, Home Office)
  
-	Country, State, City – Geographic details of the order

## Data Cleaning and Preprocessing

Before analysis, a thorough data cleaning process was carried out using SQL to ensure accuracy, consistency, and reliability of insights.

Steps taken include:

**Checking For Missing Values**
  
A comprehensive missing values check was conducted across all columns in the dataset using a single SQL aggregation query. The query calculated the total number of records and the number of NULL values present in each column by applying conditional counting with CASE WHEN statements. This approach allowed for an efficient and structured evaluation of data completeness.

```SQL
--Checking null values in all the columns
  SELECT
    SUM(CASE WHEN Order_ID IS NULL THEN 1 ELSE 0 END) AS Missing_OrderID,
    SUM(CASE WHEN Customer_ID IS NULL THEN 1 ELSE 0 END) AS Missing_CustomerID,
    SUM(CASE WHEN Sales IS NULL THEN 1 ELSE 0 END) AS Missing_Sales,
    SUM(CASE WHEN Profit IS NULL THEN 1 ELSE 0 END) AS Missing_Profit,
    SUM(CASE WHEN Order_Date IS NULL THEN 1 ELSE 0 END) AS Missing_OrderDate,
    SUM(CASE WHEN Ship_Mode IS NULL THEN 1 ELSE 0 END) AS Missing_Shipmode,
    SUM(CASE WHEN Customer_Name IS NULL THEN 1 ELSE 0 END) AS Missing_CustName,
    SUM(CASE WHEN Segment IS NULL THEN 1 ELSE 0 END) AS Missing_Segment,
    SUM(CASE WHEN Country IS NULL THEN 1 ELSE 0 END) AS Missing_Country,
    SUM(CASE WHEN City IS NULL THEN 1 ELSE 0 END) AS Missing_City,
    SUM(CASE WHEN Postal_Code IS NULL THEN 1 ELSE 0 END) AS Missing_Postcode,
    SUM(CASE WHEN Region IS NULL THEN 1 ELSE 0 END) AS Missing_Region,
    SUM(CASE WHEN Product_ID IS NULL THEN 1 ELSE 0 END) AS Missing_Product_ID,
    SUM(CASE WHEN Category IS NULL THEN 1 ELSE 0 END) AS Missing_Category,
    SUM(CASE WHEN Sub_category IS NULL THEN 1 ELSE 0 END) AS Missing_Sub_Category,
    SUM(CASE WHEN Product_Name IS NULL THEN 1 ELSE 0 END) AS Missing_ProductName,
    SUM(CASE WHEN Quantity IS NULL THEN 1 ELSE 0 END) AS Missing_Qty
FROM Superstore_sales;
```

The results provided a clear overview of columns containing missing values, enabling informed decisions on appropriate data cleaning strategies such as removal, imputation, or retention of NULL entries based on their relevance to the analysis. This step ensured improved data quality and reliability before proceeding to further analysis and modeling. A comprehensive missing values assessment was conducted across all columns in the dataset using a single SQL aggregation query with conditional counting. This approach enabled efficient identification of NULL values across the entire dataset.


**Handling Missing Profit Values**

During this process, it was observed that the Profit column contained missing values. Since profit is a numerical field required for consistent financial analysis, all NULL entries in this column were replaced with zero (0). This decision was made to maintain a uniform numeric format and to ensure that records without recorded profit did not disrupt calculations, aggregations, or visualizations.

```SQL
--Replacing the nulls in the profit column
UPDATE Superstore_sales
SET profit = 0
WHERE profit IS NULL;
```

After handling the missing values, the dataset was confirmed to be free of NULL values in critical fields, ensuring improved data quality and consistency for subsequent analysis and reporting.


**Identifying and Removing Duplicate Records**
  
Duplicate records were identified using a combination of Order ID, Product ID, and Customer ID. While these records shared identical values across most columns, they differed in the Profit field. These duplicates could inflate sales and profit figures if not addressed.
```SQL
--Checking duplicate values 
SELECT Order_ID, Product_ID, Customer_ID, COUNT(*) AS duplicate_count
FROM Superstore_sales
GROUP BY Order_ID, Product_ID, Customer_ID
HAVING COUNT(*) > 1;
```

To prevent inflated sales and profit figures, duplicates were resolved by retaining only the record with the highest profit and removing the others. This approach ensures that the most financially representative value is preserved and prevents distortion in profitability analysis.

A CTE(Common Table Expression) with a ROWNUMBER() function was used to rank duplicates by profit in descending order, after which lower-ranked records were deleted. This step improved data accuracy and ensured reliable analytical results

```SQL
-- Keep the row with the highest Profit and delete duplicates
WITH CTE AS (
 SELECT *,
      ROW_NUMBER() OVER (
PARTITION BY Order_ID, Product_ID, Customer_ID
ORDER BY Profit DESC) AS rn
FROM Superstore_sales)
DELETE FROM CTE
WHERE rn > 1;
```


**Checking for Invalid Numerical Values**
  
Negative values in numerical columns such as Sales and Quantity were examined, as these could indicate data entry errors or returns.

```SQL
--Checking for negative values in the numerical columns
SELECT *
FROM Superstore_sales
WHERE Quantity <0 OR Sales < 0
```

**Date Consistency Check**
  
To ensure logical consistency, records where the ship date occurred before the order date were identified and none was found .This cleaning process ensured the dataset was reliable and suitable for meaningful analysis

```SQL
SELECT COUNT(*) AS InvalidDateCount
FROM Superstore_sales
WHERE [Ship_Date] < [Order_Date];
```

***Addition Of New Columns***

To enhance time-based analysis and support trend identification, additional date-related columns were created from the Order Date field. These include:

-	Year: Extracted to enable yearly performance comparison and long-term trend analysis.
  
-	Month Name: Added to support monthly sales, profit, and order volume analysis.
  
-	Month Number: Created to allow correct chronological sorting of months in visualizations and dashboards.
  
  
### Data Analysis and Insights

***1. Overall Business Performance***

- Total Revenue: 2.3M

- Total Profit: 286.45K

- Total Transactions: 9,986

- Total Quantity Sold: 37,844

- Average Discount: 15.63%

![KPIS](https://github.com/user-attachments/assets/10f8fa7c-833f-4c37-b57b-2812da62c901)


**Insight:**

The business demonstrates strong revenue performance with healthy overall profitability. However, the relatively high average discount indicates that a significant portion of sales growth is driven by price reductions, which may place pressure on long-term profit margins if not carefully managed.

***2. Monthly Sales Trend and Seasonality***

Sales performance varies across the year rather than following a consistent upward trend. Revenue peaks are most pronounced in November and December.

![Total Revenue By Month](https://github.com/user-attachments/assets/1f8dd651-93a7-4462-990e-0728e3c2926a)


**Insight:**

This pattern highlights clear seasonality, likely influenced by holiday shopping, promotional campaigns, and end-of-year purchasing behaviour. Strategic planning around these peak months can further maximize revenue.

***3. Sales by Customer Segment***

The Consumer segment generates the highest revenue.

The Corporate segment follows closely.

The Home Office segment contributes the least to total sales.

![Sales By Segment](https://github.com/user-attachments/assets/4ba0352e-6be7-44dd-919f-5207c94ab333)


**Insight:**

Revenue is heavily concentrated within the consumer segment. This presents an opportunity to diversify income streams by developing targeted strategies to grow corporate and home office customer engagement.

***4. Shipping Mode Analysis***

Standard Class shipping is used most frequently.

First Class and Same Day shipping options show minimal adoption.

![Sales By Ship Mode](https://github.com/user-attachments/assets/d8e7bf61-5d8d-40cd-bcfd-97f9e90278db)


**Insight:**

Customers prioritize affordability over delivery speed, indicating strong price sensitivity. Faster shipping options may require repositioning or incentives to increase adoption.

***5. Top-Selling Product Sub-Categories***

Phones and Chairs are the highest revenue-generating sub-categories.

Tables and Binders show comparatively weaker performance.

<img width="245" height="244" alt="Top 5 Selling Products By Sub Category" src="https://github.com/user-attachments/assets/6da68852-5cf8-4ae7-8913-5fa85d4d933e" />


**Insight:**

Sales are concentrated in a limited number of high-performing sub-categories, while some products contribute less value and may increase inventory holding costs without proportional returns.

***6. Discount vs Profit Relationship***

Analysis shows that higher discount levels do not consistently translate into higher profits. In many cases, increased discounts are associated with reduced profit margins.

![Discount Vs Profit](https://github.com/user-attachments/assets/845b6518-bb23-473f-b0e5-e6998d4fbe89)


**Insight:**

Current discounting strategies are not always effective and may be eroding profitability. A more targeted and data-driven discount approach could improve margin performance.



### Recommendations

**1. Improve Discount Strategy**

The current discount level appears to reduce profit margins in some cases. Discounts should be applied selectively, focusing on low-performing products, off-peak periods, or specific customer segments rather than across all products.

**2. Plan Around Seasonal Demand**

Sales peak significantly toward the end of the year, especially in November and December. Inventory planning, staffing, and marketing campaigns should be aligned with these periods to maximize revenue while controlling costs.

**3. Grow Corporate and Home Office Sales**

The business relies heavily on consumer customers. Targeted offers, bulk purchase deals, and customized pricing for corporate and home office customers could help increase revenue from these underutilized segments.

**4. Optimize Shipping Options**

Most customers prefer Standard Class shipping, indicating strong price sensitivity. Premium shipping options such as First Class and Same Day can be promoted through limited-time offers or bundled incentives to increase adoption.

**5. Focus on High-Performing Products**

Sub-categories such as Phones and Chairs generate the most revenue and should be prioritized in inventory and marketing efforts. Low-performing products like Tables and Binders should be reviewed to determine whether repricing, promotion, or removal is necessary.

**6. Monitor Profitability More Closely**

Regular analysis of profit trends at the product and discount level is recommended. This will help ensure that sales growth is not achieved at the expense of profitability.

**7. Leverage Dashboards for Ongoing Decisions**

Power BI dashboards should be used continuously to monitor key metrics such as revenue, profit, discounts, and shipping performance. This supports faster, data-driven decision-making and long-term business planning



### Conclusion

This analysis demonstrates how structured data cleaning and exploratory analysis can uncover valuable insights from transactional data. By addressing data quality issues and analyzing customer, shipping, and temporal trends, the organization can make informed decisions that enhance efficiency, improve customer experience, and support long-term growth.By implementing these strategies, the business can drive sustainable growth, improve profitability, and make more informed decisions. Prioritizing high-performing products, optimizing discounts, and leveraging data insights will ensure both short-term gains and long-term resilience.
