# 🛒 Retail Inventory Management System (SQL-Based)

A structured and efficient inventory management system for retail stores, implemented entirely using SQL. This project demonstrates how to design, implement, and query a relational database to manage products, suppliers, inventory levels, and transactions within a retail environment.

---

## 📌 Features

- 🧾 Product and Category Management  
- 📦 Inventory Tracking (stock in/out, current levels)  
- 🧍 Supplier Management  
- 💰 Purchase and Sales Transactions  
- 📊 Analytical SQL Queries for Insights

---

## 🧱 Database Schema

The system is built using multiple normalized tables. Key tables include:

### 🔹 `products`
| Column        | Type        | Description                  |
|---------------|-------------|------------------------------|
| product_id    | INT (PK)    | Unique product ID            |
| name          | VARCHAR     | Product name                 |
| category_id   | INT (FK)    | Reference to product category|
| price         | DECIMAL     | Selling price per unit       |

### 🔹 `categories`
| Column       | Type      | Description         |
|--------------|-----------|---------------------|
| category_id  | INT (PK)  | Unique category ID  |
| name         | VARCHAR   | Category name       |

### 🔹 `suppliers`
| Column        | Type      | Description           |
|---------------|-----------|-----------------------|
| supplier_id   | INT (PK)  | Unique supplier ID    |
| name          | VARCHAR   | Supplier company name |
| contact_info  | VARCHAR   | Phone/email           |

### 🔹 `inventory`
| Column       | Type     | Description                    |
|--------------|----------|--------------------------------|
| inventory_id | INT (PK) | Unique inventory record        |
| product_id   | INT (FK) | Product reference              |
| quantity     | INT      | Current stock level            |
| updated_at   | DATE     | Last update timestamp          |

### 🔹 `purchases`
| Column        | Type     | Description                    |
|---------------|----------|--------------------------------|
| purchase_id   | INT (PK) | Purchase transaction ID        |
| product_id    | INT (FK) | Product reference              |
| supplier_id   | INT (FK) | Supplier reference             |
| quantity      | INT      | Purchased quantity             |
| purchase_date | DATE     | Date of purchase               |

### 🔹 `sales`
| Column       | Type     | Description                    |
|--------------|----------|--------------------------------|
| sale_id      | INT (PK) | Sale transaction ID            |
| product_id   | INT (FK) | Product reference              |
| quantity     | INT      | Sold quantity                  |
| sale_date    | DATE     | Date of sale                   |

---

## 📈 Sample Analytical Queries

Here are examples of SQL queries used for analysis:

### 🔍 Top 5 Bestselling Products
```sql
SELECT p.name, SUM(s.quantity) AS total_sold
FROM sales s
JOIN products p ON s.product_id = p.product_id
GROUP BY p.name
ORDER BY total_sold DESC
LIMIT 5;
