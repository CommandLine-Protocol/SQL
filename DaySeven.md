Day 7 is where everything comes together — **real-world simulation**. <br>
You’re no longer “learning SQL”… you’re **using SQL like a professional**.

---

# 🟢 DAY 7 – Real Project Simulation (4 Hours)

# 🎯 Objective

You will:

- Design a working schema
- Populate realistic data
- Write **25+ real-world queries**
- Think like a backend developer / data analyst

---

# ⏱ Hour 1 – Full Project Setup (Online Store)

## 1️⃣ Create Database

PostgreSQL:

```sql
CREATE DATABASE sql_project;
```

MySQL:

```sql
CREATE DATABASE sql_project;
USE sql_project;
```

---

## 2️⃣ Create Tables (Final Design)

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    created_at DATE
);

CREATE TABLE products (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    category VARCHAR(50),
    price INT
);

CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    order_date DATE,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id),
    FOREIGN KEY (order_id) REFERENCES orders(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

---

## 3️⃣ Insert Sample Data

```sql
INSERT INTO users VALUES
(1, 'Alice', 'alice@email.com', '2023-01-10'),
(2, 'Bob', 'bob@email.com', '2023-03-15'),
(3, 'Carol', 'carol@email.com', '2024-02-20'),
(4, 'David', 'david@email.com', '2024-05-01');

INSERT INTO products VALUES
(1, 'Laptop', 'Electronics', 1000),
(2, 'Phone', 'Electronics', 500),
(3, 'Shoes', 'Fashion', 150),
(4, 'Watch', 'Accessories', 200);

INSERT INTO orders VALUES
(1, 1, '2024-01-01'),
(2, 1, '2024-02-10'),
(3, 2, '2024-03-05'),
(4, 3, '2024-04-01');

INSERT INTO order_items VALUES
(1, 1, 1),
(1, 2, 2),
(2, 3, 1),
(3, 2, 3),
(4, 4, 1);
```

---

# ⏱ Hour 2 – Core Business Queries

## 1️⃣ Top 5 Customers (by number of orders)

```sql
SELECT users.name, COUNT(orders.id) AS total_orders
FROM users
JOIN orders ON users.id = orders.user_id
GROUP BY users.name
ORDER BY total_orders DESC
LIMIT 5;
```

---

## 2️⃣ Total Revenue

```sql
SELECT SUM(products.price * order_items.quantity) AS total_revenue
FROM order_items
JOIN products ON order_items.product_id = products.id;
```

---

## 3️⃣ Monthly Revenue

```sql
SELECT DATE_TRUNC('month', orders.order_date) AS month,
SUM(products.price * order_items.quantity) AS revenue
FROM orders
JOIN order_items ON orders.id = order_items.order_id
JOIN products ON products.id = order_items.product_id
GROUP BY month
ORDER BY month;
```

(MySQL: use `DATE_FORMAT` instead)

---

## 4️⃣ Most Sold Product

```sql
SELECT products.name, SUM(order_items.quantity) AS total_sold
FROM products
JOIN order_items ON products.id = order_items.product_id
GROUP BY products.name
ORDER BY total_sold DESC
LIMIT 1;
```

---

## 5️⃣ Products Never Sold

```sql
SELECT products.name
FROM products
LEFT JOIN order_items
ON products.id = order_items.product_id
WHERE order_items.product_id IS NULL;
```

---

# ⏱ Hour 3 – Advanced Queries (Interview Level)

## 6️⃣ Users With No Orders

```sql
SELECT users.name
FROM users
LEFT JOIN orders ON users.id = orders.user_id
WHERE orders.id IS NULL;
```

---

## 7️⃣ Highest Spending User

```sql
SELECT users.name,
SUM(products.price * order_items.quantity) AS total_spent
FROM users
JOIN orders ON users.id = orders.user_id
JOIN order_items ON orders.id = order_items.order_id
JOIN products ON products.id = order_items.product_id
GROUP BY users.name
ORDER BY total_spent DESC
LIMIT 1;
```

---

## 8️⃣ Average Order Value

```sql
SELECT AVG(order_total)
FROM (
    SELECT orders.id,
    SUM(products.price * order_items.quantity) AS order_total
    FROM orders
    JOIN order_items ON orders.id = order_items.order_id
    JOIN products ON products.id = order_items.product_id
    GROUP BY orders.id
) AS sub;
```

---

## 9️⃣ Most Popular Category

```sql
SELECT products.category,
SUM(order_items.quantity) AS total_sold
FROM products
JOIN order_items ON products.id = order_items.product_id
GROUP BY products.category
ORDER BY total_sold DESC
LIMIT 1;
```

---

## 🔟 Repeat Customers

```sql
SELECT users.name, COUNT(orders.id)
FROM users
JOIN orders ON users.id = orders.user_id
GROUP BY users.name
HAVING COUNT(orders.id) > 1;
```

---

# ⏱ Hour 4 – Full Challenge (Write These Yourself)

## 🎯 Write At Least 15–20 Queries

### 📊 Analytics

1. Total number of users
2. Total number of orders
3. Total revenue
4. Average product price
5. Highest priced product

---

### 👤 User-Based

6. Users who joined in 2024
7. Users who never ordered
8. Users with more than 1 order
9. Top spender

---

### 🛒 Product-Based

10. Products in Electronics category
11. Products never sold
12. Most expensive product per category

---

### 📦 Order-Based

13. Orders in March 2024
14. Largest order (by value)
15. Orders with more than 2 items

---

### 🔥 Advanced

16. Second highest spending user
17. Products sold more than average quantity
18. Monthly growth in revenue
19. Customers who bought Electronics but not Fashion
20. Most consistent buyer (orders every month)

---

# 🧠 Final Interview Questions

### 1️⃣ Design Question

How would you scale this database for millions of users?

### 2️⃣ Optimization

Which columns would you index and why?

### 3️⃣ Theory

Difference between normalization and denormalization?

### 4️⃣ Practical

When would you replace subqueries with JOIN?

### 5️⃣ Architecture

How does SQL connect to backend systems (Node.js / Python)?

---

# 🏁 FINAL OUTCOME (After 7 Days)

You can now:

✔ Write complex SQL queries <br>
✔ Use JOINs, GROUP BY, subqueries <br>
✔ Design relational databases <br>
✔ Understand performance (indexes) <br>
✔ Solve interview questions <br>
✔ Work with backend systems <br>

---

# What NEXT?

Now move to:

### Backend Integration

- Node.js + SQL (e.g. with **Prisma** or raw queries)
- OR Python + SQL (Flask/Django)

# Optional Next Learning Topics

- Query optimization (`EXPLAIN`)
- Transactions
- Stored procedures
- ORMs
