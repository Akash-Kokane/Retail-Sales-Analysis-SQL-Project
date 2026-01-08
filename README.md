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
- Checked for NULL values across all columns.
- Removed incomplete records to ensure data integrity.

#### 3. Exploratory Data Analysis (EDA)
- Total records count
- Unique customers
- Product categories
- Data completeness validation

#### 4. Business Analysis Queries
10 key SQL queries answered:
1. Sales on a specific date (`2022-11-05`)
2. High-quantity Clothing sales in November 2022
3. Total sales per category
4. Average age of Beauty category customers
5. High-value transactions (> 1000)
6. Transaction count by gender and category
7. Best-selling month per year
8. Top 5 customers by total sales
9. Unique customers per category
10. Order distribution across day shifts (Morning/Afternoon/Evening)

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
