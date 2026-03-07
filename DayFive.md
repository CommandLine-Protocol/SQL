Day 5 is where SQL thinking becomes **nested and analytical**. This is the stage where many interview questions come from because it tests **logical depth**, not just syntax.

You will learn **subqueries**, also called **nested queries**.

# 🟢 DAY 5 – Subqueries + Nested Thinking (3–4 Hours)

# ⏱ Hour 1 – Subqueries in `WHERE`

## 1️⃣ What Is a Subquery?

A **subquery** is a query inside another query.

Structure:

```sql
SELECT ...
FROM ...
WHERE column OPERATOR (
    SELECT ...
);
```

The inner query runs **first** and its result is used by the outer query.

---

### Example Dataset (Continue Using Earlier Tables)

Tables:

- users
- orders
- products
- order_items

---

## Example 1 – Users Who Spent More Than Average

First understand the average:

```sql
SELECT AVG(amount) FROM orders;
```

Now combine:

```sql
SELECT *
FROM orders
WHERE amount > (
    SELECT AVG(amount)
    FROM orders
);
```

Explanation:

1. Inner query calculates average.
2. Outer query compares each row to that value.

---

## Example 2 – Users Who Made Purchases

```sql
SELECT *
FROM users
WHERE id IN (
    SELECT user_id
    FROM orders
);
```

The inner query returns a list of IDs.

---

## Example 3 – Users With No Orders

```sql
SELECT *
FROM users
WHERE id NOT IN (
    SELECT user_id
    FROM orders
);
```

This is logically similar to a LEFT JOIN + NULL filter.

---

## 🔬 Academic Concept

Subqueries can return:

1️⃣ **Single value** (scalar subquery)
2️⃣ **Single column list**
3️⃣ **Full table result**

SQL uses them depending on operator.

# ⏱ Hour 2 – Subqueries in `FROM`

This creates **temporary tables**.

---

### Example – Average Spending Per User

```sql
SELECT AVG(total_spent)
FROM (
    SELECT user_id, SUM(amount) AS total_spent
    FROM orders
    GROUP BY user_id
) AS user_spending;
```

Explanation:

Inner query:

Creates temporary table:

| user_id | total_spent |

Outer query:

Calculates average.

---

## Why This Matters

This technique powers:

- dashboards
- analytics
- reports
- data pipelines

# ⏱ Hour 3 – Interview Classic Problems

These appear constantly in SQL interviews.

---

## 1️⃣ Second Highest Salary (Classic)

Example table:

```sql
CREATE TABLE employees (
    id INT,
    name VARCHAR(100),
    salary INT
);
```

Insert:

```sql
INSERT INTO employees VALUES
(1,'Alice',5000),
(2,'Bob',7000),
(3,'Carol',6000),
(4,'David',7000);
```

Query:

```sql
SELECT MAX(salary)
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

Logic:

1️⃣ Find highest salary
2️⃣ Find highest salary less than that

---

## 2️⃣ Duplicate Emails

Example:

```sql
CREATE TABLE accounts (
    id INT,
    email VARCHAR(100)
);
```

Solution:

```sql
SELECT email
FROM accounts
GROUP BY email
HAVING COUNT(*) > 1;
```

---

## 3️⃣ Users With Above Average Spending

```sql
SELECT user_id, SUM(amount)
FROM orders
GROUP BY user_id
HAVING SUM(amount) > (
    SELECT AVG(amount)
    FROM orders
);
```

---

## 4️⃣ Products More Expensive Than Average

```sql
SELECT *
FROM products
WHERE price > (
    SELECT AVG(price)
    FROM products
);
```

# ⏱ Hour 4 – Correlated Subqueries (Advanced Thinking)

A **correlated subquery** runs once for each row.

Example:

Find users with more orders than average.

```sql
SELECT u.name
FROM users u
WHERE (
    SELECT COUNT(*)
    FROM orders o
    WHERE o.user_id = u.id
) > 2;
```

The inner query references outer query variable.

This is called **correlation**.

---

## Why Correlated Queries Can Be Slow

Database executes inner query repeatedly.

Modern planners often optimize them into joins.

---

# 🧪 Practice Problems (Beginner → Advanced)

---

### 1️⃣ Beginner

Find orders with amount greater than average order amount.

### 2️⃣ Beginner+

Find products with price below average price.

### 3️⃣ Intermediate

Find users who have placed at least one order.

### 4️⃣ Intermediate+

Find users who have never placed an order.

### 5️⃣ Advanced

Find users whose total spending is greater than the average user spending.

### 6️⃣ Advanced+

Find products that were ordered more than once.

### 7️⃣ Interview Hard

Find employees with the **third highest salary**.

(Hint: nested subqueries)

# 🧠 Academic Concept Questions

### 1️⃣ What is the difference between a JOIN and a subquery?

### 2️⃣ What is a scalar subquery?

### 3️⃣ Why can correlated subqueries be inefficient?

### 4️⃣ When should you prefer JOIN over subquery?

### 5️⃣ What happens if a subquery returns multiple values but the operator expects one?

# 🔥 Practice Platforms

Focus on subquery problems.

- [https://leetcode.com/problemset/database/](https://leetcode.com/problemset/database/)
- [https://pgexercises.com/](https://pgexercises.com/)
- [https://sqlzoo.net/](https://sqlzoo.net/)
- [https://www.hackerrank.com/domains/sql](https://www.hackerrank.com/domains/sql)

---

# 🎯 End of Day 5 Goals

You should now:

✔ Understand nested queries
✔ Solve interview-style SQL problems
✔ Write queries with subqueries
✔ Understand correlated queries
✔ Think analytically about data

---

# 🚀 Mini Project Challenge

Using the store dataset, answer:

1️⃣ Which user spent the most?
2️⃣ Which product generated the most revenue?
3️⃣ Which users spent above average?
4️⃣ Which products were never ordered?
5️⃣ Which order had the highest total quantity?

---

Tomorrow (Day 6):

We go deeper into **database design and performance**, including:

- Normalization (1NF, 2NF, 3NF)
- Indexes (how queries become fast)
- Constraints
- Designing real database schemas

This is where SQL knowledge becomes **professional database engineering**.
