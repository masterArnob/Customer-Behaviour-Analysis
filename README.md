# 🛍️ Customer Shopping Behaviour Analysis

![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg)
![SQL](https://img.shields.io/badge/SQL-MySQL%20%7C%20SQLite-orange.svg)
![Pandas](https://img.shields.io/badge/Library-Pandas-yellow.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

---

## 📖 Project Overview

This project analyzes **customer shopping behaviour** using transactional data from nearly **4,000 purchases** across various product categories.  
The objective is to uncover insights into:

- Purchase patterns  
- Customer segmentation  
- Product and category performance  
- Gender- and age-based spending  
- Revenue optimization opportunities  

The findings guide **data-driven business decisions** to improve marketing, customer engagement, and sales strategy.

---

## 🧹 Data Cleaning (Python)

Performed using **Python (Pandas, NumPy)**:

- ✅ Handled missing data  
- ✅ Renamed and standardized columns  
- ✅ Feature engineering for better grouping and aggregation  
- ✅ Ensured data type consistency  

---

## 📊 Data Analysis (SQL)

SQL was used to analyze cleaned data stored in a relational database.  
Key insights were derived through **structured queries** such as:

### 🔹 Q1: Product Performance
```sql
WITH sales_data AS(
    SELECT item_purchased AS product_name,
           SUM(purchase_amount) AS current_sales
    FROM customer
    GROUP BY item_purchased
)
SELECT product_name, current_sales,
       (SELECT AVG(current_sales) FROM sales_data) AS average_sales,
       current_sales - (SELECT AVG(current_sales) FROM sales_data) AS sales_difference,
       CASE
           WHEN current_sales - (SELECT AVG(current_sales) FROM sales_data) > 0 THEN 'Profit'
           WHEN current_sales - (SELECT AVG(current_sales) FROM sales_data) < 0 THEN 'Loss'
           ELSE 'Average'
       END AS performance
FROM sales_data;
