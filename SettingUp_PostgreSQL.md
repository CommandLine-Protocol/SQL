# SetUp PostgreSQL properly from scratch - including CLI, configuration, Workbench-equivalent tools, and VS Code integration.

We’ll cover:

1. Install & open PostgreSQL (Command Line)
2. Recommended configuration
3. Create a schema using GUI (pgAdmin)
4. Connect PostgreSQL to VS Code
5. Professional setup recommendations

---

# 1️⃣ Install & Open PostgreSQL

Download:

## 🐘 PostgreSQL

Official site:
👉 [https://www.postgresql.org/download/](https://www.postgresql.org/download/)

During installation:

### ✅ Important Settings

- Choose default port: `5432`
- Set a password for user `postgres`
- Install **pgAdmin** when prompted
- Keep locale default unless you need something specific

---

## Open PostgreSQL Command Line (psql)

Postgres CLI tool is called:

```
psql
```

---

### 🪟 On Windows

Open Command Prompt:

```bash
psql -U postgres
```

Enter the password you set.

If command not found, try:

```bash
"C:\Program Files\PostgreSQL\15\bin\psql" -U postgres
```

---

### 🍎 On macOS

```bash
psql -U postgres
```

If needed:

```bash
/Library/PostgreSQL/15/bin/psql -U postgres
```

---

If successful, you'll see:

```sql
postgres=#
```

Now you're connected.

---

# 2️⃣ Recommended PostgreSQL Configuration

Main config file:

- Windows:
  `C:\Program Files\PostgreSQL\15\data\postgresql.conf`

- macOS/Linux:
  `/var/lib/postgresql/15/main/postgresql.conf`

---

## Recommended Settings

Open `postgresql.conf` and adjust:

```conf
port = 5432
max_connections = 200
shared_buffers = 1GB
effective_cache_size = 3GB
```

### Encoding (VERY important)

PostgreSQL default is already good, but ensure your database uses:

```sql
CREATE DATABASE school
WITH ENCODING 'UTF8';
```

Postgres uses UTF-8 by default (good choice).

After config changes → restart PostgreSQL service.

---

# 3️⃣ Create Schema in pgAdmin (GUI)

Postgres equivalent of Workbench:

## 🛠 pgAdmin

Open pgAdmin:

1. Connect to your server
2. Right-click **Databases**
3. Click **Create → Database**
4. Name it `school`
5. Save

---

### Important Concept Difference

In PostgreSQL:

- **Database ≠ Schema**
- A database can contain multiple schemas
- Default schema = `public`

Example:

```sql
CREATE SCHEMA app_schema;
```

Create table inside a schema:

```sql
CREATE TABLE app_schema.students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

---

# 4️⃣ Connect PostgreSQL to VS Code

Install:

## 💻 Visual Studio Code

Install extensions:

- SQLTools
- SQLTools PostgreSQL Driver

---

## Add PostgreSQL Connection

1. Press `Ctrl + Shift + P`
2. Select:

```
SQLTools: Add New Connection
```

3. Choose **PostgreSQL**
4. Enter:

| Setting  | Value                  |
| -------- | ---------------------- |
| Host     | localhost              |
| Port     | 5432                   |
| User     | postgres (or dev user) |
| Password | your_password          |
| Database | school                 |

Click **Test Connection**
Then **Save**

---

# 5️⃣ Write SQL in VS Code

Create:

```
database.sql
```

Example:

```sql
CREATE DATABASE school;

CREATE SCHEMA app;

CREATE TABLE app.students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

Right-click → **Run Query**

---

# 🔥 Professional Setup (Recommended)

Never use `postgres` superuser for development.

Create a developer role:

```sql
CREATE ROLE devuser WITH LOGIN PASSWORD 'strongpassword';

CREATE DATABASE school OWNER devuser;

GRANT ALL PRIVILEGES ON DATABASE school TO devuser;
```

Then connect VS Code using `devuser`.

---

# 📌 Best PostgreSQL Development Settings

✔ UTF-8 encoding
✔ Separate dev user
✔ Use schemas for organization
✔ Use `SERIAL` or `GENERATED AS IDENTITY` for IDs
✔ Avoid working as superuser

---

# 🆚 Key Difference: MySQL vs PostgreSQL

| MySQL             | PostgreSQL                        |
| ----------------- | --------------------------------- |
| Schema = Database | Schema inside Database            |
| AUTO_INCREMENT    | SERIAL / IDENTITY                 |
| utf8mb4 needed    | UTF-8 default                     |
| More permissive   | More strict & standards-compliant |
