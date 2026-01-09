## Retail-Sales-Analysis-SQL-Project

### Project Overview
---
This project demonstrates SQL skills for analyzing retail sales data, covering **database creation, data cleaning, exploratory data analysis (EDA), and business insights extraction**. It is designed for beginners in data analytics and SQL, providing hands-on experience with real-world data scenarios.

### Project Files
---
- **`sql_queries.sql`** – Contains all SQL queries used in the project (database creation, cleaning, analysis, and reporting).
- **`retail_sales_project.pdf`** – Full project documentation including objectives, structure, queries, and findings.


### Tools & Technologies
---
- **SQL** (PostgreSQL/MySQL compatible)
- **Database**: `retail_sales_project`
- **Table**: `retail_sales`
- **Concepts Covered**: CRUD, NULL handling, aggregation, window functions, CTEs, date/time functions.

### Project Structure
---

#### 1. Database & Table Setup
```sql
CREATE DATABASE retail_sales_project;
CREATE TABLE retail_sales (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(15),
    age INT,
    category VARCHAR(15),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
```

#### 2. Data Cleaning
-- Check initial data
```sql
SELECT * FROM retail_sales;
```
- Checked for NULL values across all columns.
```sql
SELECT * FROM retail_sales WHERE transactions_id IS NULL;
SELECT * FROM retail_sales WHERE sale_date IS NULL;
SELECT * FROM retail_sales WHERE sale_time IS NULL;
SELECT * FROM retail_sales WHERE customer_id IS NULL;
SELECT * FROM retail_sales WHERE gender IS NULL;
SELECT * FROM retail_sales WHERE age IS NULL;
```
- Removed incomplete records to ensure data integrity.
```sql
SELECT * FROM retail_sales
WHERE transactions_id IS NULL
    OR sale_date IS NULL
    OR sale_time IS NULL
    OR customer_id IS NULL
    OR gender IS NULL
    OR age IS NULL
    OR category IS NULL
    OR quantity IS NULL 
    OR price_per_unit IS NULL
    OR cogs IS NULL
    OR total_sale IS NULL;

DELETE FROM retail_sales
WHERE transactions_id IS NULL
    OR sale_date IS NULL
    OR sale_time IS NULL
    OR customer_id IS NULL
    OR gender IS NULL
    OR age IS NULL
    OR category IS NULL
    OR quantity IS NULL 
    OR price_per_unit IS NULL
    OR cogs IS NULL
    OR total_sale IS NULL;
```

#### 3. Exploratory Data Analysis (EDA)
- Total records count
```sql
SELECT COUNT(*) AS TotalRecords
FROM retail_sales;
```
- Unique customers
```sql
SELECT COUNT(DISTINCT customer_id) AS TotalCustomers
FROM retail_sales;
```
- Product categories
```sql
SELECT COUNT(DISTINCT Category) AS TotalCategories
FROM retail_sales;
```
- Data completeness validation
```sql
SELECT * FROM retail_sales;
```

#### 4. Business Analysis Queries
- 10 key SQL queries answered:
1. Sales on a specific date (`2022-11-05`)
```sql
SELECT
    *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```
2. High-quantity Clothing sales in November 2022
```sql
SELECT
    *
FROM retail_sales
WHERE category = 'Clothing'
    AND
        quantity > 3
    AND
        sale_date BETWEEN '2022-11-01' AND '2022-11-30';
```
3. Total sales per category
```sql
SELECT
    category,
    SUM(total_sale) AS TotalSales
FROM retail_sales
GROUP BY category
ORDER BY TotalSales DESC;
```
4. Average age of Beauty category customers
```sql
SELECT
    category,
    ROUND(AVG(age)) AS AverageAge
FROM retail_sales
WHERE category = 'Beauty';
```

5. High-value transactions (> 1000)
```sql
SELECT
    transactions_id,
    total_sale
FROM retail_sales
WHERE total_sale > 1000;
```

6. Transaction count by gender and category
```sql
SELECT
    gender,
    category,
    COUNT(*) AS TotalTransactions
FROM retail_sales
GROUP BY 1,2
ORDER BY 2;
```
7. Best-selling month per year
```sql
SELECT
    Year,
    Month,
    AverageSale
FROM (
        SELECT
            YEAR(sale_date) AS Year,
            MONTH(sale_date) AS Month,
            ROUND(AVG(total_sale),2) AS AverageSale,
            DENSE_RANK() OVER(PARTITION BY YEAR(sale_date) ORDER BY AVG(total_sale) DESC) AS AverageRank
        FROM retail_sales
        GROUP BY 1,2
    )t
WHERE AverageRank = 1;
```
8. Top 5 customers by total sales
```sql
SELECT
    customer_id,
    SUM(total_sale) AS TotalSales
FROM retail_sales
GROUP BY customer_id
ORDER BY TotalSales DESC
LIMIT 5;
```
9. Unique customers per category
```sql
SELECT
    category,
    COUNT(DISTINCT(customer_id)) AS uique_customers
FROM retail_sales
GROUP BY category;
```
10. Order distribution across day shifts (Morning/Afternoon/Evening)
```sql
WITH hourly_sale
AS
(
    SELECT
        *,
        CASE
            WHEN HOUR(sale_time) < 12 THEN "Morning"
            WHEN HOUR(sale_time) BETWEEN 12 AND 17 THEN "Afternoon"
            ELSE "Evening"
        END AS Shift
    FROM retail_sales
)
SELECT
    Shift,
    COUNT(*) AS TotalOrders
FROM hourly_sale
GROUP BY Shift;
```

## Key Findings
---
- **Customer Demographics**: Diverse age groups; categories include Clothing, Beauty, etc.
- **High-Value Sales**: Multiple transactions exceeded $1,000.
- **Sales Trends**: Monthly analysis revealed peak sales periods.
- **Customer Insights**: Top spenders and popular categories identified.
- **Shift Analysis**: Most orders occurred in the **Afternoon** shift.

## Reports Generated
---
1. **Sales Summary** – Overall sales and category performance.
2. **Trend Analysis** – Monthly and yearly sales trends.
3. **Customer Insights** – Top customers and category-wise unique customer counts.
4. **Shift Report** – Order distribution across time shifts.

## Learning Outcomes
---
- Setting up and managing a SQL database
- Cleaning and validating real-world data
- Writing complex queries for business insights
- Using window functions, CTEs, and date functions
- Generating analytical reports from raw data

---
---
