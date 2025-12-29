# SUPERSTORE-SALES-ANALYSIS-USING-SQL-FOR-ANALYSIS-AND-POWER-BI-FOR-VISUALIZATION
An excel file showing transactional records from a retail superstore, capturing customer, order, shipment and location details and more. The goal of this analysis is to explore sales and profit patterns, understand customer and shipping behavior, and generate actionable insights that support data-driven business and operational decisions.

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
1. Executive Management
-	Strategic planning using revenue and profit insights
  
-	Identification of growth opportunities
  
2. Sales and Marketing Teams
-	Customer segment targeting
  
-	Discount and promotional optimization
  
3. Operations and Logistics Teams
-	Shipping mode optimization
  
-	Cost efficiency improvements
  
4. Finance Teams
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

Data Cleaning and Preprocessing
Before analysis, a thorough data cleaning process was carried out using SQL to ensure accuracy, consistency, and reliability of insights.
Steps taken include:
Checking For Missing Values
A comprehensive missing values check was conducted across all columns in the dataset using a single SQL aggregation query. The query calculated the total number of records and the number of NULL values present in each column by applying conditional counting with CASE WHEN statements. This approach allowed for an efficient and structured evaluation of data completeness without inspecting columns individually.
The results provided a clear overview of columns containing missing values, enabling informed decisions on appropriate data cleaning strategies such as removal, imputation, or retention of NULL entries based on their relevance to the analysis. This step ensured improved data quality and reliability before proceeding to further analysis and modeling. A comprehensive missing values assessment was conducted across all columns in the dataset using a single SQL aggregation query with conditional counting. This approach enabled efficient identification of NULL values across the entire dataset.


Handling Missing Profit Values
During this process, it was observed that the Profit column contained missing values. Since profit is a numerical field required for consistent financial analysis, all NULL entries in this column were replaced with zero (0). This decision was made to maintain a uniform numeric format and to ensure that records without recorded profit did not disrupt calculations, aggregations, or visualizations.
After handling the missing values, the dataset was confirmed to be free of NULL values in critical fields, ensuring improved data quality and consistency for subsequent analysis and reporting.
3.3 Identifying and Removing Duplicate Records
Duplicate records were identified using a combination of Order ID, Product ID, and Customer ID. While these records shared identical values across most columns, they differed in the Profit field. These duplicates could inflate sales and profit figures if not addressed.
To prevent inflated sales and profit figures, duplicates were resolved by retaining only the record with the highest profit and removing the others. This approach ensures that the most financially representative value is preserved and prevents distortion in profitability analysis.
A CTE(Common Table Expression) with a ROWNUMBER() function was used to rank duplicates by profit in descending order, after which lower-ranked records were deleted. This step improved data accuracy and ensured reliable analytical results

Checking for Invalid Numerical Values
Negative values in numerical columns such as Sales and Quantity were examined, as these could indicate data entry errors or returns.

Date Consistency Check
To ensure logical consistency, records where the ship date occurred before the order date were identified and none was found .This cleaning process ensured the dataset was reliable and suitable for meaningful analysis
ADDITION OF NEW COLUMNS
To enhance time-based analysis and support trend identification, additional date-related columns were created from the Order Date field. These include:
•	Year: Extracted to enable yearly performance comparison and long-term trend analysis.
•	Month: Added to support monthly sales, profit, and order volume analysis.
•	Month Number: Created to allow correct chronological sorting of months in visualizations and dashboards.
Data Analysis and Insights
1. Overall Business Performance
•	Total Revenue: 2.3M
•	Total Profit: 286.45K
•	Total Transactions: 9,986
•	Total Quantity Sold: 37,844
•	Average Discount: 16%
Insight :
The business demonstrates strong revenue generation with healthy profitability. However, the relatively high average discount suggests that sales growth may be partially driven by price reductions, which could impact long-term margins.
2. Monthly Revenue Trend and Seasonality	
•	Revenue fluctuates across months rather than showing steady growth.
•	November and December record noticeable spikes in revenue.
•	Certain mid-year months experience lower sales performance.
Insight:
Sales exhibit clear seasonality, with higher revenue toward the end of the year. This trend likely reflects holiday shopping behavior and increased consumer spending during festive periods.

3. Sales by Customer Segment
•	The Consumer segment contributes the largest portion of total revenue.
•	Corporate follows, while Home Office contributes the least.
Insight :
The business relies heavily on consumer customers, creating a potential risk if demand declines. There is an opportunity to expand revenue by targeting corporate and home office customers more effectively.

4 Sales by Shipping Mode
•	Standard Class shipping accounts for the majority of sales.
•	Same Day and First Class shipping options are minimally used.
Insight :
Customers appear to be price-sensitive, prioritizing lower shipping costs over faster delivery times.

5. Top-Selling Product Sub-Categories
•	Phones and Chairs generate the highest revenue.
•	Tables and Binders underperform relative to other sub-categories.
Insight :
A small number of products drive a significant portion of total revenue, while some categories contribute less and may increase inventory holding costs.

6. Discount vs Profit Analysis
•	Higher discounts do not consistently lead to higher profits.
•	In several instances, increased discounting corresponds with reduced profitability.
Insight :
Excessive discounting is eroding profit margins without guaranteeing proportional sales growth, indicating the need for a more strategic discount approach.

Data Visualization
Power BI dashboards were developed to visualize:
•	Monthly revenue trends
•	Segment-wise sales distribution
•	Shipping mode usage
•	Product sub-category performance
•	Discount vs profit comparison
These visuals enable stakeholders to quickly interpret trends and monitor performance.

Recommendations
 1. Improve Weekend Sales (Based on Daily Revenue Insight)
•	Introduce weekend-only promotions or flash sales.
•	Offer bundle deals or free shipping on Saturdays and Sundays.
•	Run targeted weekend ads to increase engagement.

 2. Optimize Discount Strategy
•	Reduce discounts on high-demand products (e.g., Phones, Chairs).
•	Apply discounts strategically to low-performing categories only.
•	Monitor profit margins closely when running promotions.
3. Leverage Seasonal Demand
•	Increase inventory and marketing spend before Q4 (Nov–Dec).
•	Launch pre-season campaigns to maximize peak-period revenue
 4. Leverage High-Performing Days
•	Schedule major campaigns and product launches mid-week.
•	Push email and social media marketing on Tuesdays–Thursdays.

 5. Strengthen Underperforming Categories
•	Re-evaluate pricing or product quality for Tables and Accessories.
•	Consider bundling them with high-performing products.
•	Reduce inventory holding costs for slow-moving items.

 5. Diversify Customer Segments
•	Create tailored offers for Corporate and Home Office customers.
•	Offer bulk purchase discounts for business clients.
 5. Encourage Premium Shipping Options
•	Offer limited-time incentives for Same Day or First Class shipping.
•	Promote faster shipping during peak seasons.

 6. Plan for Seasonal Demand
•	Prepare inventory ahead of high-performing months.
•	Launch pre-season campaigns to maximize peak-period revenue.




Conclusion
This analysis demonstrates how structured data cleaning and exploratory analysis can uncover valuable insights from transactional data. By addressing data quality issues and analyzing customer, shipping, and temporal trends, the organization can make informed decisions that enhance efficiency, improve customer experience, and support long-term growth.
