# Example syntax for 100 SQL commands/functions

Examples use standard SQL where possible (some are vendor-specific and noted).

---

# 🔹 1. Data Query Language (DQL)

1. **SELECT**

```sql
SELECT name, age FROM users;
```

2. **SELECT DISTINCT**

```sql
SELECT DISTINCT country FROM customers;
```

3. **FROM**

```sql
SELECT * FROM orders;
```

4. **WHERE**

```sql
SELECT * FROM users WHERE age > 18;
```

5. **GROUP BY**

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

6. **HAVING**

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

7. **ORDER BY**

```sql
SELECT * FROM products ORDER BY price DESC;
```

8. **LIMIT** (MySQL/PostgreSQL)

```sql
SELECT * FROM users LIMIT 10;
```

9. **OFFSET**

```sql
SELECT * FROM users LIMIT 10 OFFSET 20;
```

10. **FETCH FIRST** (ANSI SQL)

```sql
SELECT * FROM users FETCH FIRST 10 ROWS ONLY;
```

---

# 🔹 2. Data Manipulation Language (DML)

11. **INSERT**

```sql
INSERT INTO users (name, age) VALUES ('John', 25);
```

12. **INSERT INTO SELECT**

```sql
INSERT INTO archive_users (name, age)
SELECT name, age FROM users WHERE active = 0;
```

13. **UPDATE**

```sql
UPDATE users SET age = 26 WHERE name = 'John';
```

14. **DELETE**

```sql
DELETE FROM users WHERE age < 18;
```

15. **TRUNCATE**

```sql
TRUNCATE TABLE logs;
```

16. **MERGE** (SQL Server/Oracle)

```sql
MERGE INTO target t
USING source s
ON (t.id = s.id)
WHEN MATCHED THEN UPDATE SET t.name = s.name
WHEN NOT MATCHED THEN INSERT (id, name) VALUES (s.id, s.name);
```

17. **REPLACE** (MySQL)

```sql
REPLACE INTO users (id, name) VALUES (1, 'Alice');
```

18. **UPSERT** (PostgreSQL)

```sql
INSERT INTO users (id, name)
VALUES (1, 'Alice')
ON CONFLICT (id)
DO UPDATE SET name = EXCLUDED.name;
```

19. **CALL**

```sql
CALL GetUserStats();
```

20. **EXPLAIN**

```sql
EXPLAIN SELECT * FROM users WHERE id = 1;
```

---

# 🔹 3. Data Definition Language (DDL)

21. **CREATE DATABASE**

```sql
CREATE DATABASE company_db;
```

22. **DROP DATABASE**

```sql
DROP DATABASE company_db;
```

23. **ALTER DATABASE**

```sql
ALTER DATABASE company_db SET READ_ONLY = 1;
```

24. **CREATE TABLE**

```sql
CREATE TABLE users (
  id INT PRIMARY KEY,
  name VARCHAR(100),
  age INT
);
```

25. **DROP TABLE**

```sql
DROP TABLE users;
```

26. **ALTER TABLE**

```sql
ALTER TABLE users ADD email VARCHAR(100);
```

27. **RENAME TABLE** (MySQL)

```sql
RENAME TABLE users TO customers;
```

28. **CREATE INDEX**

```sql
CREATE INDEX idx_name ON users(name);
```

29. **DROP INDEX**

```sql
DROP INDEX idx_name ON users;
```

30. **CREATE VIEW**

```sql
CREATE VIEW active_users AS
SELECT * FROM users WHERE active = 1;
```

31. **DROP VIEW**

```sql
DROP VIEW active_users;
```

32. **CREATE SEQUENCE**

```sql
CREATE SEQUENCE order_seq START WITH 1 INCREMENT BY 1;
```

33. **DROP SEQUENCE**

```sql
DROP SEQUENCE order_seq;
```

34. **CREATE TRIGGER**

```sql
CREATE TRIGGER before_insert_users
BEFORE INSERT ON users
FOR EACH ROW
SET NEW.created_at = NOW();
```

35. **DROP TRIGGER**

```sql
DROP TRIGGER before_insert_users;
```

36. **CREATE FUNCTION**

```sql
CREATE FUNCTION get_age(birthdate DATE)
RETURNS INT
RETURN YEAR(CURDATE()) - YEAR(birthdate);
```

37. **DROP FUNCTION**

```sql
DROP FUNCTION get_age;
```

38. **CREATE PROCEDURE**

```sql
CREATE PROCEDURE GetUsers()
BEGIN
  SELECT * FROM users;
END;
```

39. **DROP PROCEDURE**

```sql
DROP PROCEDURE GetUsers;
```

40. **COMMENT**

```sql
COMMENT ON TABLE users IS 'Stores user information';
```

---

# 🔹 4. Constraints

41. **PRIMARY KEY**

```sql
id INT PRIMARY KEY
```

42. **FOREIGN KEY**

```sql
FOREIGN KEY (user_id) REFERENCES users(id)
```

43. **UNIQUE**

```sql
email VARCHAR(100) UNIQUE
```

44. **NOT NULL**

```sql
name VARCHAR(100) NOT NULL
```

45. **CHECK**

```sql
age INT CHECK (age >= 18)
```

46. **DEFAULT**

```sql
status VARCHAR(20) DEFAULT 'active'
```

47. **AUTO_INCREMENT** (MySQL)

```sql
id INT AUTO_INCREMENT PRIMARY KEY
```

48. **IDENTITY** (SQL Server)

```sql
id INT IDENTITY(1,1) PRIMARY KEY
```

49. **ON DELETE CASCADE**

```sql
FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
```

50. **ON UPDATE CASCADE**

```sql
FOREIGN KEY (user_id) REFERENCES users(id) ON UPDATE CASCADE
```

---

# 🔹 5–10 (Condensed for readability)

Below are concise syntax examples.

---

### Joins

51. **INNER JOIN**

```sql
SELECT * FROM orders
INNER JOIN users ON orders.user_id = users.id;
```

52. **LEFT JOIN**

```sql
SELECT * FROM users
LEFT JOIN orders ON users.id = orders.user_id;
```

53. **RIGHT JOIN**

```sql
SELECT * FROM users
RIGHT JOIN orders ON users.id = orders.user_id;
```

54. **FULL JOIN**

```sql
SELECT * FROM users
FULL JOIN orders ON users.id = orders.user_id;
```

55. **CROSS JOIN**

```sql
SELECT * FROM users CROSS JOIN roles;
```

---

### Aggregate Functions

56. **COUNT()**

```sql
SELECT COUNT(*) FROM users;
```

57. **SUM()**

```sql
SELECT SUM(price) FROM orders;
```

58. **AVG()**

```sql
SELECT AVG(price) FROM orders;
```

59. **MIN()**

```sql
SELECT MIN(price) FROM products;
```

60. **MAX()**

```sql
SELECT MAX(price) FROM products;
```

---

### String Functions

61. **CONCAT()**

```sql
SELECT CONCAT(first_name, ' ', last_name) FROM users;
```

62. **SUBSTRING()**

```sql
SELECT SUBSTRING(name, 1, 3) FROM users;
```

63. **UPPER()**

```sql
SELECT UPPER(name) FROM users;
```

64. **LOWER()**

```sql
SELECT LOWER(name) FROM users;
```

65. **TRIM()**

```sql
SELECT TRIM(name) FROM users;
```

---

### Date Functions

66. **NOW()**

```sql
SELECT NOW();
```

67. **CURRENT_DATE**

```sql
SELECT CURRENT_DATE;
```

68. **DATE_ADD()**

```sql
SELECT DATE_ADD(NOW(), INTERVAL 7 DAY);
```

69. **DATEDIFF()**

```sql
SELECT DATEDIFF('2025-12-31', '2025-01-01');
```

70. **EXTRACT()**

```sql
SELECT EXTRACT(YEAR FROM NOW());
```

---

### Transactions

71. **BEGIN TRANSACTION**

```sql
BEGIN TRANSACTION;
```

72. **COMMIT**

```sql
COMMIT;
```

73. **ROLLBACK**

```sql
ROLLBACK;
```

74. **SAVEPOINT**

```sql
SAVEPOINT before_update;
```

75. **SET TRANSACTION**

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

---

### Security

76. **GRANT**

```sql
GRANT SELECT ON users TO user1;
```

77. **REVOKE**

```sql
REVOKE SELECT ON users FROM user1;
```

78. **CREATE USER**

```sql
CREATE USER user1 IDENTIFIED BY 'password';
```

79. **DROP USER**

```sql
DROP USER user1;
```

80. **ALTER USER**

```sql
ALTER USER user1 IDENTIFIED BY 'newpassword';
```

---

# 🔹 Additional Date & Time Functions (continued)

81. **CURRENT_TIME**

```sql
SELECT CURRENT_TIME;
```

82. **YEAR()**

```sql
SELECT YEAR(order_date) FROM orders;
```

83. **MONTH()**

```sql
SELECT MONTH(order_date) FROM orders;
```

84. **DAY()**

```sql
SELECT DAY(order_date) FROM orders;
```

85. **DATE_SUB()**

```sql
SELECT DATE_SUB(NOW(), INTERVAL 30 DAY);
```

86. **TIME()**

```sql
SELECT TIME(NOW());
```

87. **HOUR()**

```sql
SELECT HOUR(order_time) FROM orders;
```

88. **MINUTE()**

```sql
SELECT MINUTE(order_time) FROM orders;
```

89. **SECOND()**

```sql
SELECT SECOND(order_time) FROM orders;
```

90. **CURRENT_TIMESTAMP**

```sql
SELECT CURRENT_TIMESTAMP;
```

---

# 🔹 Additional Transaction & Control Statements

91. **SET AUTOCOMMIT** (MySQL)

```sql
SET AUTOCOMMIT = 0;
```

92. **LOCK TABLE**

```sql
LOCK TABLE users WRITE;
```

93. **UNLOCK TABLES**

```sql
UNLOCK TABLES;
```

94. **SET CONSTRAINTS** (PostgreSQL)

```sql
SET CONSTRAINTS ALL DEFERRED;
```

95. **ROLLBACK TO SAVEPOINT**

```sql
ROLLBACK TO SAVEPOINT before_update;
```

---

# 🔹 Additional Administrative / Utility Commands

96. **SHOW TABLES** (MySQL)

```sql
SHOW TABLES;
```

97. **SHOW DATABASES** (MySQL)

```sql
SHOW DATABASES;
```

98. **DESCRIBE** (MySQL)

```sql
DESCRIBE users;
```

99. **ANALYZE TABLE**

```sql
ANALYZE TABLE users;
```

100. **VACUUM** (PostgreSQL)

```sql
VACUUM;
```

---

⚠️ Note: Some commands vary slightly between **MySQL, PostgreSQL, SQL Server, and Oracle**.
