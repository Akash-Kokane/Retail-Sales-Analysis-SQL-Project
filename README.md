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
SELECT COUNT(*) AS total_sales_data
FROM retail_sales;
```
- Unique customers
```sql
SELECT COUNT(DISTINCT customer_id) AS total_customers
FROM retail_sales;
```
- Product categories
```sql
SELECT DISTINCT category AS number_of_categories
FROM retail_sales;
```
- Data completeness validation
```sql
SELECT * FROM retail_sales;
```

#### 4. Business Analysis Queries
10 key SQL queries answered:
1. Sales on a specific date (`2022-11-05`)
```sql
SELECT * 
FROM retail_sales
WHERE sale_date = '2022-11-05';
```
3. High-quantity Clothing sales in November 2022
```sql
SELECT *
FROM retail_sales
WHERE category = 'Clothing'
    AND quantity > 3
    AND sale_date BETWEEN '2022-11-01' AND '2022-11-30';
```
5. Total sales per category
```sql
SELECT 
    category, 
    SUM(total_sale) AS total_sales_amount,
    ROUND(SUM(total_sale), 2) AS total_sales_rounded
FROM retail_sales
GROUP BY category
ORDER BY total_sales_amount DESC;
```
7. Average age of Beauty category customers
```sql
SELECT 
    ROUND(AVG(age), 2) AS avg_age_beauty_customers
FROM retail_sales
WHERE category = 'Beauty';
```

9. High-value transactions (> 1000)
```sql
SELECT *
FROM retail_sales
WHERE total_sale > 1000
ORDER BY total_sale DESC;
```

11. Transaction count by gender and category
```sql
SELECT 
    gender,
    category,
    COUNT(*) AS total_transactions
FROM retail_sales
GROUP BY gender, category
ORDER BY category, gender;
```
13. Best-selling month per year
```sql
SELECT 
    year,
    month,
    avg_sale
FROM (
    SELECT
        EXTRACT(YEAR FROM sale_date) AS year,
        EXTRACT(MONTH FROM sale_date) AS month,
        ROUND(AVG(total_sale), 2) AS avg_sale,
        RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) 
                   ORDER BY AVG(total_sale) DESC) AS rank
    FROM retail_sales
    GROUP BY EXTRACT(YEAR FROM sale_date), EXTRACT(MONTH FROM sale_date)
) AS ranked_months
WHERE rank = 1
ORDER BY year;
```
15. Top 5 customers by total sales
```sql
SELECT 
    customer_id,
    ROUND(SUM(total_sale), 2) AS total_sales_amount,
    COUNT(*) AS total_transactions
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales_amount DESC
LIMIT 5;
```
17. Unique customers per category
```sql
SELECT 
    category,
    COUNT(DISTINCT customer_id) AS count_of_unique_customers,
    ROUND(COUNT(DISTINCT customer_id) * 100.0 / 
          (SELECT COUNT(DISTINCT customer_id) FROM retail_sales), 2) AS percentage_of_total_customers
FROM retail_sales
GROUP BY category
ORDER BY count_of_unique_customers DESC;
```
19. Order distribution across day shifts (Morning/Afternoon/Evening)
```sql
WITH hourly_sale AS (
    SELECT 
        *,
        CASE 
            WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
            WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
            ELSE 'Evening'
        END AS shift
    FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) AS total_orders,
    ROUND(COUNT(*) * 100.0 / (SELECT COUNT(*) FROM retail_sales), 2) AS percentage_of_total_orders
FROM hourly_sale
GROUP BY shift
ORDER BY total_orders DESC;
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
