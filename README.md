# Sales Insights Data Analysis Project

## Introduction
This project aims to generate sales insights for AtliQ Hardware, a company supplying computer hardware and peripherals. The project demonstrates the entire data analysis process from problem identification to generating actionable insights through a Power BI dashboard. It is ideal for aspiring data analysts and data scientists looking to gain hands-on experience.

## Problem Statement
**AtliQ Hardware**, a computer hardware supplier, is facing challenges in tracking sales performance across various regions. The Sales Director, Bhavin Patel, is struggling to derive clear insights from verbal reports and scattered Excel files provided by regional managers. These reports are often incomplete or sugarcoated, making it difficult to identify the true state of sales performance. 

Patel needs a consolidated, easy-to-digest Power BI dashboard that visualizes sales trends, revenue breakdowns by region and product, and automates monthly reporting. This will enable him to make data-driven decisions and implement strategies to boost sales.

## Project Workflow
1. **Problem Definition**: Understand AtliQ Hardware's sales challenges.
2. **Data Discovery**: Collect and clean the sales data from multiple Excel files.
3. **Dashboard Creation**: Develop a Power BI dashboard that tracks:
   - Year-over-year sales trends
   - Revenue by product and region
   - Insights into declining sales regions
4. **Stakeholder Feedback**: Simulate feedback from stakeholders and iterate on the dashboard design.

### SQL Queries for Analysis

- **Show all customer records**:
    ```sql
    SELECT * FROM customers;
    ```

- **Show total number of customers**:
    ```sql
    SELECT count(*) FROM customers;
    ```

- **Show transactions for the Chennai market** (market code for Chennai is `Mark001`):
    ```sql
    SELECT * FROM transactions WHERE market_code = 'Mark001';
    ```

- **Show distinct product codes that were sold in Chennai**:
    ```sql
    SELECT DISTINCT product_code FROM transactions WHERE market_code = 'Mark001';
    ```

- **Show transactions where the currency is US dollars**:
    ```sql
    SELECT * FROM transactions WHERE currency = 'USD';
    ```

- **Show transactions from the year 2020 (join with the `date` table)**:
    ```sql
    SELECT transactions.*, date.* 
    FROM transactions 
    INNER JOIN date ON transactions.order_date = date.date 
    WHERE date.year = 2020;
    ```

- **Show total revenue in the year 2020**:
    ```sql
    SELECT SUM(transactions.sales_amount) 
    FROM transactions 
    INNER JOIN date ON transactions.order_date = date.date 
    WHERE date.year = 2020 AND (transactions.currency = 'INR' OR transactions.currency = 'USD');
    ```

- **Show total revenue for January 2020**:
    ```sql
    SELECT SUM(transactions.sales_amount) 
    FROM transactions 
    INNER JOIN date ON transactions.order_date = date.date 
    WHERE date.year = 2020 AND date.month_name = 'January' 
    AND (transactions.currency = 'INR' OR transactions.currency = 'USD');
    ```

- **Show total revenue in Chennai in 2020**:
    ```sql
    SELECT SUM(transactions.sales_amount) 
    FROM transactions 
    INNER JOIN date ON transactions.order_date = date.date 
    WHERE date.year = 2020 AND transactions.market_code = 'Mark001';
    ```

---

## Data Analysis Using Power BI

- To normalize the `sales_amount` based on the currency in Power BI, use the following formula to create a `norm_amount` column:

    ```powerquery
    = Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] = "USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)
    ```

---

## Tools Used
- Power BI
- Microsoft Excel
- SQL

# Power BI Sales Insights Dashboard
To view the dashboard, [download the Power BI file](https://github.com/Shagun292001/Sales-Insights-Data-Analysis-Project/blob/main/Power%20bi.pbix) and open it in Power BI Desktop.

