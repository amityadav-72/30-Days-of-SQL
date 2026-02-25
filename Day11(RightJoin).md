# RIGHT JOIN -- Complete Advanced Guide

## 1. What is RIGHT JOIN

- RIGHT JOIN returns all rows from the right table and matching rows from
- the left table.
- Unmatched left rows → NULL.

------------------------------------------------------------------------

## 2. RIGHT JOIN = LEFT JOIN (Swapped Tables)

`A RIGHT JOIN B`

is same as:

`B LEFT JOIN A`

------------------------------------------------------------------------

## 3. Sample Tables

<table>
<tr>
<td valign="top">

### 🎓 Students

| student_id | student_name |
|------------|-------------|
| 1 | Amit  |
| 2 | Neha  |
| 3 | Rahul |

</td>

<td valign="top">

### 📝 Enrollments

| student_id | course_id |
|------------|-----------|
| 1 | 101 |
| 2 | 102 |

</td>

<td valign="top">

### 📚 Courses

| course_id | course_name |
|-----------|------------|
| 101 | SQL    |
| 102 | Java   |
| 103 | Python |

</td>
</tr>
</table>

------------------------------------------------------------------------

## 4. Show All Courses and Enrolled Students

``` sql
SELECT c.course_name, s.student_name
FROM students s
RIGHT JOIN enrollments e
ON s.student_id = e.student_id
RIGHT JOIN courses c
ON e.course_id = c.course_id;
```

### Result Logic

- All courses appear
- Courses without students → NULL

------------------------------------------------------------------------

## 5. Find Courses With No Students

``` sql
SELECT c.course_name
FROM students s
RIGHT JOIN enrollments e
ON s.student_id = e.student_id
RIGHT JOIN courses c
ON e.course_id = c.course_id
WHERE s.student_id IS NULL;
```

------------------------------------------------------------------------

## 6. RIGHT JOIN + COUNT

``` sql
SELECT c.course_name, COUNT(s.student_id) AS total_students
FROM students s
RIGHT JOIN enrollments e
ON s.student_id = e.student_id
RIGHT JOIN courses c
ON e.course_id = c.course_id
GROUP BY c.course_name;
```

### Why COUNT(student_id)?

COUNT ignores NULL → gives 0 for empty courses.

------------------------------------------------------------------------

## 7. Execution Flow

1.  First RIGHT JOIN executes
2.  Result joins with next table

Internally behaves like LEFT JOIN.

------------------------------------------------------------------------

## 8. Common Mistakes

-   Thinking RIGHT JOIN is different logic
-   Using COUNT(*) instead of COUNT(column)
-   Confusing table order
-   Wrong NULL filtering column

------------------------------------------------------------------------

## 9. Performance Note

1. Query optimizer rewrites:

2. RIGHT JOIN → LEFT JOIN

3. So performance difference is negligible.

------------------------------------------------------------------------

## 10. Interview Question

Convert:

A RIGHT JOIN B

### Answer:

``` sql
B LEFT JOIN A
```

------------------------------------------------------------------------

## 11. JOIN Comparison

 | JOIN TYPE  | RETURNS                  |
|------------|--------------------------|
| INNER JOIN | Matching rows only       |
| LEFT JOIN  | All left + matching      |
| RIGHT JOIN | All right + matching     |

------------------------------------------------------------------------

## 12. Senior-Level Interview Answer

Do you use RIGHT JOIN?

Rarely.
Because LEFT JOIN with swapped table order is more readable and gives
the same result.


# 📘 RIGHT JOIN – Practice Questions (Basic → Interview Level)


```
CREATE DATABASE right_join_practice;
USE right_join_practice;
```

-- ================= STUDENTS =================
```
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50)
);

CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50)
);

CREATE TABLE enrollments (
    enroll_id INT PRIMARY KEY,
    student_id INT,
    course_id INT,
    enroll_date DATE
);

INSERT INTO students VALUES
(1,'Amit'),
(2,'Neha'),
(3,'Rahul'),
(4,'Sneha');

INSERT INTO courses VALUES
(101,'SQL'),
(102,'Java'),
(103,'Python'),
(104,'Power BI');

INSERT INTO enrollments VALUES
(1,1,101,'2024-01-10'),
(2,2,102,'2024-01-12'),
(3,1,103,'2024-01-15'),
(4,5,101,'2024-02-01');

```
-- ================= DEPARTMENTS =================
```
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);

CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    salary INT,
    dept_id INT,
    manager_id INT
);

INSERT INTO departments VALUES
(10,'HR'),
(20,'IT'),
(30,'Sales'),
(40,'Marketing');

INSERT INTO employees VALUES
(1,'John',50000,10,NULL),
(2,'Sara',60000,20,1),
(3,'Mike',55000,20,1),
(4,'Emma',45000,30,NULL);
```
-- ================= CUSTOMERS =================
```
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(50)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    amount INT
);

INSERT INTO customers VALUES
(1,'Raj'),
(2,'Simran'),
(3,'Arjun'),
(4,'Priya');

INSERT INTO orders VALUES
(101,1,'2024-03-01',500),
(102,2,'2024-03-05',700),
(103,1,'2024-03-10',300);
```

-- ================= PRODUCTS =================
```
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(50),
    price INT
);

CREATE TABLE sales (
    sale_id INT PRIMARY KEY,
    product_id INT,
    quantity INT
);

INSERT INTO products VALUES
(1,'Laptop',50000),
(2,'Mouse',500),
(3,'Keyboard',1000),
(4,'Monitor',8000);

INSERT INTO sales VALUES
(1,1,2),
(2,2,5),
(3,1,1);
```
---

## 🟢 BASIC LEVEL (1–15)

### 🔹 Basic Matching

1. Show all enrollments with student names using RIGHT JOIN.  
2. Show all courses with enrolled student IDs using RIGHT JOIN.  
3. Show all departments with employee names using RIGHT JOIN.  
4. Show all orders with customer names using RIGHT JOIN.  
5. Show all sales with product names using RIGHT JOIN.  

---

### 🔹 Understand NULL Side

6. Show all courses and student names (include courses with no students).  
7. Show all departments and employees (include empty departments).  
8. Show all customers and their orders (include customers with no orders).  
9. Show all products and their sales (include unsold products).  
10. Show all students and their enrollments using RIGHT JOIN (observe result).  

---

### 🔹 Selecting Specific Columns

11. Show course_name and student_name using RIGHT JOIN.  
12. Show dept_name and emp_name using RIGHT JOIN.  
13. Show customer_name and order_date using RIGHT JOIN.  
14. Show product_name and quantity using RIGHT JOIN.  
15. Show course_name and enroll_date.  

---

## 🟡 INTERMEDIATE LEVEL (16–30)

### 🔹 RIGHT JOIN + WHERE

16. Show only courses where student is enrolled.  
17. Show only departments that have employees.  
18. Show only customers who placed orders.  
19. Show only products that were sold.  
20. Show only students who have enrollments using RIGHT JOIN.  

---

### 🔹 RIGHT JOIN + IS NULL (⭐ Most Important Pattern)

21. Find courses with no students.  
22. Find departments with no employees.  
23. Find customers with no orders.  
24. Find products that were never sold.  
25. Find enrollments that reference missing students.  

---

### 🔹 RIGHT JOIN + ORDER BY

26. Show all courses with students sorted by course_name.  
27. Show departments with employees sorted by emp_name.  
28. Show customers and their orders sorted by order_date.  
29. Show products and total quantity sold sorted descending.  
30. Show courses sorted by number of students.  

---

## 🟠 ADVANCED LEVEL (31–40)

### 🔹 GROUP BY with RIGHT JOIN

31. Count students per course (include courses with zero students).  
32. Count employees per department (include empty departments).  
33. Count orders per customer (include zero).  
34. Show total sales amount per product (include unsold products).  
35. Show average salary per department (include empty departments).  

---

### 🔹 MULTI-TABLE RIGHT JOIN

36. Show course_name and student_name using students + enrollments + courses.  
37. Show order_id, customer_name, product_name using orders + sales + products.  
38. Show employee name and manager name using RIGHT JOIN (self join logic).  
39. Show customer_name and total amount spent.  
40. Show student_name and total courses enrolled.  

---

## 🔴 HARD / INTERVIEW LEVEL (41–50)

### 🔹 Logic Building

41. Find the course with maximum students.  
42. Find department with highest employee count.  
43. Find customer who placed the most orders.  
44. Find product with lowest sales (include unsold).  
45. Find courses where more than one student enrolled.  

---

### 🔹 NULL + AGGREGATION EDGE CASES

46. Show courses with student count (display 0 instead of NULL).  
47. Show departments with total salary (NULL → 0).  
48. Show customers with total order amount (NULL → 0).  
49. Show products with total revenue (include unsold).  
50. Find courses where no enrollment happened after a specific date.  

---

