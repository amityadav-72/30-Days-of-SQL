## 📌 Quick Navigation

- [JOIN Theory](#-join-in-dbms--complete-theory)
- [INNER JOIN Complete Guide](#-inner-join-in-dbms----complete-guide)


# 🔗 JOIN in DBMS – Complete Theory


## 📌 What is a JOIN?

A **JOIN** is a SQL operation used to combine rows from two or more tables based on a related column (usually a key).

It helps in:

- Fetching data stored in multiple tables  
- Maintaining normalization  
- Avoiding data redundancy  

👉 JOIN works on a **logical relationship between tables**.

---

## 🧠 Why do we need JOIN?

In a relational database:

- Data is stored in multiple tables.
- To get meaningful information, we combine them.

### Example:

- **Students table** → student details  
- **Marks table** → student marks  

To see **name + marks together → JOIN is required**

---

# 🔑 Types of JOIN

## 1️⃣ Based on Matching

### ✅ INNER JOIN

- Returns only **matching rows** from both tables  
- Non-matching rows are discarded  
- Most commonly used join  

📍 **Think:** Intersection

---

### ✅ OUTER JOIN

Used when we also want **non-matching data**

#### 🔹 LEFT OUTER JOIN

- All records from **left table**
- Matching records from right
- If no match → `NULL`

📍 **Think:** Left table is priority

#### 🔹 RIGHT OUTER JOIN

- All records from **right table**
- Matching from left
- If no match → `NULL`

📍 **Think:** Right table is priority

#### 🔹 FULL OUTER JOIN

- All rows from **both tables**
- Matching where possible
- Non-matching → `NULL`

📍 **Think:** Union of both tables

---

## 2️⃣ Based on Condition

### ✅ EQUI JOIN

- Join condition uses `=`
- Most common type

---

### ✅ NON-EQUI JOIN

Join condition uses:

- `<`
- `>`
- `BETWEEN`
- `!=`

📌 Used in **range matching**

**Example:**  
Salary table joined with grade table.

---

### ✅ SELF JOIN

- A table joined with itself
- Used when data in the same table is related

**Example:**  
Employee → Manager (both in same table)

---

### ✅ CROSS JOIN

- No condition
- Produces **Cartesian product**

📍 Rows = **m × n**

---

# 🔗 JOIN vs SET OPERATIONS

| JOIN | UNION |
|------|------|
| Combines columns | Combines rows |
| Works on related tables | Works on same structure tables |
| Uses condition | No condition |

---

# 🔑 Keys Used in JOIN

### 1️⃣ Primary Key
- Unique identifier in one table

### 2️⃣ Foreign Key
- Column that references primary key in another table

👉 JOIN is usually performed on:

```sql
Primary Key = Foreign Key
```
--------------------------------
## ⚙️ How JOIN Works Internally

DBMS uses the following algorithms to execute JOIN efficiently:

- **Nested Loop Join**
- **Hash Join**
- **Merge Join**

👉 These are used for **query optimization** and improving performance.

---

## 🎯 Real-Life Use Cases

JOIN is widely used in:

- Banking systems  
- E-commerce order management  
- Social media platforms  
- College management systems  
- Human resource management systems  

---

## 🧩 Visual Understanding

Think of two circles (tables):

- **INNER JOIN →** Common area  
- **LEFT JOIN →** Full left circle  
- **RIGHT JOIN →** Full right circle  
- **FULL JOIN →** Both circles  

---

## ⭐ Advantages of JOIN

✔ Retrieves meaningful data  
✔ Reduces data redundancy  
✔ Maintains normalization  
✔ Faster than multiple separate queries  

---

## ⚠️ Disadvantages

❌ Complex for very large tables  
❌ Performance cost if indexing is not proper  
❌ Wrong JOIN condition can produce duplicate data  

---

## 🏁 Summary

JOIN is a powerful SQL operation that:

- Combines data from multiple tables  
- Uses relationships between keys  
- Helps in building real-world applications efficiently

  -----------------------------------


 # 🔗 INNER JOIN in DBMS -- Complete Guide

## 🎯 Example Tables

<table>
<tr>
<td>

### 🧑‍🎓 students

| student_id | name |
|------------|------|
| 1 | Amit |
| 2 | Neha |

</td>
<td>

### 📚 courses

| course_id | course_name |
|-----------|-------------|
| 101 | SQL |
| 102 | Java |

</td>
<td>

### 📝 enrollments

| student_id | course_id |
|------------|-----------|
| 1 | 101 |
| 2 | 102 |

</td>
</tr>
</table>

### ❓ Requirement

👉 Show **student name + course name**

Data is stored in **3 tables → JOIN is required**

------------------------------------------------------------------------

# 🧠 1. WHAT IS INNER JOIN?

## ✅ Definition

**INNER JOIN** returns only the **matching rows from both tables**.

✔ Common data between tables

------------------------------------------------------------------------

## 🧩 Visual Understanding

## 🧩 Visual Understanding

| Table A | Table B |
|--------|--------|
| 1 | 2 |
| 2 | 3 |
| 3 | 4 |

**INNER JOIN Result:** → 2, 3  

Only **common values** are returned.

------------------------------------------------------------------------

# 🧠 2. INNER JOIN SYNTAX

## ✅ Basic Syntax

``` sql
SELECT column_list
FROM table1
INNER JOIN table2
ON table1.common_column = table2.common_column;
```

## ✅ Using Alias (Best Practice)

``` sql
SELECT s.name, c.course_name
FROM students s
INNER JOIN enrollments e
ON s.student_id = e.student_id
INNER JOIN courses c
ON e.course_id = c.course_id;
```

------------------------------------------------------------------------

# 🧠 3. Step-by-Step Execution

1️⃣ Take first table
2️⃣ Take second table
3️⃣ Compare ON condition
4️⃣ Return only matching rows

------------------------------------------------------------------------

# 🧠 4. Single INNER JOIN -- Full Example

## 🎯 Example Tables

### 🏢 departments

| dept_id | dept_name |
|---------|-----------|
| 1 | HR |
| 2 | IT |

---

### 👨‍💼 employees

| emp_id | emp_name | dept_id |
|--------|----------|---------|
| 101 | Amit | 1 |
| 102 | Neha | 2 |
| 103 | Raj | 5 |

### ✅ Query

``` sql
SELECT emp_name, dept_name
FROM employees
INNER JOIN departments
ON employees.dept_id = departments.dept_id;
```

### ✅ Result

## 📊 INNER JOIN Output

| emp_name | dept_name |
|----------|-----------|
| Amit | HR |
| Neha | IT |

❗ Raj is not shown because there is no matching department.

------------------------------------------------------------------------

# 🧠 5. INNER JOIN with SELECT \*

``` sql
SELECT *
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id;
```

❗ Use table aliases to avoid ambiguity:
```
    e.dept_id
    d.dept_id
```
------------------------------------------------------------------------

# 🧠 6. Filtering with INNER JOIN

``` sql
SELECT emp_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id
WHERE d.dept_name = 'IT';
```

### 🔥 Execution Order

1️⃣ FROM
2️⃣ JOIN
3️⃣ ON
4️⃣ WHERE
5️⃣ SELECT

------------------------------------------------------------------------

# 🧠 7. INNER JOIN on Different Column Names

``` sql
SELECT name, order_id
FROM orders o
INNER JOIN customers c
ON o.customer_id = c.id;
```

------------------------------------------------------------------------

# 🧠 8. INNER JOIN using USING()

``` sql
SELECT *
FROM employees
INNER JOIN departments
USING (dept_id);
```

## 🔍 Difference Between USING and ON

| USING | ON |
|-------|----|
Removes duplicate column | Shows both columns |

------------------------------------------------------------------------

# 🧠 9. Multiple INNER JOIN

``` sql
SELECT s.name, c.course_name
FROM students s
INNER JOIN enrollments e
ON s.student_id = e.student_id
INNER JOIN courses c
ON e.course_id = c.course_id;
```

### 🔄 Execution Flow

1️⃣ students + enrollments
2️⃣ Result joins with courses

------------------------------------------------------------------------

# 🧠 10. INNER JOIN + AGGREGATION

``` sql
SELECT d.dept_name, COUNT(*) AS total
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id
GROUP BY d.dept_name;
```

------------------------------------------------------------------------

# 🧠 11. INNER JOIN + ORDER BY

The `ORDER BY` clause is used to **sort the final result set** after the JOIN operation is completed.

### ✅ Example

```
SELECT e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id
ORDER BY d.dept_name;
```

### 🔍 Explanation

- First, the JOIN is performed.

- The matching rows are produced.

- Then the result is sorted based on `dept_name`.

  📌 Key Point

- `ORDER BY` is always executed at the end.

------------------------------------------------------------------------

## 🧠 12. INNER JOIN vs WHERE JOIN (Old Style)

### ❌ Old Style (Implicit Join)

``` sql
SELECT emp_name, dept_name
FROM employees, departments
WHERE employees.dept_id = departments.dept_id;
```

### ⚠ Problems with Old Style

-   Join condition and filtering condition are mixed together
-   Harder to read and maintain
-   Easy to forget the join condition → causes **Cartesian product**
-   Not recommended in modern SQL

------------------------------------------------------------------------

### ✅ Modern Style (Explicit Join)

``` sql
SELECT emp_name, dept_name
FROM employees
INNER JOIN departments
ON employees.dept_id = departments.dept_id;
```

### ⭐ Advantages

-   Clear separation of JOIN condition and filtering condition
-   More readable and structured
-   Easier debugging
-   Industry standard
-   Supports multiple joins in a clean way

------------------------------------------------------------------------

## 🧠 13. Most Common Interview Mistakes

### ❌ 1. Missing ON Condition

``` sql
SELECT *
FROM employees
INNER JOIN departments;
```

### 🚨 Result

Produces a **Cartesian product**

If:

-   employees = 3 rows
-   departments = 2 rows

Result → **3 × 2 = 6 rows**

------------------------------------------------------------------------

### ❌ 2. Joining on Wrong Column

``` sql
ON employees.emp_id = departments.dept_id
```

### 🚨 Problem

-   Incorrect output
-   Sometimes empty result
-   Logical data mismatch

------------------------------------------------------------------------

### ❌ 3. Filtering in ON vs WHERE Confusion

✔ **ON** → Used for matching rows between tables
✔ **WHERE** → Used for filtering the final result

#### ✅ Correct Example

``` sql
SELECT e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id
WHERE d.dept_name = 'IT';
```

------------------------------------------------------------------------

### ❌ 4. Not Using Aliases

#### Without alias

``` sql
SELECT employees.emp_name, departments.dept_name
FROM employees
INNER JOIN departments
ON employees.dept_id = departments.dept_id;
```

#### ✅ With alias (Recommended)

``` sql
SELECT e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id;
```

### ⭐ Why Alias?

-   Shorter query
-   Better readability
-   Required when column names are same
-   Cleaner for multiple joins

------------------------------------------------------------------------

## 🧠 14. Performance Note

### 🚀 Why INNER JOIN is Faster

-   Returns only matching rows
-   Less data processing than OUTER JOIN
-   Optimizer can use indexes efficiently

------------------------------------------------------------------------

### 📌 Role of Indexing

Creating an index on the join column improves performance.

``` sql
CREATE INDEX idx_dept_id
ON employees(dept_id);
```

------------------------------------------------------------------------

### 🔥 Benefits of Indexing

-   Faster row matching
-   Reduced full table scan
-   Better execution plan
-   Improved query response time

------------------------------------------------------------------------

### ⚙ Without Index

-   Full table scan
-   High I/O cost
-   Slow for large datasets

------------------------------------------------------------------------

### ⚙ With Index

-   Direct lookup using index
-   Minimal scanning
-   Much faster JOIN

------------------------------------------------------------------------

## 🧠 Query Execution Optimization

DBMS may internally use:

-   **Nested Loop Join** → Best for small tables or indexed columns
-   **Hash Join** → Best for large tables without indexes
-   **Merge Join** → Best for sorted and indexed data

### 📌 Selection Depends On:

-   Table size
-   Index availability
-   Memory availability
-   Data distribution
-   Database optimizer

------------------------------------------------------------------------

## 🏁 Quick Interview Revision

-   Always use explicit INNER JOIN
-   Never forget the ON condition
-   Use aliases for readability
-   Index join columns for performance
-   ON → matching, WHERE → filtering


# 🧱 Practice Database Schema (SQL)

Use the following tables to practice SQL queries like JOINs, GROUP BY, Subqueries, etc.

---

## 👨‍💼 Employees Table

```sql
CREATE TABLE Employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(50),
    dept_id INT,
    salary INT,
    manager_id INT
);
```

---

## 🏢 Departments Table

```sql
CREATE TABLE Departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50),
    location VARCHAR(50)
);
```

---

## 📦 Orders Table

```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    amount INT
);
```

---

## 👤 Customers Table

```sql
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(50),
    city VARCHAR(50)
);
```

---

## 📚 Courses Table

```sql
CREATE TABLE Courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50),
    instructor VARCHAR(50)
);
```

---

## 🎓 Students Table

```sql
CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    course_id INT
);
```

# 📊 Sample Data for SQL Practice

This dataset is designed for practicing SQL concepts like JOINs, GROUP BY, Subqueries, etc.

---

## 🧱 1. Employees Data

```sql
INSERT INTO Employees VALUES
(1, 'Amit', 1, 60000, NULL),
(2, 'Rahul', 2, 50000, 1),
(3, 'Sneha', 1, 70000, 1),
(4, 'Priya', 3, 45000, 2),
(5, 'Karan', 2, 80000, 1),
(6, 'Neha', 3, 55000, 2),
(7, 'Arjun', 1, 90000, 3),
(8, 'Riya', 2, 40000, 5);
```

---

## 🏢 2. Departments Data

```sql
INSERT INTO Departments VALUES
(1, 'IT', 'Mumbai'),
(2, 'HR', 'Delhi'),
(3, 'Finance', 'Pune'),
(4, 'Marketing', 'Bangalore');
```

---

## 👤 3. Customers Data

```sql
INSERT INTO Customers VALUES
(1, 'Rohit', 'Mumbai'),
(2, 'Anjali', 'Delhi'),
(3, 'Vikas', 'Pune'),
(4, 'Simran', 'Mumbai'),
(5, 'Aman', 'Bangalore');
```

---

## 📦 4. Orders Data

```sql
INSERT INTO Orders VALUES
(101, 1, '2024-01-10', 5000),
(102, 2, '2024-01-12', 7000),
(103, 1, '2024-02-01', 3000),
(104, 3, '2024-02-10', 9000),
(105, 4, '2024-03-05', 4000),
(106, 2, '2024-03-10', 6000),
(107, 1, '2024-03-15', 8000),
(108, 5, '2024-04-01', 10000);
```

---

## 🎓 5. Courses Data

```sql
INSERT INTO Courses VALUES
(1, 'Java', 'Mr. Sharma'),
(2, 'Python', 'Ms. Gupta'),
(3, 'SQL', 'Mr. Khan'),
(4, 'Web Dev', 'Ms. Mehta');
```

---

## 📚 6. Students Data

```sql
INSERT INTO Students VALUES
(1, 'Aman', 1),
(2, 'Riya', 2),
(3, 'Sohan', 3),
(4, 'Neha', 1),
(5, 'Kunal', 2),
(6, 'Pooja', 3),
(7, 'Ankit', 4),
(8, 'Simran', 1);
```

---

## 🔥 Practice Example

### 👉 Get employee name + department name

```sql
SELECT e.name, d.dept_name
FROM Employees e
INNER JOIN Departments d
ON e.dept_id = d.dept_id;
```

# 🧠 SQL INNER JOIN Practice Questions (Basic → Advanced)

Practice these questions using the given schema and data.

---

## 🔰 BASIC INNER JOIN QUESTIONS (1–15)

1. Get employee names with their department names
2. Show all employees and their department locations
3. List students with their course names
4. Get customer names and their order amounts
5. Show employees working in “IT” department
6. Get all orders with customer names
7. List employees with salary > 50,000 and department name
8. Show students enrolled in “Java” course
9. Get employees and their managers (self join)
10. Show departments with employee names
11. Find employees in Mumbai location departments
12. Get all customers who placed orders
13. Show orders placed after 2024 with customer name
14. List employees with department id = 2
15. Get course names with student names

---

## ⚙️ INTERMEDIATE QUESTIONS (16–35)

16. Count employees in each department
17. Find total salary per department
18. Get highest salary employee in each department
19. Show customers with total order amount
20. Find departments with more than 3 employees
21. Get average salary per department
22. List employees whose salary > department average
23. Show customers who placed more than 2 orders
24. Get latest order per customer
25. Find students count per course
26. Get department with highest total salary
27. Show employees and their manager names
28. Find employees who have same manager
29. Get customers from same city with orders
30. Find departments where avg salary > 60k
31. Get top 3 highest paid employees with department
32. Show employees not in HR department
33. Find courses with more than 5 students
34. Get customers who spent more than 10,000
35. Show employee + department sorted by salary

---

## 🚀 ADVANCED QUESTIONS (36–50)

36. Find second highest salary in each department
37. Get employees earning more than their manager
38. Show department-wise rank of employees by salary
39. Find duplicate salary employees within same department
40. Get employees who joined same dept as their manager
41. Find customers who never ordered (Hint: LEFT JOIN comparison)
42. Get running total of orders per customer
43. Show top spending customer per city
44. Find employees working in same department & location
45. Get employees whose salary is top 10% in department
46. Find departments where all employees earn > 50k
47. Get employees with no manager (using join logic)
48. Show gap between employee salary and department avg
49. Get most popular course (max students)
50. Find customers who ordered on consecutive days

---



