# SQL Sales Analysis – Business Case Study

## Overview
This project focuses on analyzing sales data using SQL to extract actionable business insights and support data-driven decision-making. The analysis covers customer behavior, product performance, and overall sales trends.

## Tools Used
- SQL (MySQL / PostgreSQL / SQLite)
- DB Browser / DBeaver

## Database Setup
- **Database Name:** `sales_db`

### Tables
- `customers` – Stores customer information such as customer ID, name, and contact details.
- `orders` – Stores order details including order ID, customer ID, product ID, quantity, price, and order date.
- `products` – Stores product information including product ID, product name, category, stock level, and price.

## SQL Queries Performed

### 1. View complete data from all tables
```sql
-- View complete data from all tables
SELECT * FROM customers;
SELECT * FROM orders;
SELECT * FROM products;

SELECT
    o.order_id,
    c.name AS customer_name,
    p.product_name,
    o.quantity,
    o.price
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
JOIN products p ON o.product_id = p.product_id;


```
## Total sales by product category
```sql
SELECT
    p.category,
    SUM(o.price * o.quantity) AS total_sales
FROM orders o
JOIN products p ON o.product_id = p.product_id
GROUP BY p.category;

```

## Total number of orders per customer
```sql

SELECT
    c.name AS customer_name,
    COUNT(o.order_id) AS total_orders
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
GROUP BY c.name;

```

## Top 5 products by total quantity sold
```sql

SELECT
    p.product_name,
    SUM(o.quantity) AS total_sold
FROM orders o
JOIN products p ON o.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_sold DESC
LIMIT 5;

```
## Key Business Insights
- Certain product categories generate significantly higher revenue, indicating strong customer demand.
- A small group of customers contributes to a large number of orders, highlighting high-value customers.
- Top-selling products should be prioritized for inventory restocking.
- Sales trends can be used for future forecasting and planning.
## How to Run the Project

1. Open your SQL tool (MySQL / PostgreSQL / SQLite).
2. Create the database:
```sql
CREATE DATABASE sales_db;
USE sales_db;
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    contact VARCHAR(50)
);

CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    stock INT,
    price DECIMAL(10,2)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    product_id INT,
    quantity INT,
    price DECIMAL(10,2),
    order_date DATE,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
INSERT INTO customers (customer_id, name, contact) VALUES
(1, 'Amit Sharma', 'amit@gmail.com'),
(2, 'Neha Verma', 'neha@gmail.com'),
(3, 'Rahul Singh', 'rahul@gmail.com');
INSERT INTO products (product_id, product_name, category, stock, price) VALUES
(101, 'Laptop', 'Electronics', 50, 55000),
(102, 'Mobile Phone', 'Electronics', 100, 25000),
(103, 'Office Chair', 'Furniture', 40, 7000),
(104, 'Notebook', 'Stationery', 200, 100);INSERT INTO orders (order_id, customer_id, product_id, quantity, price, order_date) VALUES
(1001, 1, 101, 1, 55000, '2024-01-10'),
(1002, 2, 102, 2, 25000, '2024-01-12'),
(1003, 3, 103, 1, 7000, '2024-01-15'),
(1004, 1, 104, 10, 100, '2024-01-18'),
(1005, 2, 101, 1, 55000, '2024-01-20');
SELECT * FROM customers;
SELECT * FROM products;
SELECT * FROM orders;
-- Total sales by category
SELECT 
    p.category,
    SUM(o.price * o.quantity) AS total_sales
FROM orders o
JOIN products p ON o.product_id = p.product_id
GROUP BY p.category;
-- Orders per customer
SELECT 
    c.name,
    COUNT(o.order_id) AS total_orders
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
GROUP BY c.name;
-- Top 5 products
SELECT 
    p.product_name,
    SUM(o.quantity) AS total_sold
FROM orders o
JOIN products p ON o.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_sold DESC
LIMIT 5;

```

### CONCLUSION
 This project demonstrates the practical use of SQL for real-world business analysis.

 It covers essential SQL concepts such as data retrieval, joins, and aggregations.

 The project shows how raw sales data can be transformed into meaningful business insights.

### AUTHOR
Shanti Kumari Verma
