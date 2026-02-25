#Setting up MySQL properly from scratch, then connect it to **VS Code** so you can work like a developer.

We’ll go in this order:

1. Install & open MySQL (Command Line)
2. Set up MySQL properly (recommended configuration)
3. Create a schema in MySQL Workbench
4. Connect MySQL to VS Code
5. Write and run SQL from VS Code

---

# 1️⃣ Install & Open MySQL Command Line

## Install MySQL

Download **MySQL Community Server**:

👉 [https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/)

During installation:

### ✅ Important Settings

- Choose **Developer Default**
- Set a **root password** (SAVE THIS)
- Keep default port: `3306`
- Leave authentication as default (recommended)

---

## Open MySQL Command Line

### On Windows

- Press `Win + R`
- Type:

```bash
cmd
```

Then connect:

```bash
mysql -u root -p
```

Enter your root password.

---

### On macOS

Open Terminal:

```bash
mysql -u root -p
```

If command not found:

```bash
/usr/local/mysql/bin/mysql -u root -p
```

---

If successful, you’ll see:

```sql
mysql>
```

Now you're inside MySQL.

---

# 2️⃣ Recommended MySQL Configuration

Configuration file:

- Windows: `C:\ProgramData\MySQL\MySQL Server 8.0\my.ini`
- macOS/Linux: `/etc/my.cnf`

### Recommended Settings

```ini
[mysqld]
port=3306
max_connections=200
innodb_buffer_pool_size=1G
character-set-server=utf8mb4
collation-server=utf8mb4_unicode_ci
```

### Why?

- `utf8mb4` → supports full Unicode
- `innodb_buffer_pool_size` → improves performance
- `max_connections` → allows more users

After editing → restart MySQL service.

---

# 3️⃣ Create Schema in MySQL Workbench

Install:

## 🛠 MySQL Workbench

Open Workbench:

### Steps:

1. Click your local MySQL connection
2. On left panel → right-click **Schemas**
3. Click **Create Schema**
4. Name it (example: `school`)
5. Choose:
   - Charset: `utf8mb4`
   - Collation: `utf8mb4_unicode_ci`

6. Click **Apply**

To verify:

```sql
SHOW DATABASES;
```

---

# 4️⃣ Connect MySQL to VS Code (Recommended Setup)

Install:

## 💻 Visual Studio Code

Then install extensions:

- SQLTools
- SQLTools MySQL/MariaDB Driver

---

## Configure Connection in VS Code

1. Open VS Code
2. Press `Ctrl + Shift + P`
3. Type:

```
SQLTools: Add New Connection
```

4. Choose **MySQL**
5. Enter:

| Setting  | Value                   |
| -------- | ----------------------- |
| Host     | localhost               |
| Port     | 3306                    |
| User     | root                    |
| Password | your_password           |
| Database | school (or leave empty) |

Click **Test Connection**
Then **Save**

---

# 5️⃣ Write SQL in VS Code

Create a file:

```
database.sql
```

Example:

```sql
CREATE DATABASE school;
USE school;

CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    age INT
);
```

Right-click → **Run Query**

---

# 🔥 Professional Setup Recommendation

For real development, don’t use root.

Instead create a developer user:

```sql
CREATE USER 'devuser'@'localhost' IDENTIFIED BY 'strongpassword';
GRANT ALL PRIVILEGES ON school.* TO 'devuser'@'localhost';
FLUSH PRIVILEGES;
```

Then connect VS Code using `devuser`.

---

# 📌 Final Recommended Setup Summary

✔ MySQL Server installed
✔ utf8mb4 enabled
✔ MySQL Workbench for visual management
✔ VS Code + SQLTools for coding
✔ Separate developer user (not root)
