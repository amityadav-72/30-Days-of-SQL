# 🧠 SQL Joins --- FULL OUTER JOIN & SELF JOIN

------------------------------------------------------------------------

# 🔷 PART 1 --- FULL OUTER JOIN

## 🧠 1. What is FULL JOIN?

### ✅ Definition

**FULL OUTER JOIN returns:**

✔ All rows from the LEFT table
✔ All rows from the RIGHT table
✔ Matched rows from both tables
❌ Non-matching rows → `NULL` on the missing side

------------------------------------------------------------------------

## 🧠 2. Visual Representation

  ## 🧠 FULL JOIN — Visual Tables

### 🔹 Source Tables

### Table A

| id |
|----|
| 1  |
| 2  |
| 3  |

### Table B

| id |
|----|
| 2  |
| 3  |
| 4  |

### FULL OUTER JOIN Result

| A.id | B.id |
|------|------|
| 1    | NULL |
| 2    | 2    |
| 3    | 3    |
| NULL | 4    |

---

### 🔹 Single Column Representation

| Result |
|--------|
| 1      |
| 2      |
| 3      |
| 4      |

| Situation        | Result               |
|------------------|----------------------|
| Matched rows     | Normal data          |
| Unmatched LEFT   | NULL on RIGHT side   |
| Unmatched RIGHT  | NULL on LEFT side    |

------------------------------------------------------------------------

## ❗ MySQL Important Note

MySQL **does NOT support FULL OUTER JOIN directly**

### ✅ Workaround using UNION

``` sql
SELECT ...
FROM A
LEFT JOIN B ON condition

UNION

SELECT ...
FROM A
RIGHT JOIN B ON condition;
```

------------------------------------------------------------------------

## 🧪 3. Example Data

### 🎓 students

| id | name  |
|----|-------|
| 1  | Amit  |
| 2  | Neha  |
| 3  | Rahul |

---

### 📚 enrollments

| student_id | course |
|------------|--------|
| 2          | SQL    |
| 3          | Java   |
| 4          | Python |


------------------------------------------------------------------------

## 🧪 4. FULL JOIN Query (MySQL)

``` sql
SELECT s.id, s.name, e.course
FROM students s
LEFT JOIN enrollments e
ON s.id = e.student_id

UNION

SELECT s.id, s.name, e.course
FROM students s
RIGHT JOIN enrollments e
ON s.id = e.student_id;
```

------------------------------------------------------------------------

## 🧠 5. Result


| id   | name  | course |
|------|-------|--------|
| 1    | Amit  | NULL   |
| 2    | Neha  | SQL    |
| 3    | Rahul | Java   |
| NULL | NULL  | Python |

------------------------------------------------------------------------

## 🧠 6. Explanation

✔ Amit → exists only in **students**
✔ Python → exists only in **enrollments**
✔ Neha & Rahul → matched in both

➡️ **FULL JOIN = Everything from both tables**

------------------------------------------------------------------------

## 🎯 7. When Do We Use FULL JOIN?

### Real-World Use Cases

✅ Find unmatched data from both tables
✅ Data reconciliation
✅ Compare two tables
✅ Detect missing records
✅ Audit / migration validation

------------------------------------------------------------------------

## 🎤 8. Interview Question

### Find non-matching rows from both tables

``` sql
SELECT s.id, e.student_id
FROM students s
LEFT JOIN enrollments e
ON s.id = e.student_id
WHERE e.student_id IS NULL

UNION

SELECT s.id, e.student_id
FROM students s
RIGHT JOIN enrollments e
ON s.id = e.student_id
WHERE s.id IS NULL;
```

------------------------------------------------------------------------

# 🔷 PART 2 --- SELF JOIN

------------------------------------------------------------------------

## 🧠 9. What is SELF JOIN?

A **SELF JOIN** is when a table is joined with itself.

### Used when:

The table has a **relationship within itself**.

------------------------------------------------------------------------

## 🧪 10. Example --- Employees Table

### 👨‍💼 employees

| emp_id | name   | manager_id |
|--------|--------|------------|
| 101    | Raj    | NULL       |
| 102    | Simran | 101        |
| 103    | Arjun  | 101        |

------------------------------------------------------------------------

## 🎯 Goal

Employee → Manager

------------------------------------------------------------------------

## 🧠 11. SELF JOIN Query

``` sql
SELECT e.name AS employee,
       m.name AS manager
FROM employees e
JOIN employees m
ON e.manager_id = m.emp_id;
```

------------------------------------------------------------------------

## 🧠 12. Result

### 🔹 Employee → Manager

| employee | manager |
|----------|---------|
| Simran   | Raj     |
| Arjun    | Raj     |

------------------------------------------------------------------------

## ❗ Why Alias is Required?

Because the **same table is used twice**


| Alias | Meaning  |
|-------|----------|
| e     | Employee |
| m     | Manager  |

------------------------------------------------------------------------

## 🧠 13. SELF JOIN Types

### ✅ INNER SELF JOIN

Shows only employees who have managers.

------------------------------------------------------------------------

### ✅ LEFT SELF JOIN

``` sql
SELECT e.name AS employee,
       m.name AS manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.emp_id;
```

✔ Includes CEO (NULL manager)

------------------------------------------------------------------------

## 🚀 14. SELF JOIN Interview Use Cases

✔ Employee → Manager hierarchy
✔ Find duplicate records
✔ Customers from same city
✔ Generate pairs
✔ Compare rows within same table
✔ Organizational tree

------------------------------------------------------------------------

## 🧪 15. Find Duplicates Using SELF JOIN

``` sql
SELECT a.name
FROM students a
JOIN students b
ON a.email = b.email
AND a.id <> b.id;
```

------------------------------------------------------------------------

## 🧪 16. Students Enrolled in Same Course (Pairs)

``` sql
SELECT a.student_id, b.student_id
FROM enrollments a
JOIN enrollments b
ON a.course_id = b.course_id
AND a.student_id < b.student_id;
```

------------------------------------------------------------------------


### 🔥 FULL JOIN vs SELF JOIN

| FULL JOIN               | SELF JOIN                          |
|-------------------------|------------------------------------|
| Two different tables    | Same table                         |
| Combines all rows       | Compares rows within table         |
| Used for reconciliation | Used for hierarchy & relationships |
| Find missing records    | Find duplicates / pairs            |


------------------------------------------------------------------------

# 🏆 Interview Summary

### FULL JOIN

➡️ Used for **data reconciliation & unmatched detection**

### SELF JOIN

➡️ Used for **hierarchy, comparison, duplicates, pairing**

------------------------------------------------------------------------

# ⭐ Pro Tip for Interviews

If interviewer asks:

Find missing data from both tables

``` sql
LEFT JOIN … WHERE NULL
UNION
RIGHT JOIN … WHERE NULL
```


# 🧠 SQL Practice — FULL JOIN & SELF JOIN (50 Questions)

----
# 🧠 SQL Practice Database Setup

A ready-to-run dataset for practicing:

* FULL JOIN
* SELF JOIN
* Aggregations
* Unmatched data detection
* Hierarchy queries

---

## 🗄️ Create Database

```sql
CREATE DATABASE sql_practice;
USE sql_practice;
```

---

# 🎓 STUDENTS & COURSES

## 👨‍🎓 Students

```sql
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(50)
);

INSERT INTO students VALUES
(1, 'Amit'),
(2, 'Neha'),
(3, 'Rahul'),
(4, 'Sneha'),
(5, 'Karan');
```

---

## 📚 Courses

```sql
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50)
);

INSERT INTO courses VALUES
(101, 'SQL'),
(102, 'Java'),
(103, 'Python'),
(104, 'Power BI');
```

---

## 📝 Enrollments

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT
);

INSERT INTO enrollments VALUES
(1, 101),
(2, 101),
(2, 102),
(3, 103),
(6, 101);  -- invalid student for FULL JOIN practice
```

---

# 🛒 CUSTOMERS & ORDERS

## 👥 Customers

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(50),
    city VARCHAR(50)
);

INSERT INTO customers VALUES
(1, 'Amit', 'Mumbai'),
(2, 'Neha', 'Pune'),
(3, 'Rahul', 'Delhi'),
(4, 'Sneha', 'Mumbai');
```

---

## 📦 Orders

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    amount INT
);

INSERT INTO orders VALUES
(101, 1, 500),
(102, 1, 700),
(103, 2, 400),
(104, 5, 900); -- invalid customer for FULL JOIN practice
```

---

# 🏬 PRODUCTS & SALES

## 🛍️ Products

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(50),
    price INT
);

INSERT INTO products VALUES
(1, 'Laptop', 50000),
(2, 'Mouse', 500),
(3, 'Keyboard', 1500),
(4, 'Monitor', 12000);
```

---

## 💰 Sales

```sql
CREATE TABLE sales (
    sale_id INT PRIMARY KEY,
    product_id INT,
    quantity INT
);

INSERT INTO sales VALUES
(1, 1, 2),
(2, 2, 5),
(3, 5, 1); -- invalid product for FULL JOIN practice
```

---

# 🏢 DEPARTMENTS & EMPLOYEES

## 🏬 Departments

```sql
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);

INSERT INTO departments VALUES
(10, 'HR'),
(20, 'IT'),
(30, 'Sales'),
(40, 'Marketing');
```

---

## 👨‍💼 Employees (SELF JOIN Table)

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(50),
    manager_id INT,
    dept_id INT,
    salary INT
);

INSERT INTO employees VALUES
(101, 'Raj', NULL, 20, 90000),
(102, 'Simran', 101, 20, 60000),
(103, 'Arjun', 101, 20, 65000),
(104, 'Priya', 102, 10, 50000),
(105, 'Karan', NULL, NULL, 40000);
```

---

# 🧪 Quick Test

```sql
SELECT * FROM students;
SELECT * FROM enrollments;
SELECT * FROM employees;
```
---

## 🟢 BASIC LEVEL (1–15)

### 🔹 FULL JOIN — Understanding Unmatched Data

1. Show all students and their enrollments (matched + unmatched)
2. Show all courses and their enrollments (include courses with no students)
3. Show all customers and their orders (include customers with no orders and invalid orders)
4. Show all products and their sales (include unsold products)
5. Show all departments and employees (include empty departments and employees without department)

### 🔹 Identify NULL Sides

6. Show students who are not enrolled in any course
7. Show enrollments that reference non-existing students
8. Show courses that have no enrollments
9. Show products that were never sold
10. Show customers who never placed an order

### 🔹 SELF JOIN — Basic Hierarchy

11. Show employee name with their manager name
12. Show all employees and their managers (include CEO)
13. Show employees who do not have a manager
14. Show employees who are managers
15. Show employee–manager pairs ordered by manager name

---

## 🟡 INTERMEDIATE LEVEL (16–30)

### 🔹 FULL JOIN with Filtering

16. Show only unmatched students and enrollments
17. Show only matched records between students and enrollments
18. Show non-matching customers and orders
19. Show non-matching products and sales
20. Show non-matching departments and employees

### 🔹 FULL JOIN + Aggregation

21. Count number of enrollments per student (include students with zero)
22. Count number of students per course (include empty courses)
23. Count orders per customer (include zero)
24. Show total sales per product (include unsold products)
25. Show total salary per department (include empty departments)

### 🔹 SELF JOIN — Comparison Within Same Table

26. Find pairs of students enrolled in the same course
27. Find employees working in the same department
28. Show customers from the same city (pair them)
29. Find products with the same price
30. Find students with the same name (duplicates)

---

## 🟠 ADVANCED LEVEL (31–40)

### 🔹 FULL JOIN — Reconciliation Queries

31. Compare students and enrollments and show missing records from both sides
32. Compare orders and customers and show invalid foreign key records
33. Show courses that never had any enrollment after a given date
34. Show customers who placed orders but no sales record exists
35. Show products that exist in sales but not in products table

### 🔹 SELF JOIN — Hierarchy & Depth

36. Show employee → manager → grand manager
37. Count number of employees under each manager
38. Show managers with more than 2 employees
39. Show employees who report to the same manager
40. Show the top-level manager (who has no manager)

---

## 🔴 HARD / INTERVIEW LEVEL (41–50)

### 🔹 FULL JOIN + HAVING

41. Find students enrolled in all courses
42. Find courses that have more than 2 students
43. Find customers who placed more than 2 orders
44. Find departments where total salary > 100000 (include empty ones)
45. Find products whose total sales amount is greater than average

### 🔹 SELF JOIN — Advanced Logic

46. Find the longest reporting chain in employees table
47. Show manager with highest team size
48. Find employees earning more than their manager
49. Find duplicate rows using self join (based on multiple columns)
50. Generate all possible student pairs for project grouping (no repetition)

---


## ✅ BASIC LEVEL — Solutions (1–5)

---

### 1️⃣ Show all students and their enrollments (matched + unmatched)

```sql
SELECT s.id, s.name, c.course_name
FROM students s
LEFT JOIN enrollments e ON s.id = e.student_id
LEFT JOIN courses c ON e.course_id = c.course_id

UNION

SELECT s.id, s.name, c.course_name
FROM students s
RIGHT JOIN enrollments e ON s.id = e.student_id
LEFT JOIN courses c ON e.course_id = c.course_id;
```

---

### 2️⃣ Show all courses and their enrollments (include courses with no students)

```sql
SELECT c.course_id, c.course_name, s.name
FROM courses c
LEFT JOIN enrollments e ON c.course_id = e.course_id
LEFT JOIN students s ON s.id = e.student_id

UNION

SELECT c.course_id, c.course_name, s.name
FROM courses c
RIGHT JOIN enrollments e ON c.course_id = e.course_id
LEFT JOIN students s ON s.id = e.student_id;
```

---

### 3️⃣ Show all customers and their orders

(include customers with no orders and invalid orders)

```sql
SELECT c.customer_id, c.name, o.order_id, o.amount
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id

UNION

SELECT c.customer_id, c.name, o.order_id, o.amount
FROM customers c
RIGHT JOIN orders o ON c.customer_id = o.customer_id;
```

---

### 4️⃣ Show all products and their sales (include unsold products)

```sql
SELECT p.product_id, p.product_name, s.quantity
FROM products p
LEFT JOIN sales s ON p.product_id = s.product_id

UNION

SELECT p.product_id, p.product_name, s.quantity
FROM products p
RIGHT JOIN sales s ON p.product_id = s.product_id;
```

---

### 5️⃣ Show all departments and employees

(include empty departments and employees without department)

```sql
SELECT d.dept_id, d.dept_name, e.name
FROM departments d
LEFT JOIN employees e ON d.dept_id = e.dept_id

UNION

SELECT d.dept_id, d.dept_name, e.name
FROM departments d
RIGHT JOIN employees e ON d.dept_id = e.dept_id;
```

---

## 🟢 BASIC LEVEL — Solutions (6–10)

---

### 6️⃣ Show students who are not enrolled in any course

```sql id="z9m1k6"
SELECT s.id, s.name
FROM students s
LEFT JOIN enrollments e
ON s.id = e.student_id
WHERE e.student_id IS NULL;
```

---

### 7️⃣ Show enrollments that reference non-existing students

```sql id="x5c4m2"
SELECT e.*
FROM students s
RIGHT JOIN enrollments e
ON s.id = e.student_id
WHERE s.id IS NULL;
```

---

### 8️⃣ Show courses that have no enrollments

```sql id="a7q2p1"
SELECT c.course_id, c.course_name
FROM courses c
LEFT JOIN enrollments e
ON c.course_id = e.course_id
WHERE e.course_id IS NULL;
```

---

### 9️⃣ Show products that were never sold

```sql id="w8v3n0"
SELECT p.product_id, p.product_name
FROM products p
LEFT JOIN sales s
ON p.product_id = s.product_id
WHERE s.product_id IS NULL;
```

---

### 🔟 Show customers who never placed an order

```sql id="r2k6d9"
SELECT c.customer_id, c.name
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.customer_id IS NULL;
```

---
## 🟢 BASIC LEVEL — Solutions (11–15)

---

### 1️⃣1️⃣ Show employee name with their manager name

```sql id="n3k8q1"
SELECT e.name AS employee, m.name AS manager
FROM employees e
JOIN employees m
ON e.manager_id = m.emp_id;
```

---

### 1️⃣2️⃣ Show all employees and their managers (include CEO)

```sql id="b6p2x4"
SELECT e.name AS employee, m.name AS manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.emp_id;
```

---

### 1️⃣3️⃣ Show employees who do not have a manager

```sql id="q1v9m7"
SELECT emp_id, name
FROM employees
WHERE manager_id IS NULL;
```

---

### 1️⃣4️⃣ Show employees who are managers

```sql id="t4z6k2"
SELECT DISTINCT m.emp_id, m.name
FROM employees e
JOIN employees m
ON e.manager_id = m.emp_id;
```

---

### 1️⃣5️⃣ Show employee–manager pairs ordered by manager name

```sql id="u8y3c5"
SELECT e.name AS employee, m.name AS manager
FROM employees e
JOIN employees m
ON e.manager_id = m.emp_id
ORDER BY m.name;
```

---
## 🟡 INTERMEDIATE LEVEL — Solutions (16–20)

---

### 1️⃣6️⃣ Show only unmatched students and enrollments

```sql id="k2m9x1"
SELECT s.id, s.name, e.course_id
FROM students s
LEFT JOIN enrollments e
ON s.id = e.student_id
WHERE e.student_id IS NULL

UNION

SELECT s.id, s.name, e.course_id
FROM students s
RIGHT JOIN enrollments e
ON s.id = e.student_id
WHERE s.id IS NULL;
```

---

### 1️⃣7️⃣ Show only matched records between students and enrollments

```sql id="p7v4c8"
SELECT s.id, s.name, e.course_id
FROM students s
JOIN enrollments e
ON s.id = e.student_id;
```

---

### 1️⃣8️⃣ Show non-matching customers and orders

```sql id="d5q1z6"
SELECT c.customer_id, c.name, o.order_id
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.customer_id IS NULL

UNION

SELECT c.customer_id, c.name, o.order_id
FROM customers c
RIGHT JOIN orders o
ON c.customer_id = o.customer_id
WHERE c.customer_id IS NULL;
```

---

### 1️⃣9️⃣ Show non-matching products and sales

```sql id="m8w3n2"
SELECT p.product_id, p.product_name, s.sale_id
FROM products p
LEFT JOIN sales s
ON p.product_id = s.product_id
WHERE s.product_id IS NULL

UNION

SELECT p.product_id, p.product_name, s.sale_id
FROM products p
RIGHT JOIN sales s
ON p.product_id = s.product_id
WHERE p.product_id IS NULL;
```

---

### 2️⃣0️⃣ Show non-matching departments and employees

```sql id="x6r2b9"
SELECT d.dept_id, d.dept_name, e.emp_id
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id
WHERE e.dept_id IS NULL

UNION

SELECT d.dept_id, d.dept_name, e.emp_id
FROM departments d
RIGHT JOIN employees e
ON d.dept_id = e.dept_id
WHERE d.dept_id IS NULL;
```

---
## 🟡 INTERMEDIATE LEVEL — Solutions (21–25)

---

### 2️⃣1️⃣ Count number of enrollments per student (include students with zero)

```sql id="h3k9p2"
SELECT s.id, s.name, COUNT(e.course_id) AS total_enrollments
FROM students s
LEFT JOIN enrollments e
ON s.id = e.student_id
GROUP BY s.id, s.name;
```

---

### 2️⃣2️⃣ Count number of students per course (include empty courses)

```sql id="c7v1x5"
SELECT c.course_id, c.course_name, COUNT(e.student_id) AS total_students
FROM courses c
LEFT JOIN enrollments e
ON c.course_id = e.course_id
GROUP BY c.course_id, c.course_name;
```

---

### 2️⃣3️⃣ Count orders per customer (include zero)

```sql id="n2q8m4"
SELECT c.customer_id, c.name, COUNT(o.order_id) AS total_orders
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.name;
```

---

### 2️⃣4️⃣ Show total sales per product (include unsold products)

```sql id="w5z6k1"
SELECT p.product_id, p.product_name,
       COALESCE(SUM(s.quantity), 0) AS total_quantity
FROM products p
LEFT JOIN sales s
ON p.product_id = s.product_id
GROUP BY p.product_id, p.product_name;
```

---

### 2️⃣5️⃣ Show total salary per department (include empty departments)

```sql id="r9d4t7"
SELECT d.dept_id, d.dept_name,
       COALESCE(SUM(e.salary), 0) AS total_salary
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id
GROUP BY d.dept_id, d.dept_name;
```

---
## 🟡 INTERMEDIATE LEVEL — Solutions (26–30)

---

### 2️⃣6️⃣ Find pairs of students enrolled in the same course

```sql id="p4x8k2"
SELECT a.student_id, b.student_id, a.course_id
FROM enrollments a
JOIN enrollments b
ON a.course_id = b.course_id
AND a.student_id < b.student_id;
```

---

### 2️⃣7️⃣ Find employees working in the same department

```sql id="m7q1v6"
SELECT a.name AS employee1, b.name AS employee2, a.dept_id
FROM employees a
JOIN employees b
ON a.dept_id = b.dept_id
AND a.emp_id < b.emp_id;
```

---

### 2️⃣8️⃣ Show customers from the same city (pair them)

```sql id="k3c9z5"
SELECT a.name AS customer1, b.name AS customer2, a.city
FROM customers a
JOIN customers b
ON a.city = b.city
AND a.customer_id < b.customer_id;
```

---

### 2️⃣9️⃣ Find products with the same price

```sql id="t8n2w4"
SELECT a.product_name AS product1, b.product_name AS product2, a.price
FROM products a
JOIN products b
ON a.price = b.price
AND a.product_id < b.product_id;
```

---

### 3️⃣0️⃣ Find students with the same name (duplicates)

```sql id="v6r3p1"
SELECT a.id, a.name
FROM students a
JOIN students b
ON a.name = b.name
AND a.id <> b.id;
```

---
## 🟠 ADVANCED LEVEL — Solutions (31–35)

---

### 3️⃣1️⃣ Compare students and enrollments and show missing records from both sides

```sql id="a1k9x3"
SELECT s.id, s.name, e.student_id, e.course_id
FROM students s
LEFT JOIN enrollments e
ON s.id = e.student_id
WHERE e.student_id IS NULL

UNION

SELECT s.id, s.name, e.student_id, e.course_id
FROM students s
RIGHT JOIN enrollments e
ON s.id = e.student_id
WHERE s.id IS NULL;
```

---

### 3️⃣2️⃣ Compare orders and customers and show invalid foreign key records

```sql id="f6m2q8"
SELECT c.customer_id, c.name, o.order_id
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.customer_id IS NULL

UNION

SELECT c.customer_id, c.name, o.order_id
FROM customers c
RIGHT JOIN orders o
ON c.customer_id = o.customer_id
WHERE c.customer_id IS NULL;
```

---

### 3️⃣3️⃣ Show courses that never had any enrollment after a given date

```sql id="d8p4z7"
SELECT c.course_id, c.course_name
FROM courses c
LEFT JOIN enrollments e
ON c.course_id = e.course_id
WHERE e.course_id IS NULL;
```

---

### 3️⃣4️⃣ Show customers who placed orders but no sales record exists

```sql id="g3v9n1"
SELECT DISTINCT c.customer_id, c.name
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id
LEFT JOIN sales s
ON s.product_id = o.order_id
WHERE s.product_id IS NULL;
```

---

### 3️⃣5️⃣ Show products that exist in sales but not in products table

```sql id="h5t1w6"
SELECT p.product_id, p.product_name, s.product_id AS sales_product
FROM products p
RIGHT JOIN sales s
ON p.product_id = s.product_id
WHERE p.product_id IS NULL;
```

---
## 🟠 ADVANCED LEVEL — Solutions (36–40)

---

### 3️⃣6️⃣ Show employee → manager → grand manager

```sql id="k7m2p4"
SELECT e.name AS employee,
       m.name AS manager,
       gm.name AS grand_manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.emp_id
LEFT JOIN employees gm
ON m.manager_id = gm.emp_id;
```

---

### 3️⃣7️⃣ Count number of employees under each manager

```sql id="q3v8x1"
SELECT m.emp_id, m.name, COUNT(e.emp_id) AS team_size
FROM employees e
JOIN employees m
ON e.manager_id = m.emp_id
GROUP BY m.emp_id, m.name;
```

---

### 3️⃣8️⃣ Show managers with more than 2 employees

```sql id="p6n4z9"
SELECT m.emp_id, m.name
FROM employees e
JOIN employees m
ON e.manager_id = m.emp_id
GROUP BY m.emp_id, m.name
HAVING COUNT(e.emp_id) > 2;
```

---

### 3️⃣9️⃣ Show employees who report to the same manager

```sql id="r1t5w8"
SELECT a.name AS employee1,
       b.name AS employee2,
       a.manager_id
FROM employees a
JOIN employees b
ON a.manager_id = b.manager_id
AND a.emp_id < b.emp_id;
```

---

### 4️⃣0️⃣ Show the top-level manager (who has no manager)

```sql id="x9c2k7"
SELECT emp_id, name
FROM employees
WHERE manager_id IS NULL;
```

---
## 🔴 HARD / INTERVIEW LEVEL — Solutions (41–45)

---

### 4️⃣1️⃣ Find students enrolled in all courses

```sql id="p2k9x4"
SELECT e.student_id
FROM enrollments e
GROUP BY e.student_id
HAVING COUNT(DISTINCT e.course_id) =
(
    SELECT COUNT(*) FROM courses
);
```

---

### 4️⃣2️⃣ Find courses that have more than 2 students

```sql id="m7v3c1"
SELECT c.course_id, c.course_name
FROM courses c
JOIN enrollments e
ON c.course_id = e.course_id
GROUP BY c.course_id, c.course_name
HAVING COUNT(DISTINCT e.student_id) > 2;
```

---

### 4️⃣3️⃣ Find customers who placed more than 2 orders

```sql id="n8q5z2"
SELECT c.customer_id, c.name
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.name
HAVING COUNT(o.order_id) > 2;
```

---

### 4️⃣4️⃣ Find departments where total salary > 100000 (include empty ones)

```sql id="t4x1k6"
SELECT d.dept_id, d.dept_name,
       COALESCE(SUM(e.salary), 0) AS total_salary
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id
GROUP BY d.dept_id, d.dept_name
HAVING COALESCE(SUM(e.salary), 0) > 100000;
```

---

### 4️⃣5️⃣ Find products whose total sales amount is greater than average

```sql id="w6r8p3"
SELECT p.product_id, p.product_name,
       SUM(s.quantity * p.price) AS total_sales
FROM products p
JOIN sales s
ON p.product_id = s.product_id
GROUP BY p.product_id, p.product_name
HAVING SUM(s.quantity * p.price) >
(
    SELECT AVG(total_sales)
    FROM (
        SELECT SUM(s.quantity * p.price) AS total_sales
        FROM products p
        JOIN sales s
        ON p.product_id = s.product_id
        GROUP BY p.product_id
    ) t
);
```

---
## 🔴 HARD / INTERVIEW LEVEL — Solutions (46–50)

---

### 4️⃣6️⃣ Find the longest reporting chain in employees table

```sql id="k9x3p7"
WITH RECURSIVE emp_cte AS (
    SELECT emp_id, manager_id, 1 AS level
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    SELECT e.emp_id, e.manager_id, level + 1
    FROM employees e
    JOIN emp_cte c
    ON e.manager_id = c.emp_id
)
SELECT MAX(level) AS longest_chain
FROM emp_cte;
```

---

### 4️⃣7️⃣ Show manager with highest team size

```sql id="p4v8m2"
SELECT m.emp_id, m.name, COUNT(e.emp_id) AS team_size
FROM employees e
JOIN employees m
ON e.manager_id = m.emp_id
GROUP BY m.emp_id, m.name
ORDER BY team_size DESC
LIMIT 1;
```

---

### 4️⃣8️⃣ Find employees earning more than their manager

```sql id="t7n1q5"
SELECT e.name AS employee, m.name AS manager,
       e.salary AS employee_salary,
       m.salary AS manager_salary
FROM employees e
JOIN employees m
ON e.manager_id = m.emp_id
WHERE e.salary > m.salary;
```

---

### 4️⃣9️⃣ Find duplicate rows using self join (based on multiple columns)

```sql id="r2c6x9"
SELECT a.*
FROM employees a
JOIN employees b
ON a.name = b.name
AND a.dept_id = b.dept_id
AND a.salary = b.salary
AND a.emp_id <> b.emp_id;
```

---

### 5️⃣0️⃣ Generate all possible student pairs for project grouping (no repetition)

```sql id="z8k4p1"
SELECT a.id AS student1, b.id AS student2
FROM students a
JOIN students b
ON a.id < b.id;
```

---

