# Retail Sales Analysis SQL Project

## Project Overview

**Project Title**: Retail Sales Analysis  
**Level**: Beginner  
**Database**: `p1_retail_db`

This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. This project is ideal for those who are starting their journey in data analysis and want to build a solid foundation in SQL.

## Objectives

1. **Set up a retail sales database**: Create and populate a retail sales database with the provided sales data.
2. **Data Cleaning**: Identify and remove any records with missing or null values.
3. **Exploratory Data Analysis (EDA)**: Perform basic exploratory data analysis to understand the dataset.
4. **Business Analysis**: Use SQL to answer specific business questions and derive insights from the sales data.

## Project Structure

### 1. Database Setup

- **Database Creation**: The project starts by creating a database named `p1_retail_db`.
- **Table Creation**: A table named `retail_sales` is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

--- SQL RETAIL SALES ANALYSIS 
CREATE DATABASE RETAIL_PROJECT;

USE RETAIL_PROJECT;

CREATE TABLE RETAIL_SALES(
	transactions_id INT,
	sale_date DATE,
	sale_time TIME,
	customer_id	INT,
    gender VARCHAR(10),
	age INT,
	category VARCHAR (20),
	quantiy INT,
	price_per_unit INT,
	cogs INT,
	total_sale INT);

SELECT * FROM RETAIL_SALES;


-- DATA CLEANING 
select * from RETAIL_SALES 
WHERE transactions_id is null;

select * from RETAIL_SALES 
WHERE sale_date is null;

SELECT * FROM RETAIL_SALES 
WHERE sale_time IS NULL
OR CUSTOMER_ID OR GENDER OR AGE OR CATEGORY OR QUANTIY OR PRICE_PER_UNIT OR COGS OR TOTAL_SALE IS NULL;

-- DATA EXPLORATION 

-- HOW MANY SALES WE HAVE?
SELECT COUNT(*) total_sale FROM RETAIL_SALES;

-- HOW MANY UNIQUE CUSTOMERS WE HAVE?
SELECT  COUNT(distinct customer_id)   FROM RETAIL_SALES;

-- HOW MANY UNIQUE CATEGORY WE HAVE?
SELECT COUNT(distinct Category) FROM RETAIL_SALES;

-- DATA ANALYSIS & BUSINESS KEY PROBLEMS & ANSWERS 

-- WRITE A SQL QUERY TO RETRIVE ALL COLUMNS FOR SALE MADE ON "2022-11-05"
SELECT * FROM RETAIL_SALES WHERE SALE_DATE=("2022-11-05");

-- WRITE A SQL QUERY TO RETRIVE ALL TRANSACTION WHERE THE CATEGORY IS "CLOTHING" AND THE QTY SOLD IS MORE THAN 10 IN THE MONTH OF NOV-2022?
SELECT * FROM RETAIL_SALES WHERE CATEGORY= "CLOTHING" AND SALE_DATE LIKE "2022-11%" AND QUANTIY>3;

-- WRITE A QUERY TO CALCULATE THE TOTAL SALES FOR EACH CATEGORY?
SELECT CATEGORY, SUM(TOTAL_SALE) FROM RETAIL_SALES GROUP BY CATEGORY;


--  WRITE A QUERY TO FIND THE AVERAGE AGE OF CUSTOMERS WHO PURCHASED ITEMS FROM THE "BEAUTY" CATEGORY?
SELECT AVG(AGE) FROM RETAIL_SALES WHERE CATEGORY= "BEAUTY";

-- WRITE A QUERY TO FIND ALL TRANSACTION WHERE THE TOTAL_SALE IS GREATER THAN 1000
SELECT * FROM RETAIL_SALES WHERE TOTAL_SALE> 1000;

-- WRITE A SQL QUERY TO FIND THE TOTAL NUMBER OF TRANSACTIONS (TRANSACTION_ID) MADE BY EACH GENDER CATEGORY?
SELECT GENDER,CATEGORY, COUNT(*) AS TRANSACTIONS_ID FROM RETAIL_SALES GROUP BY CATEGORY,GENDER;

-- WRITE A QUERY TO CALCULATE THE AVERAGE SALE FOR EACH MONTH. FIND OUT BEST SELLING MONTH IN EACH YEAR?
 SELECT  YEAR(SALE_DATE) AS year,
 MONTH (SALE_DATE)AS MONTH, AVG (TOTAL_SALE), MAX(SALE_DATE)
 FROM RETAIL_SALES GROUP BY (SALE_DATE)
 ORDER BY AVG(TOTAL_SALE) DESC;
 
 -- WRITE A SQL QUERY TO FIND TOP 5 CUSTOMER BASED ON HIGHEST TOTAL SALES ?
 SELECT customer_id, sum(TOTAL_SALE)	FROM retail_SALES group by customer_id order by sum(total_sale) desc limit 5;
 
 -- WRITE A SQL QUERY TO FIND THE NUMBER OF UNIQUE CUTOMER WHO PURCHASED ITEMS FROM EACH CATEGORY?
 SELECT COUNT(DISTINCT	CUSTOMER_ID),CATEGORY FROM RETAIL_SALES GROUP BY CATEGORY;
 
 -- WRITE A QUERY T CREATE EACH SHIFT AND NUMBER OF ORDERS ( EXAMPLE MORNING<=12,AFTERNOON BETWEEN 12 & 17, EVENING>17)?
WITH  HOURLY_SALE
AS(
SELECT *,
HOUR(SALE_TIME) AS HOUR,
CASE  WHEN HOUR(SALE_TIME)<12 THEN "MORNING"
WHEN HOUR(SALE_TIME) BETWEEN 12 AND 17	THEN "AFTERNOON"
ELSE "EVENING" END AS SHIFT
FROM RETAIL_SALES)
SELECT	SHIFT,COUNT(TRANSACTIONS_ID)
FROM HOURLY_SALE 
GROUP BY SHIFT;



---	END OF PROJECT 1 RETAIL SALE ANALAYSIS ---

- **Customer Demographics**: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
- **High-Value Transactions**: Several transactions had a total sale amount greater than 1000, indicating premium purchases.
- **Sales Trends**: Monthly analysis shows variations in sales, helping identify peak seasons.
- **Customer Insights**: The analysis identifies the top-spending customers and the most popular product categories.

## Reports

- **Sales Summary**: A detailed report summarizing total sales, customer demographics, and category performance.
- **Trend Analysis**: Insights into sales trends across different months and shifts.
- **Customer Insights**: Reports on top customers and unique customer counts per category.

## Conclusion

This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.

## How to Use

1. **Clone the Repository**: Clone this project repository from GitHub.
2. **Set Up the Database**: Run the SQL scripts provided in the `database_setup.sql` file to create and populate the database.
3. **Run the Queries**: Use the SQL queries provided in the `analysis_queries.sql` file to perform your analysis.
4. **Explore and Modify**: Feel free to modify the queries to explore different aspects of the dataset or answer additional business questions.



Thank you for your support, and I look forward to connecting with you!
