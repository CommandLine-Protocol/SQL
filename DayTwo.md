**Day 2** is where you start thinking like a backend developer instead of just writing syntax.

You already know `SELECT`, `WHERE`, and sorting.
Today we master **logical filtering + translating English into SQL**.

# 🟢 DAY 2 – Filtering + Logical Thinking (3–4 Hours)

# ⏱ Hour 1.5 – Advanced Filtering (Deep Understanding)

We continue using PostgreSQL or MySQL locally.

If you completed Day 1, you already have the `users` table.
If not, recreate it:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    country VARCHAR(50),
    signup_year INT,
    purchases INT
);

INSERT INTO users VALUES
(1, 'Alice', 25, 'USA', 2023, 5),
(2, 'Bob', 30, 'UK', 2024, 2),
(3, 'Carol', 22, 'USA', 2024, 8),
(4, 'David', 35, 'Canada', 2022, 1),
(5, 'Eve', 28, 'UK', 2023, 4),
(6, 'Frank', 40, 'USA', 2021, 10),
(7, 'Grace', 19, 'Germany', 2024, 0);
```

---

## 1️⃣ AND / OR (Boolean Logic in SQL)

### AND

Both conditions must be true.

```sql
SELECT * FROM users
WHERE country = 'USA' AND age > 25;
```

### OR

At least one condition must be true.

```sql
SELECT * FROM users
WHERE country = 'USA' OR country = 'UK';
```

---

### 🔬 Academic Insight

SQL evaluates logical conditions using Boolean algebra.

Order of evaluation:

1. Parentheses
2. NOT
3. AND
4. OR

Example:

```sql
SELECT * FROM users
WHERE country = 'USA'
AND (age > 30 OR purchases > 5);
```

Without parentheses, your logic may change.

---

## 2️⃣ IN

Cleaner alternative to multiple ORs.

Instead of:

```sql
WHERE country = 'USA' OR country = 'UK'
```

Use:

```sql
WHERE country IN ('USA', 'UK')
```

This improves readability and execution planning.

---

## 3️⃣ BETWEEN

Range filtering.

```sql
SELECT * FROM users
WHERE age BETWEEN 20 AND 30;
```

Important:
`BETWEEN` is inclusive.

Equivalent to:

```sql
age >= 20 AND age <= 30
```

---

## 4️⃣ LIKE (Pattern Matching)

Used for string searching.

### Wildcards:

- `%` → any number of characters
- `_` → single character

Example:

Users whose name starts with A:

```sql
SELECT * FROM users
WHERE name LIKE 'A%';
```

Names ending with 'e':

```sql
WHERE name LIKE '%e';
```

Names that contain the letter 'o'

```sql
WHERE name LIKE '%o%'
```

---

### Case Sensitivity

- PostgreSQL: `LIKE` is case-sensitive. Use `ILIKE` for case-insensitive.
- MySQL: Usually case-insensitive depending on collation.

---

## 5️⃣ IS NULL

NULL is NOT zero.
NULL means “unknown” or “missing.”

```sql
SELECT * FROM users
WHERE purchases IS NULL;
```

Never use:

```sql
WHERE purchases = NULL
```

That will NOT work.

---

# ⏱ Hour 2 – Translating English → SQL (Critical Skill)

This is what interviewers test.

---

## Example 1

English:

> Find users who signed up in 2024 and made more than 3 purchases.

SQL:

```sql
SELECT * FROM users
WHERE signup_year = 2024
AND purchases > 3;
```

---

## Example 2

English:

> Find users from USA or UK who are older than 25.

SQL:

```sql
SELECT * FROM users
WHERE country IN ('USA', 'UK')
AND age > 25;
```

---

## Example 3 (Trickier)

English:

> Find users who are NOT from Canada and signed up before 2024.

SQL:

```sql
SELECT * FROM users
WHERE country <> 'Canada'
AND signup_year < 2024;
```

Or:

```sql
WHERE NOT country = 'Canada'
```

---

## Example 4 (Logic Priority)

English:

> Users from USA who are older than 30 OR have more than 8 purchases.

Correct:

```sql
SELECT * FROM users
WHERE country = 'USA'
AND (age > 30 OR purchases > 8);
```

If you remove parentheses, the logic changes.

# ⏱ Hour 3 – Practice Set (Solve Without Looking at Answers)

### 1️⃣ Beginner

Find users younger than 25.

### 2️⃣ Beginner+

Find users from Germany or Canada.

### 3️⃣ Intermediate

Find users aged between 25 and 35 who are from the UK.

### 4️⃣ Intermediate+

Find users whose name starts with 'C'.

### 5️⃣ Advanced

Find users who:

- Are from USA
- Signed up after 2022
- AND have more than 5 purchases

### 6️⃣ Advanced Logic

Find users who:

- Are from USA or UK
- AND are younger than 30
- BUT exclude those with 8 purchases

# ⏱ Hour 4 – Real Job-Oriented Practice

Use:

- [https://leetcode.com/problemset/database/](https://leetcode.com/problemset/database/)
- [https://www.hackerrank.com/domains/sql](https://www.hackerrank.com/domains/sql)
- [https://sqlzoo.net/](https://sqlzoo.net/)

Focus only on filtering problems today.

# 🧠 Academic Deep Dive (Important Concept)

## How Filtering Works Internally

When you run:

```sql
SELECT * FROM users
WHERE age > 30;
```

The database:

1. Parses query
2. Creates execution plan
3. Decides:
   - Full table scan?
   - Use index?

4. Filters rows
5. Returns result

Without index:
It scans every row.

With index:
It uses a B-tree structure to jump directly to relevant rows.

We go deeper into indexing on Day 6.

# 🧪 Test Questions (Beginner → Advanced)

### 1️⃣ What is the difference between `AND` and `OR` in terms of result set size?

### 2️⃣ Why does `= NULL` not work?

### 3️⃣ Write a query to find users whose name contains the letter 'a' anywhere.

### 4️⃣ Explain how parentheses change logical evaluation in SQL.

### 5️⃣ If a table has 1 million rows and no index, what happens internally when you filter by age?

### 6️⃣ Advanced

Explain how SQL’s three-valued logic (TRUE, FALSE, UNKNOWN) affects NULL comparisons.

# 🎯 End of Day 2 Goals

You should now:

✔ Write multi-condition filters confidently
✔ Translate English to SQL
✔ Understand Boolean logic in queries
✔ Know how NULL behaves
✔ Think like a backend engineer

# 🚀 Mini Challenge (Simulated Startup Scenario)

Imagine a startup app.

Find:

1. Active users (purchases > 0)
2. Dormant users (purchases = 0)
3. VIP users (purchases > 7)
4. Users from top 2 countries
5. Users under 25 from USA or Germany

Write all queries.

---

Tomorrow (Day 3):

We enter **Aggregations — the most important topic for SQL job interviews.**

That’s where SQL starts becoming powerful.

---
