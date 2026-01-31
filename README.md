# SQL Sales Analysis – Business Case Study

## Overview
This project analyzes sales data using SQL to extract actionable business insights and support data-driven decision-making.

## Tools Used
- SQL (MySQL / PostgreSQL / SQLite)
- Optional: DB Browser, DBeaver

## Database Setup
- **Database Name:** `sales_db`  
- **Tables:**
  - `customers` – contains customer information (ID, name, contact, etc.)
  - `orders` – contains order details (order ID, customer ID, product ID, quantity, price, date)
  - `products` – contains product details (product ID, name, category, stock, price)

## Queries Executed
**Retrieve all data from tables:**
```sql
SELECT * FROM customers;
SELECT * FROM orders;
SELECT * FROM products;
SELECT o.order_id, c.name, p.product_name, o.quantity, o.price
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
JOIN products p ON o.product_id = p.product_id;
-- Total sales by product category
SELECT p.category, SUM(o.price * o.quantity) AS total_sales
FROM orders o
JOIN products p ON o.product_id = p.product_id
GROUP BY p.category;

-- Count of orders per customer
SELECT c.name, COUNT(o.order_id) AS total_orders
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
GROUP BY c.name;
SELECT p.product_name, SUM(o.quantity) AS total_sold
FROM orders o
JOIN products p ON o.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_sold DESC
LIMIT 5;
