Day 6 is what separates **people who can write queries** from those who can **design real systems**.

Today you learn how databases are **designed, optimized, and enforced**.

# 🟢 DAY 6 – Database Design + Indexing (4 Hours)

# ⏱ Hour 1 – Normalization (Academic Depth)

## 1️⃣ What is Normalization?

Normalization is the process of:

> Structuring a database to reduce redundancy and improve data integrity.

Goals:

- Eliminate duplicate data
- Prevent update anomalies
- Maintain consistency

---

## 🔴 Problem Without Normalization

Bad table:

| user_id | user_name | order_id | product |
| ------- | --------- | -------- | ------- |

Issues:

- User name repeated many times
- Updating name requires multiple updates
- Risk of inconsistency

---

## 2️⃣ First Normal Form (1NF)

Rule:

- No repeating groups
- Atomic values only (no lists inside cells)

❌ Bad:

| id  | products      |
| --- | ------------- |
| 1   | Laptop, Phone |

✅ Good:

| id  | product |
| --- | ------- |
| 1   | Laptop  |
| 1   | Phone   |

---

## 3️⃣ Second Normal Form (2NF)

Rule:

- Must be in 1NF
- No partial dependency on composite key

Example problem:

| order_id | product_id | product_name |

If primary key = (order_id, product_id)

product_name depends only on product_id → violation

✅ Fix:
Split into:

products
order_items

---

## 4️⃣ Third Normal Form (3NF)

Rule:

- Must be in 2NF
- No transitive dependency

❌ Bad:

| user_id | country | country_code |

country_code depends on country, not user_id

✅ Fix:

users
countries

---

## 🔬 Academic Insight

Normalization improves:

- Data integrity
- Storage efficiency
- Logical clarity

Trade-off:

- More joins required

---

# ⏱ Hour 2 – Indexes (Performance Core)

## 1️⃣ What is an Index?

An **index** is a data structure that improves query speed.

Think:
Book index → jump to page instead of reading entire book.

## Without Index

```sql
SELECT * FROM users WHERE age = 30;
```

Database scans ALL rows → slow.

---

## With Index

```sql
CREATE INDEX idx_age ON users(age);
```

Now database uses **B-tree**:

- Logarithmic lookup
- Much faster

## 🔬 How B-Tree Works (Simplified)

- Balanced tree
- Sorted values
- Fast lookup: O(log n)

## 2️⃣ Types of Indexes

- Primary Index (auto-created)
- Unique Index
- Composite Index

Example:

```sql
CREATE INDEX idx_user_country_age
ON users(country, age);
```

## 3️⃣ Trade-offs

Indexes improve:
✔ SELECT speed

But slow down:
❌ INSERT
❌ UPDATE
❌ DELETE

Because index must be updated.

## 4️⃣ When to Use Indexes

Use when:

- Frequent filtering (`WHERE`)
- Joins (`JOIN`)
- Sorting (`ORDER BY`)

Avoid:

- Small tables
- Columns rarely queried

---

# ⏱ Hour 3 – Constraints (Data Integrity)

## 1️⃣ NOT NULL

```sql
name VARCHAR(100) NOT NULL
```

Prevents missing data.

## 2️⃣ UNIQUE

```sql
email VARCHAR(100) UNIQUE
```

No duplicates allowed.

## 3️⃣ PRIMARY KEY

```sql
id INT PRIMARY KEY
```

- Unique
- Not null
- Indexed

## 4️⃣ FOREIGN KEY

```sql
FOREIGN KEY (user_id) REFERENCES users(id)
```

Ensures relational integrity.

## 5️⃣ CHECK

```sql
CHECK (age >= 0)
```

Enforces rules.

## 🔬 Why Constraints Matter

They push validation into the database.

Even if backend fails → database stays correct.

---

# ⏱ Hour 4 – Design a Real System

## 🎯 Project: E-Commerce Database

We design properly normalized schema.

## 1️⃣ Users Table

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL
);
```

## 2️⃣ Products Table

```sql
CREATE TABLE products (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    price INT CHECK (price > 0)
);
```

## 3️⃣ Orders Table

```sql
CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    created_at DATE,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

## 4️⃣ Order Items (Many-to-Many)

```sql
CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT CHECK (quantity > 0),
    PRIMARY KEY (order_id, product_id),
    FOREIGN KEY (order_id) REFERENCES orders(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

## 🔬 Why This Design is Good

✔ No redundancy <br>
✔ Scalable <br>
✔ Maintains integrity <br>
✔ Supports complex queries

## Add Indexes (Performance)

```sql
CREATE INDEX idx_orders_user ON orders(user_id);
CREATE INDEX idx_order_items_product ON order_items(product_id);
```

# 🧪 Practice Questions

### 1️⃣ Beginner

What is normalization and why is it important?

### 2️⃣ Beginner+

Give an example of a 1NF violation.

### 3️⃣ Intermediate

Why does 2NF require removal of partial dependencies?

### 4️⃣ Intermediate+

Explain transitive dependency with an example.

### 5️⃣ Advanced

Why can over-normalization hurt performance?

### 6️⃣ Advanced+

Explain how indexes improve JOIN performance.

### 7️⃣ Interview-Level

Design a database schema for a school system with:

- students
- teachers
- courses
- enrollments

# 🧠 Deep Concept Questions

### 1️⃣ What is the time complexity difference between indexed and non-indexed search?

### 2️⃣ Why are B-trees preferred over arrays for indexing?

### 3️⃣ What happens internally when inserting into an indexed table?

### 4️⃣ Why should foreign keys be indexed?

### 5️⃣ What are trade-offs between normalization and denormalization?

# 🔥 Practice Resources

- [https://pgexercises.com/](https://pgexercises.com/)
- [https://leetcode.com/problemset/database/](https://leetcode.com/problemset/database/)
- [https://sqlzoo.net/](https://sqlzoo.net/)
- [https://www.hackerrank.com/domains/sql](https://www.hackerrank.com/domains/sql)

Focus today:

- Schema design
- Index usage
- Data integrity

---

# 🎯 End of Day 6 Goals

You should now:

✔ Understand normalization (1NF–3NF) <br>
✔ Know how indexes work internally <br>
✔ Use constraints properly <br>
✔ Design a real database schema <br>
✔ Think like a database engineer <br>

---

Tomorrow (Day 7):

You will:

- Build a **full mini-project**
- Write **25+ real queries**
- Simulate **job-level SQL tasks**
