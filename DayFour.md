**Day 4** is the most important day for backend development.

This is where SQL stops being “table queries” and becomes **relational thinking**.

If you master today, you understand how real web applications work internally.

---

# 🟢 DAY 4 – JOINS (Critical for Web Development) (4 Hours)

# ⏱ Hour 1 – Academic Foundation (How Relationships Work)

## 1️⃣ Why JOINS Exist

Relational databases avoid duplication through normalization.

Instead of this (bad design):

| order_id | user_name | product_name |
| -------- | --------- | ------------ |

We split into tables:

users <br>
orders <br>
products <br>

Now data is clean — but separated.

JOINS reconstruct relationships when querying.

---

## 2️⃣ Types of Relationships

### One-to-Many

One user → Many orders

users (1) —— (∞) orders

Foreign key exists in “many” side.

---

### Many-to-Many

Many students → Many courses

Requires junction table:

students<br>
courses<br>
student_courses<br>

---

## 3️⃣ Foreign Keys (Reinforcement)

Example:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    amount INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

Now orders.user_id links to users.id.

---

## 🔬 Internal Concept

JOIN does not merge tables permanently.

It creates a **virtual result set** during execution.

Internally:

- Nested loop join
- Hash join
- Merge join

We go deeper on optimization later.

# ⏱ Hour 2 – Types of JOINS (Practical Mastery)

## Setup Practice Dataset

Run this in PostgreSQL or MySQL:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    amount INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

INSERT INTO users VALUES
(1, 'Alice'),
(2, 'Bob'),
(3, 'Carol'),
(4, 'David');

INSERT INTO orders VALUES
(1, 1, 200),
(2, 1, 150),
(3, 2, 300),
(4, 3, 400);
```

---

## 1️⃣ INNER JOIN

Returns only matching rows.

```sql
SELECT users.name, orders.amount
FROM users
INNER JOIN orders
ON users.id = orders.user_id;
```

Result:
Only users who have orders.

David disappears (no order).

---

## 2️⃣ LEFT JOIN

Returns all rows from left table.

```sql
SELECT users.name, orders.amount
FROM users
LEFT JOIN orders
ON users.id = orders.user_id;
```

Now David appears with NULL amount.

---

## 3️⃣ RIGHT JOIN

Opposite of LEFT JOIN.

Returns all rows from right table.

(MySQL & PostgreSQL support it.)

---

## 4️⃣ FULL OUTER JOIN

PostgreSQL supports it.
MySQL does not directly.

Returns everything from both sides.

---

## 5️⃣ SELF JOIN

Table joins itself.

Example:
Find users who share the same name:

```sql
SELECT u1.name, u2.id
FROM users u1
JOIN users u2
ON u1.name = u2.name
AND u1.id <> u2.id;
```

# ⏱ Hour 3 – Real Web App Simulation

Imagine an online store.

## Expanded Dataset

```sql
CREATE TABLE products (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    price INT
);

INSERT INTO products VALUES
(1, 'Laptop', 1000),
(2, 'Phone', 500),
(3, 'Tablet', 700);

CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT,
    FOREIGN KEY (order_id) REFERENCES orders(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);

INSERT INTO order_items VALUES
(1, 1, 1),
(1, 2, 2),
(2, 3, 1),
(3, 2, 3),
(4, 1, 1);
```

Now we simulate backend queries.

---

## 1️⃣ Find All Orders With User Names

```sql
SELECT orders.id, users.name, orders.amount
FROM orders
JOIN users ON orders.user_id = users.id;
```

---

## 2️⃣ Find Products Purchased By Alice

```sql
SELECT products.name
FROM users
JOIN orders ON users.id = orders.user_id
JOIN order_items ON orders.id = order_items.order_id
JOIN products ON order_items.product_id = products.id
WHERE users.name = 'Alice';
```

This is real backend-level SQL.

---

## 3️⃣ Total Revenue Per User

```sql
SELECT users.name, SUM(orders.amount)
FROM users
JOIN orders ON users.id = orders.user_id
GROUP BY users.name;
```

---

## 4️⃣ Users With No Orders

```sql
SELECT users.name
FROM users
LEFT JOIN orders ON users.id = orders.user_id
WHERE orders.id IS NULL;
```

Classic interview question.

# ⏱ Hour 4 – Deep Academic Thinking

## What Happens Internally During JOIN?

Database must decide:

- Which table to scan first?
- Which join algorithm to use?

Three main strategies:

1️⃣ Nested Loop Join
2️⃣ Hash Join
3️⃣ Merge Join

Choice depends on:

- Indexes
- Table size
- Statistics

## JOIN Order Matters

```sql
FROM users
JOIN orders
```

Is logically same as reversed.

But execution plan may differ.

Query planner optimizes automatically.

# 🧪 Practice Questions (Solve Fully)

### 1️⃣ Beginner

List all orders with user names.

### 2️⃣ Beginner+

Find all users and their total number of orders.

### 3️⃣ Intermediate

Find total amount spent by each user.

### 4️⃣ Intermediate+

Find the most purchased product. <br>
(Hint: SUM quantity + GROUP BY product)

### 5️⃣ Advanced

Find users who never purchased anything.

### 6️⃣ Advanced+

Find the user who generated the highest revenue.

### 7️⃣ Interview Classic

Find products that were never ordered.

# 🧠 Conceptual Questions (Interview Level)

### 1️⃣ What is the difference between INNER JOIN and LEFT JOIN?

### 2️⃣ Why is a foreign key important for JOIN correctness?

### 3️⃣ What happens if you JOIN without ON condition?

(Cartesian product)

### 4️⃣ How does indexing improve JOIN performance?

### 5️⃣ Explain nested loop join in simple terms.

# 🔥 Strong Practice Resources

- [https://pgexercises.com/](https://pgexercises.com/)
- [https://leetcode.com/problemset/database/](https://leetcode.com/problemset/database/)
- [https://sqlzoo.net/](https://sqlzoo.net/)
- [https://www.hackerrank.com/domains/sql](https://www.hackerrank.com/domains/sql)

Focus on multi-table problems.

# 🎯 End of Day 4 Goals

You should now:

✔ Understand relational modeling<br>
✔ Write multi-table JOIN queries<br>
✔ Combine JOIN + GROUP BY<br>
✔ Think like backend developer<br>
✔ Solve real app-level SQL<br>

---

Tomorrow (Day 5):

We go into:

Subqueries
Nested thinking
Second highest salary
Ranking logic
Correlated subqueries
