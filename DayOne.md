# 🟢 DAY 1 – Database Foundations + SELECT (4 Hours Deep Dive)

---

# ⏱ Hour 1 – Academic Foundations (How Databases Actually Work)

---

## 1️⃣ What Is a Relational Database?

A **relational database** is a structured system for storing data in **tables** where relationships between tables are defined using keys.

The concept comes from **Edgar F. Codd** at IBM in 1970.

### Core Idea:

Data is stored in **relations** (tables), not files.

Each table:

- Has rows (tuples)
- Has columns (attributes)
- Has a defined schema

Example:

| id  | name  | email                                     |
| --- | ----- | ----------------------------------------- |
| 1   | Alice | [alice@email.com](mailto:alice@email.com) |

This table represents a mathematical relation.

---

## 2️⃣ What is a DBMS?

A **DBMS (Database Management System)** is software that:

- Stores data
- Retrieves data
- Enforces constraints
- Manages concurrency
- Ensures security
- Handles backups

Examples:

- PostgreSQL
- MySQL
- Oracle Database
- Microsoft SQL Server

You are learning the language (SQL), not the engine itself.

---

## 3️⃣ Tables, Rows, Columns (Formal View)

### Table

Logical container for structured data.

### Row (Tuple)

Single record.

### Column (Attribute)

Defines property and datatype.

Schema = Blueprint of table.

Example schema:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    created_at DATE
);
```

---

## 4️⃣ Primary Key

A **primary key**:

- Uniquely identifies each row
- Cannot be NULL
- Must be unique

Example:

```sql
id INT PRIMARY KEY
```

Why important?
Without it, you cannot reliably identify records.

---

## 5️⃣ Foreign Key

A **foreign key**:

- Links one table to another
- Enforces referential integrity

Example:

```sql
CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

This ensures:
You cannot create an order for a user that does not exist.

---

## 6️⃣ Normalization (Intro Only Today)

Normalization = process of reducing redundancy.

Goal:

- Avoid duplicate data
- Avoid update anomalies
- Improve consistency

Example of bad design:

| user_id | user_name | order_id |
| ------- | --------- | -------- |

If user_name changes, you update many rows.

Normalized design separates users and orders.

We will go deeper on Day 6.

---

## 7️⃣ ACID (Critical Concept)

ACID properties guarantee reliability:

### A – Atomicity

Transaction happens fully or not at all.

### C – Consistency

Database remains valid after transaction.

### I – Isolation

Concurrent transactions don’t break each other.

### D – Durability

Committed data survives crashes.

Example:
Bank transfer must be atomic.

---

# ⏱ Hour 2 – Setting Up Locally (Postgres or MySQL)

Choose ONE.

---

# OPTION A – PostgreSQL Setup (Recommended)

1️⃣ Download:
[https://www.postgresql.org/download/](https://www.postgresql.org/download/)

2️⃣ Install:

- Keep default port (5432)
- Set password for user `postgres`
- Install pgAdmin

3️⃣ Open pgAdmin
4️⃣ Create database:
Right click → Create → Database → name it `sql_bootcamp`

5️⃣ Open Query Tool

---

# OPTION B – MySQL Setup

1️⃣ Download:
[https://dev.mysql.com/downloads/installer/](https://dev.mysql.com/downloads/installer/)

2️⃣ Install:

- Choose Developer Default
- Set root password
- Install MySQL Workbench

3️⃣ Open MySQL Workbench
4️⃣ Create schema:

```sql
CREATE DATABASE sql_bootcamp;
USE sql_bootcamp;
```

---

# ⏱ Hour 3 – Basic Queries (Deep Understanding)

---

## 1️⃣ SELECT

Basic form:

```sql
SELECT column_name FROM table_name;
```

Example:

```sql
SELECT name FROM users;
```

Returns one column.

---

## 2️⃣ SELECT \*

```sql
SELECT * FROM users;
```

Returns all columns.

⚠ Avoid in production when tables are large.

---

## 3️⃣ WHERE

Filtering condition:

```sql
SELECT * FROM users
WHERE id = 1;
```

---

## 4️⃣ ORDER BY

Sort results:

```sql
SELECT * FROM users
ORDER BY name ASC;
```

DESC for descending.

---

## 5️⃣ LIMIT

Restrict rows (Postgres/MySQL):

```sql
SELECT * FROM users
LIMIT 5;
```

---

## 6️⃣ DISTINCT

Remove duplicates:

```sql
SELECT DISTINCT name FROM users;
```

---

# Practice Setup Data

Create this table:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    country VARCHAR(50),
    signup_year INT
);
```

Insert:

```sql
INSERT INTO users VALUES
(1, 'Alice', 25, 'USA', 2023),
(2, 'Bob', 30, 'UK', 2024),
(3, 'Carol', 22, 'USA', 2024),
(4, 'David', 35, 'Canada', 2022),
(5, 'Eve', 28, 'UK', 2023);
```

Now practice 20+ queries.

---

# ⏱ Hour 4 – Guided Practice

Use:

- [https://www.w3schools.com/sql/](https://www.w3schools.com/sql/)
- [https://www.hackerrank.com/domains/sql](https://www.hackerrank.com/domains/sql)
- [https://leetcode.com/problemset/database/](https://leetcode.com/problemset/database/)

Focus on:

- Filtering
- Sorting
- Simple retrieval

---

# 🧠 Test Questions (Beginner → Advanced)

---

### 1️⃣ Beginner

Write a query to retrieve all users from the UK.

---

### 2️⃣ Beginner+

Select only the names and ages of users older than 25.

---

### 3️⃣ Intermediate

Retrieve users who signed up after 2022 and sort them by age descending.

---

### 4️⃣ Intermediate+

Count how many users are from the USA.

---

### 5️⃣ Advanced Thinking

Explain why a primary key improves indexing performance internally in a B-tree structure.

---

### 6️⃣ Advanced

If two concurrent transactions update the same row, which ACID property ensures they don’t corrupt data?

---

# 🔥 Additional Deep Practice Links

- [https://pgexercises.com/](https://pgexercises.com/) (PostgreSQL specific)
- [https://sqlzoo.net/](https://sqlzoo.net/)
- [https://mode.com/sql-tutorial/](https://mode.com/sql-tutorial/)
- [https://leetcode.com/problemset/database/](https://leetcode.com/problemset/database/)

---

# 🎯 What You Must Understand By End of Day 1

You must:

✔ Understand what a relational model is
✔ Know what ACID means
✔ Know why primary keys matter
✔ Create tables
✔ Insert data
✔ Write filtered SELECT queries confidently

---

# 🚀 Homework Challenge (Important)

Design a simple `students` table with:

- id
- name
- age
- grade
- enrollment_year

Insert 10 records.

Write queries:

1. Students older than 18
2. Students in grade A
3. Top 3 oldest students
4. Distinct grades
5. Students enrolled after 2022

---

Tomorrow (Day 2):
We move into logical filtering mastery and SQL thinking patterns.

---
