# 📘 DBMS & SQL — COMPLETE NOTES (FOUNDATION)

---

## 1️⃣ WHAT IS DBMS (Database Management System)

### Definition

A **DBMS** is software that allows users to:

* Store data
* Retrieve data
* Update data
* Manage data securely and efficiently

### Examples of DBMS

* MySQL
* PostgreSQL
* Oracle
* SQL Server

---

## Why DBMS is Needed (Very Important)

### Problems with File System

* Data redundancy (same data stored many times)
* Data inconsistency
* No security
* Difficult to search
* No multi-user support

### DBMS Solutions

* Centralized data
* Data consistency
* Access control
* Fast retrieval
* Concurrency control

---

## DBMS vs RDBMS

| DBMS                 | RDBMS                     |
| -------------------- | ------------------------- |
| Data stored as files | Data stored as tables     |
| No relationships     | Tables related using keys |
| Less structured      | Highly structured         |
| Example: File system | MySQL, PostgreSQL         |

👉 MySQL is an RDBMS

---

## Basic DBMS Terms (Must Know)

* **Database** → Collection of tables
* **Table** → Collection of rows & columns
* **Row (Record)** → Single entry
* **Column (Field)** → Attribute
* **Schema** → Structure of database

---

## 2️⃣ WHAT IS SQL

### Definition

**SQL (Structured Query Language)** is used to:

* Create databases and tables
* Insert, update, delete data
* Retrieve data
* Control access
* Manage transactions

👉 SQL is not case sensitive, but keywords are written in **UPPERCASE** for readability.

---

## 3️⃣ TYPES OF SQL COMMANDS (VERY IMPORTANT NOTES)

### SQL commands are divided into 5 main categories.

### 1️⃣ DDL – Data Definition Language

**Purpose:** Used to define or change the structure of database objects.

**Commands:**

* CREATE
* ALTER
* DROP
* TRUNCATE
* RENAME

👉 DDL works on structure, not data
👉 DDL commands are auto-commit

---

### 2️⃣ DML – Data Manipulation Language

**Purpose:** Used to manipulate data inside tables.

**Commands:**

* INSERT
* UPDATE
* DELETE
* SELECT

👉 SELECT belongs to DML (interview favorite question)

---

### 3️⃣ DCL – Data Control Language

**Purpose:** Used to control user permissions.

**Commands:**

* GRANT
* REVOKE

---

### 4️⃣ TCL – Transaction Control Language

**Purpose:** Used to manage transactions.

**Commands:**

* COMMIT
* ROLLBACK
* SAVEPOINT

---

### MEMORY TRICK

```
DDL → Structure
DML → Data
DCL → Permission
TCL → Transaction
```

---

# 📘 DDL COMMANDS (Data Definition Language)

## 1️⃣ What is DDL?

DDL commands are used to:

* Define database structure
* Create objects
* Modify objects
* Delete objects

👉 DDL works on **SCHEMA / STRUCTURE**, not on actual data logic.

---

## Key Characteristics of DDL

* Works on database objects
* Changes are permanent
* AUTO-COMMIT
* Cannot be rolled back (generally)

---

## Examples of Database Objects

* Database
* Table
* View
* Index
* Schema

---

## 📌 LIST OF DDL COMMANDS

| Command  | Purpose               |
| -------- | --------------------- |
| CREATE   | Create database/table |
| ALTER    | Modify structure      |
| DROP     | Delete structure      |
| TRUNCATE | Remove all records    |
| RENAME   | Rename table          |

---

# 📘 DBMS & SQL — DDL COMMANDS (README)

---

## 📌 LIST OF DDL COMMANDS

| Command  | Purpose |
|--------|---------|
| CREATE | Create database or table |
| ALTER | Modify table structure |
| DROP | Delete database or table |
| TRUNCATE | Remove all records from a table |
| RENAME | Rename a table (sometimes part of ALTER) |

---

## 2️⃣ CREATE COMMAND

### Purpose
Used to create new database objects.

### CREATE DATABASE

**Syntax**
```sql
CREATE DATABASE database_name;
```

**Example**
```sql
CREATE DATABASE company_db;
```

👉 Creates an empty database.

---

### USE DATABASE  
*(Not a DDL command, but essential)*

**Syntax**
```sql
USE company_db;
```

👉 Selects the database to work on.

---

### CREATE TABLE

**Syntax**
```sql
CREATE TABLE table_name (
  column_name datatype,
  column_name datatype
);
```

**Example**
```sql
CREATE TABLE employees (
  emp_id INT,
  name VARCHAR(50),
  department VARCHAR(50),
  salary INT,
  city VARCHAR(50)
);
```

**Important Points**
- Each column must have a datatype  
- Column names should be meaningful  
- Table name must be unique in the database  

---

## 3️⃣ ALTER COMMAND

### Purpose
Used to modify an existing table structure.

### ALTER – ADD COLUMN

**Syntax**
```sql
ALTER TABLE table_name
ADD column_name datatype;
```

**Example**
```sql
ALTER TABLE employees
ADD email VARCHAR(100);
```

👉 Adds a new column to the table.

---

### ALTER – MODIFY COLUMN

**Syntax**
```sql
ALTER TABLE table_name
MODIFY column_name new_datatype;
```

**Example**
```sql
ALTER TABLE employees
MODIFY salary BIGINT;
```

👉 Changes datatype or size.

---

### ALTER – RENAME COLUMN (MySQL 8+)

```sql
ALTER TABLE employees
RENAME COLUMN city TO location;
```

---

### ALTER – DROP COLUMN

```sql
ALTER TABLE employees
DROP COLUMN email;
```

👉 Deletes a column permanently.

---

### ALTER – RENAME TABLE

```sql
RENAME TABLE employees TO staff;
```

---

## 4️⃣ DROP COMMAND

### Purpose
Used to delete database objects completely.

### DROP TABLE

```sql
DROP TABLE table_name;
```

**Example**
```sql
DROP TABLE employees;
```

👉 Deletes table structure and all data (cannot be recovered).

---

### DROP DATABASE

```sql
DROP DATABASE company_db;
```

⚠️ Dangerous command – deletes everything.

---

## 5️⃣ TRUNCATE COMMAND

### Purpose
Used to delete all rows from a table but keep structure.

```sql
TRUNCATE TABLE table_name;
```

**Example**
```sql
TRUNCATE TABLE employees;
```

### TRUNCATE vs DELETE

| TRUNCATE | DELETE |
|--------|--------|
| DDL command | DML command |
| Deletes all rows | Deletes selected rows |
| Faster | Slower |
| Auto-commit | Can rollback |
| WHERE not allowed | WHERE allowed |

---

## 6️⃣ RENAME COMMAND

```sql
RENAME TABLE old_name TO new_name;
```

**Example**
```sql
RENAME TABLE employees TO employees_data;
```

---

## 📘 50 DDL PRACTICE QUESTIONS

### SECTION A: CREATE DATABASE & TABLE
1. Create a database named `school_db`.  
2. Switch to `school_db`.  
3. Create a table `students (student_id, name, age, city)`.  
4. Create a table `teachers (teacher_id, name, subject`).  
5. Create a table `classes (class_id, class_name)`.  

### SECTION B: ALTER – ADD COLUMN
6. Add `email` column to `students`.  
7. Add `phone` column to `students`.  
8. Add `salary` column to `teachers`.  
9. Add `experience` column to `teachers`.  
10. Add `room_no` column to `classes`.  

### SECTION C: ALTER – MODIFY COLUMN
11. Change datatype of age to `SMALLINT`.  
12. Increase size of name to `VARCHAR(100)`.  
13. Change phone datatype to `VARCHAR(20)`.  
14. Change salary datatype to `BIGINT`.  
15. Increase subject size to `VARCHAR(100)`.  

### SECTION D: ALTER – RENAME COLUMN
16. Rename `city` to `location` in students.  
17. Rename `name` to `student_name` in students.  
18. Rename `name` to `teacher_name` in teachers.  
19. Rename `room_no` to `room_number` in classes.  
20. Rename `experience` to `years_of_experience`.  

### SECTION E: ALTER – DROP COLUMN
21. Drop email from `students`.  
22. Drop phone from `students`.  
23. Drop salary from `teachers`.  
24. Drop room_number from `classes`.  
25. Drop years_of_experience from `teachers`.  

### SECTION F: RENAME TABLE
26. Rename `students` to `school_students`.  
27. Rename `teachers` to `school_teachers`.  
28. Rename `classes` to `school_classes`.  
29. Rename `school_students` to `students_info`.  
30. Rename `school_teachers` to `teachers_info`.  

### SECTION G: TRUNCATE TABLE
31. Remove all records from `students_info`.  
32. Truncate `teachers_info`.  
33. Truncate `school_classes`.  
34. Truncate `students_info` again.  
35. Truncate `teachers_info` again.  

### SECTION H: DROP TABLE
36. Drop `students_info`.  
37. Drop `teachers_info`.  
38. Drop `school_classes`.  
39. Drop `classes` if exists.  
40. Drop `students` if exists.  

### SECTION I: DROP DATABASE
41. Drop `school_db`.  
42. Create `office_db`.  
43. Drop `office_db`.  
44. Create `test_db`.  
45. Drop `test_db`.  

### SECTION J: INTERVIEW / THINKING
46. Delete only table structure but keep database.  
47. Delete all records but keep table structure.  
48. Identify which is faster: DELETE or TRUNCATE.  
49. Identify which DDL command cannot be rolled back.  
50. Permanently delete a database.  

---

## 7️⃣ DDL SUMMARY

- DDL commands define or change structure  
- DDL is auto-commit  
- DDL cannot be rolled back  
- DDL works on schema  
