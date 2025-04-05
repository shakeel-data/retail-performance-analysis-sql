# 🛒 Retail Analytics Project | SQL 

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
































