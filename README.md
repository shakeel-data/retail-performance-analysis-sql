# 🛒 End-to-End Retail Analytics Project | SQL 
Retail sales is essential for businesses aiming to make informed, data-driven decisions. It provides valuable insights into customer purchasing behavior, product performance, and sales trends. By analyzing transactional data, companies can identify peak sales periods, top-performing categories, and shifting customer preferences. These insights enable businesses to optimize pricing strategies, manage inventory efficiently, and tailor marketing efforts—leading to improved customer satisfaction, increased revenue, and a stronger competitive edge in the market.

## Project Overview
SQL skills commonly applied by data analysts to clean, explore, and analyze retail sales data. It involves creating a structured retail database, conducting exploratory data analysis (EDA), and key for business growth barriers and solutions through well-crafted SQL queries. This project Designed for data analysis and serves as a practical mastering of SQL in real-world business contexts.

## Strategic Objectives
- **Retail Sales Database Setup** - Design and implement a structured relational database to store retail transaction data efficiently.

- **Data Cleaning** - Identify and eliminate records with null or inconsistent values to ensure data quality and reliability.

- **Exploratory Data Analysis (EDA)** - Perform initial data exploration using SQL to understand patterns, trends, and data distribution.

- **Business Insight Generation** - Develop and execute targeted SQL queries to address key business questions, uncover growth opportunities, and support strategic decision-making.

## Project Breakdown

### 1. Database Configuration
- **Database Deployment** : The project initiates by provisioning a structured database named `Project1`, designed to serve as the centralized repository for all retail transaction data.
- **Schema Definition & Table Structuring** : A comprehensive table, retail_sales, is architected to encapsulate critical sales attributes such as transaction identifiers, timestamps, customer profiles (ID, gender, age), product classifications, quantities sold, pricing metrics, cost of goods sold (COGS), and overall sales figures.

```sql
CREATE DATABASE project1

CREATE TABLE  Retail_sales
(
   transactions_id INT PRIMARY KEY,
   sale_date DATE,
   sale_time TIME,
   customer_id INT,
   gender VARCHAR(10),
   age INT,
   category VARCHAR(25),
   quantity INT,
   price_per_unit FLOAT,
   cogs FLOAT,
   total_sale FLOAT

 );
```

### 2. Data Profiling & Preparation
- **Total Records Evaluation**: Calculate the total number of entries in the dataset.

```sql
SELECT
     COUNT(*)
FROM retail_sales;

```

- **Distinct Customer Identification**: Determine the count of unique customers represented in the sales data.

```sql
SELECT
     COUNT(DISTINCT customer_id)
FROM retail_sales;

```

- **Product Category Enumeration**: Extract and list all distinct product categories found in the dataset.

```sql
SELECT
     DISTINCT category
FROM retail_sales;  

```

- **Missing Data Handling**: Inspect the dataset for any null or incomplete values and remove any records that may compromise data integrity.

```sql

SELECT * FROM retail_sales
WHERE
    transactions_id is null
    or
    sale_date is null
    or
    sale_time is null
    or
    customer_id is null
    or 
    gender is null
    or
    age is null
    or
    category is null
    or 
    quantity is null 
    or
    price_per_unit is null
    or
    cogs is null
    or 
    total_sale is null;


DELETE FROM retail_sales
WHERE
    transactions_id is null
    or
    sale_date is null
    or
    sale_time is null
    or
    customer_id is null
    or 
    gender is null
    or
    age is null
    or
    category is null
    or 
    quantity is null 
    or
    price_per_unit is null
    or
    cogs is null
    or 
    total_sale is null;

```

### 3. Data Exploration & Key Outcomes

To extract actionable insights, the following SQL statements were executed in response to targeted business questions.

**Q.1** **What is the Total revenue generated?**
```sql
SELECT 
     SUM(total_sale) AS Total_revenue 
FROM Retail_sales;
```

**Q.2** **What’s the Average sale amount per transaction?**
```sql
SELECT 
     AVG(total_sale) AS Average_transaction
FROM Retail_sales;
```

**Q.3** **How many sales were made by male vs female customers?**
```sql
SELECT gender, 
            COUNT(*) AS sales_count
FROM Retail_sales
GROUP BY gender;
```

**Q.4** **Find all transactions where the total_sale is greater than "1000"?**
```sql
SELECT * 
FROM retail_sales
WHERE total_sale > 1000
```

**Q.5** **Which sales transactions occurred on '2022-11-05?**
```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```

**Q.6** **What is the Percentage of male vs female customers?**
```sql
SELECT gender, 
       COUNT(*) * 100.0 / (SELECT COUNT(*) FROM Retail_sales) AS percentage
FROM Retail_sales
GROUP BY gender;
```

**Q.7** **Find out the top 5 customers based on the highest total sales?**
```sql
SELECT 
    customer_id,
    SUM(total_sale) as total_spent
FROM retail_sales
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5
```

**Q.8** **How does the total sales for each category?**
```sql
SELECT 
     category,
     SUM(total_sale) as Net_sale,
     COUNT(*) as total_orders
FROM retail_sales
GROUP BY 1
```

**Q.9** **What is the revenue generated by each age group (e.g., 10-year intervals)?**
```sql
SELECT 
     FLOOR(age / 10) * 10 AS age_group, 
	 SUM(total_sale) AS Revenue
FROM Retail_sales
GROUP BY age_group
ORDER BY age_group;
```

**Q.10** **Find the average age of customers who purchased items from the 'Electronics' category?**
```sql
SELECT
     ROUND(AVG (age),2) AS AVERAGE_AGE
FROM retail_sales
WHERE category = 'Electronics'
```

**Q.11** **Find out the total number of transactions made by each gender in each category?**
```sql
SELECT 
    category,
    gender,
    COUNT(*) as total_transactions
FROM retail_sales
GROUP BY 
    category,
    gender
ORDER BY 1
```

**Q.12** **Which Category has highest quantity sold?**
```sql
SELECT 
     category, 
     SUM(quantity) AS total_quantity
FROM Retail_sales
GROUP BY category
ORDER BY total_quantity DESC
LIMIT 1;
```

**Q.13** **Which day has the highest revenue occured?**
```sql
SELECT 
     EXTRACT(HOUR FROM sale_time) AS hour, 
	 SUM(total_sale) AS total_sales
FROM Retail_sales
GROUP BY hour
ORDER BY hour;
```

**Q.14** **What’s the month-wise revenue distribution?**
```sql
SELECT 
     TO_CHAR(sale_date, 'YYYY-MM') AS month, 
	 SUM(total_sale) AS monthly_revenue
FROM Retail_sales
GROUP BY month
ORDER BY month;
```

**Q.15** **Find out each shift and number of orders (Eg. Morning <12, Afternoon Between 12 & 17, Evening >17)?**
```sql
SELECT 
     CASE 
     WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
     WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
     ELSE 'Evening'
     END AS shift,
     COUNT(*) AS order_count
FROM Retail_sales
GROUP BY 1;
```


## Analysis Highlights
- **Premium Transactions** - A notable portion of transactions exceeded the 1000-unit mark in total sales, highlighting instances of high-value or premium purchases.
- **Consumer Intelligence** - The analysis identifies high-spending customers and pinpoints the most frequently purchased product categories, offering valuable inputs for customer segmentation and targeted marketing strategies.
- **Customer Profile Overview** - The dataset captures a broad spectrum of age groups, reflecting a diverse customer base. Sales activity is distributed across multiple product segments, notably in categories like Clothing and Beauty.
- **Revenue Patterns** - Month-over-month analysis reveals fluctuations in revenue, providing visibility into seasonal demand cycles and peak performance periods.

## Analytical Summaries
- **Sales Insights** : A comprehensive analysis highlighting overall revenue, customer segmentation, and category-wise sales performance.
- **Consumer Analytics** - This section provides insights into top-spending customers and evaluates the count of distinct customers across each product category, offering a clearer view of customer value and segmentation trends.
- **Time-Series Analysis**- This analysis highlights monthly revenue patterns and sales distribution across different shifts (morning, afternoon, evening). It offers valuable insights into peak performance periods and customer buying behavior, supporting more informed and strategic business decisions.

## Conclusion
- This project provides a comprehensive and practical introduction to SQL, designed specifically for aspiring data analysts. It covers the entire process, including database creation, structured data loading, careful data cleaning, and thorough exploratory data analysis (EDA).
- The results of this project can be vital in identifying revenue opportunities, improving customer targeting strategies, optimizing inventory management, and supporting overall business growth. It serves not only as a technical exercise but also as a real-world application of SQL to address business challenges.







