# 📅 DAY 10 --- LEFT JOIN (Complete Deep Theory)

## 🧠 1. WHY LEFT JOIN?

INNER JOIN → gives only matching data
LEFT JOIN →
- keeps unmatched rows,
- missing data,
- zero counts.

Used for: - Who did NOT... - Missing relationships - Zero counts

------------------------------------------------------------------------

## 🧠 2. DEFINITION

**LEFT JOIN** - Returns ALL rows from LEFT table - Matching rows from
RIGHT table - If no match → NULL

------------------------------------------------------------------------

## 🧠 3. VISUAL

**LEFT TABLE:** 1 2 3 4  
**RIGHT TABLE:** 2 3  

### RESULT

| LEFT | RIGHT |
|------|-------|
| 1    | NULL  |
| 2    | Match |
| 3    | Match |
| 4    | NULL  |

------------------------------------------------------------------------

## 🧠 4. SYNTAX

``` sql
SELECT column_list
FROM table1
LEFT JOIN table2
ON table1.common_column = table2.common_column;
```

⚠ table1 = LEFT TABLE

------------------------------------------------------------------------

## 🧪 5. PRACTICE TABLES

``` sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50)
);
```
```
CREATE TABLE enrollments (
    student_id INT,
    course VARCHAR(50)
);
```

### INSERT DATA

``` sql
INSERT INTO students VALUES
(1,'Amit'),
(2,'Neha'),
(3,'Rahul'),
(4,'Sneha');
```
```
INSERT INTO enrollments VALUES
(1,'SQL'),
(2,'Java'),
(3,'Python');
```

------------------------------------------------------------------------

## 🧪 6. BASIC LEFT JOIN

``` sql
SELECT name, course
FROM students s
LEFT JOIN enrollments e
ON s.student_id = e.student_id;
```

### ✅ RESULT

| name  | course |
|-------|--------|
| Amit  | SQL    |
| Neha  | Java   |
| Rahul | Python |
| Sneha | NULL ⭐ |

### WHY NULL?

Sneha exists in LEFT table but not in RIGHT.

------------------------------------------------------------------------

## 🧠 7. LEFT vs INNER

| JOIN  | RESULT                  |
|-------|--------------------------|
| INNER | Only matched rows        |
| LEFT  | All left + matched rows  |

------------------------------------------------------------------------

## 🧠 8. FIND UNMATCHED

``` sql
SELECT name
FROM students s
LEFT JOIN enrollments e
ON s.student_id = e.student_id
WHERE e.student_id IS NULL;
```

------------------------------------------------------------------------

## 🧠 9. COUNT WITH LEFT JOIN

``` sql
SELECT s.name, COUNT(e.course) AS total_courses
FROM students s
LEFT JOIN enrollments e
ON s.student_id = e.student_id
GROUP BY s.name;
```

### RESULT

| name  | total_courses |
|-------|---------------|
| Amit  | 1             |
| Neha  | 1             |
| Rahul | 1             |
| Sneha | 0 ⭐          |

### WHY 0?

COUNT(column) ignores NULL.

------------------------------------------------------------------------

## ❌ COMMON MISTAKE

``` sql
COUNT(*)
```

Counts NULL rows → Wrong for zero-count problems.

------------------------------------------------------------------------

## 🧠 10. MULTIPLE LEFT JOIN

``` sql
SELECT s.name, c.course_name
FROM students s
LEFT JOIN enrollments e
ON s.student_id = e.student_id
LEFT JOIN courses c
ON e.course_id = c.course_id;
```

------------------------------------------------------------------------

## 🧠 11. FILTERING (IMPORTANT)

❌ WRONG

``` sql
WHERE c.course_name = 'SQL'
```

Converts LEFT → INNER.

✅ CORRECT

``` sql
LEFT JOIN courses c
ON e.course_id = c.course_id
AND c.course_name = 'SQL'
```

------------------------------------------------------------------------

## 🧠 12. INTERVIEW PATTERNS

-   Customers with no orders
-   Departments with no employees
-   Products never sold
-   Zero counts

Using:

``` sql
LEFT JOIN + IS NULL
```

------------------------------------------------------------------------

## 🧠 13. EXECUTION FLOW

- 1.  FROM
- 2.  LEFT JOIN
- 3.  ON
- 4.  WHERE
- 5.  GROUP BY
- 6.  SELECT

------------------------------------------------------------------------

## 🧠 14. PERFORMANCE

-   Slightly heavier than INNER JOIN
-   Use index on join column

------------------------------------------------------------------------

# 🏆 MOST ASKED INTERVIEW QUESTION

### Difference between INNER JOIN and LEFT JOIN

**INNER JOIN → Only matched rows**
**LEFT JOIN → All left rows + matched rows (unmatched → NULL)**

------------------------------------------------------------------------

# 📘 SQL JOIN Practice Sheet (50 Questions)

# 🗄️ SQL PRACTICE — COMPLETE SCHEMA SETUP

## 🟢 1. CREATE DATABASE

```sql
CREATE DATABASE sql_practice;
USE sql_practice;
```

---

## 👨‍🎓 2. STUDENTS

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50)
);

INSERT INTO students VALUES
(1,'Amit'),
(2,'Neha'),
(3,'Rahul'),
(4,'Sneha'),
(5,'Karan'),
(6,'Pooja');
```

---

## 📚 3. COURSES

```sql
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50)
);

INSERT INTO courses VALUES
(101,'SQL'),
(102,'Java'),
(103,'Python'),
(104,'Power BI'),
(105,'Tableau');
```

---

## 📝 4. ENROLLMENTS (Many-to-Many)

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    enroll_date DATE,
    PRIMARY KEY (student_id, course_id)
);

INSERT INTO enrollments VALUES
(1,101,'2024-01-10'),
(1,102,'2024-01-12'),
(2,103,'2024-01-15'),
(3,101,'2024-01-18'),
(3,103,'2024-01-20'),
(4,104,'2024-01-22');
```

👉 **Karan & Pooja not enrolled → for LEFT JOIN NULL cases**

---

## 👨‍💼 5. DEPARTMENTS

```sql
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);

INSERT INTO departments VALUES
(10,'HR'),
(20,'IT'),
(30,'Sales'),
(40,'Marketing');
```

---

## 👩‍💻 6. EMPLOYEES

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    salary INT,
    dept_id INT,
    manager_id INT
);

INSERT INTO employees VALUES
(101,'Raj',50000,10,NULL),
(102,'Simran',60000,20,101),
(103,'Arjun',55000,20,101),
(104,'Kavya',45000,30,102),
(105,'Mohit',70000,NULL,101);
```

👉 **Mohit has no department → LEFT JOIN case**  
👉 **manager_id → for self join**

---

## 👥 7. CUSTOMERS

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(50)
);

INSERT INTO customers VALUES
(1,'Amit'),
(2,'Neha'),
(3,'Rahul'),
(4,'Sneha'),
(5,'Karan');
```

---

## 🧾 8. ORDERS

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE
);

INSERT INTO orders VALUES
(1001,1,'2024-02-01'),
(1002,1,'2024-02-03'),
(1003,2,'2024-02-05'),
(1004,3,'2024-02-07');
```

👉 **Sneha & Karan have no orders**

---

## 📦 9. PRODUCTS

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(50),
    price INT
);

INSERT INTO products VALUES
(201,'Laptop',80000),
(202,'Mouse',500),
(203,'Keyboard',1000),
(204,'Monitor',15000),
(205,'Headphones',2000);
```

---

## 💰 10. SALES

```sql
CREATE TABLE sales (
    sale_id INT PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity INT,
    amount INT
);

INSERT INTO sales VALUES
(1,1001,201,1,80000),
(2,1001,202,2,1000),
(3,1002,203,1,1000),
(4,1003,204,1,15000),
(5,1004,201,1,80000);
```

👉 **Headphones never sold → for LEFT JOIN NULL case**

---

# 🧠 RELATIONSHIP MAP (REMEMBER THIS)

```
students ──< enrollments >── courses

departments ──< employees
                     │
                     └── manager_id → self join

customers ──< orders ──< sales >── products
```

## 🟢 BASIC LEVEL (1–15)

### 🔹 INNER JOIN — basic matching

1. Show student names with their enrolled course IDs.  
2. Show student name and course name.  
3. Show employee name with department name.  
4. Show order_id with customer_name.  
5. Show product_name with sale amount.  

### 🔹 LEFT JOIN — basic

6. Show all students and their courses (include students with no course).  
7. Show all departments and their employees.  
8. Show all customers and their orders.  
9. Show all products and their sales quantity.  
10. Show all courses and enrolled students.  

### 🔹 Filtering

11. Show students enrolled in SQL course.  
12. Show employees working in IT department.  
13. Show orders placed by a specific customer.  
14. Show sales for a specific product.  
15. Show students whose course_id = 101.  

---

## 🟡 INTERMEDIATE LEVEL (16–30)

### 🔹 LEFT JOIN + IS NULL (very important)

16. Find students who are not enrolled in any course.  
17. Find departments with no employees.  
18. Find customers who never placed an order.  
19. Find products that were never sold.  
20. Find courses with zero students.  

### 🔹 COUNT with JOIN

21. Count number of students in each course.  
22. Count number of employees in each department.  
23. Count orders per customer.  
24. Count how many courses each student enrolled in.  
25. Show departments with employee count (include zero).  

### 🔹 ORDER BY with JOIN

26. Show students with course names sorted by student name.  
27. Show employees sorted by department name.  
28. Show customers by number of orders (descending).  
29. Show courses by number of students.  
30. Show top 3 customers who placed most orders.  

---

## 🟠 ADVANCED LEVEL (31–40)

### 🔹 MULTI TABLE JOIN

31. Show student name, course name, and enrollment date.  
32. Show order_id, customer_name, product_name.  
33. Show employee name, department name, and manager name.  
34. Show sales with product and customer details.  
35. Show students enrolled in multiple courses.  

### 🔹 GROUP BY + HAVING

36. Show courses having more than 3 students.  
37. Show customers who placed more than 5 orders.  
38. Show departments with total salary > 1,00,000.  
39. Show students enrolled in more than 2 courses.  
40. Show products sold more than 10 times.  

---

## 🔴 HARD / INTERVIEW LEVEL (41–50)

### 🔹 LOGIC BASED

41. Find the most popular course (maximum students).  
42. Find the department with highest number of employees.  
43. Find customer who spent the most money.  
44. Find product with lowest sales.  
45. Find students who enrolled in ALL courses.  

### 🔹 LEFT JOIN + AGGREGATION EDGE CASES

46. Show students and number of courses (students with zero must appear).  
47. Show departments and average salary (include empty departments).  
48. Show customers with total order amount (NULL → 0).  
49. Show courses with no enrollments and display 0 as count.  
50. Show employees who are not assigned to any department.  

---
