# SQL SUBQUERIES -- 

## 🧠 1. WHAT IS A SUBQUERY?

A subquery is a query written inside another query.
Also called: - Inner query - Nested query

``` sql
SELECT column
FROM table
WHERE column = (
    SELECT column
    FROM table
);
```

Inner query runs first → result goes to outer query.

------------------------------------------------------------------------

## 🧠 2. WHY DO WE NEED SUBQUERIES?

When a query depends on the result of another query.

🎯 Example Requirement

“Find employees who earn more than the average salary”

Steps:

1️⃣ Find average salary
2️⃣ Compare each salary with it

This needs a subquery.

------------------------------------------------------------------------

## 🧠 3. EXECUTION FLOW

``` sql
SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

## 🧠 3. HOW DATABASE RUNS (EXECUTION FLOW)

### Step 1 → Run the inner query

``` sql
SELECT AVG(salary) 
FROM employees;
```

📌 Suppose the result is:

    55000

------------------------------------------------------------------------

### Step 2 → Outer query becomes

``` sql
SELECT name
FROM employees
WHERE salary > 55000;
```

------------------------------------------------------------------------

### 🔍 What actually happens internally

1.  Inner query runs first
2.  Result is stored temporarily
3.  Outer query uses that result
4.  Final output is returned


------------------------------------------------------------------------

## 🧠 4. TYPES OF SUBQUERIES


A **subquery = query inside another query**

``` sql
SELECT column
FROM table
WHERE column OPERATOR (SELECT column FROM table);
```

------------------------------------------------------------------------

## 🧠 1. SINGLE ROW SUBQUERY

Returns only **one row**

### ✅ Operators used
```
= \> \< \>= \<= \<\>
```

### 📌 Example

Find students who scored more than the average marks

``` sql
SELECT name, marks
FROM students
WHERE marks > (
    SELECT AVG(marks) FROM students
);
```

✔ Inner query → returns single value
✔ Outer query → compares with it

------------------------------------------------------------------------

## 🧠 2. MULTIPLE ROW SUBQUERY

Returns **more than one row**

### ✅ Operators used

IN ANY ALL

### 📌 Example --- IN

Find students enrolled in Java or Python

``` sql
SELECT name
FROM students
WHERE course_id IN (
    SELECT course_id
    FROM courses
    WHERE course_name IN ('Java', 'Python')
);
```

### 📌 Example --- ANY

Find students who scored more than any student in section A

``` sql
SELECT name, marks
FROM students
WHERE marks > ANY (
    SELECT marks
    FROM students
    WHERE section = 'A'
);
```

💡 greater than **minimum**

### 📌 Example --- ALL

Find students who scored more than all students in section A

``` sql
SELECT name, marks
FROM students
WHERE marks > ALL (
    SELECT marks
    FROM students
    WHERE section = 'A'
);
```

💡 greater than **maximum**

------------------------------------------------------------------------

## 🧠 3. MULTIPLE COLUMN SUBQUERY

Returns multiple columns

``` sql
SELECT name
FROM students
WHERE (course_id, marks) IN (
    SELECT course_id, MAX(marks)
    FROM students
    GROUP BY course_id
);
```

------------------------------------------------------------------------

## 🧠 4. CORRELATED SUBQUERY 🔥

Inner query depends on outer query
Runs once for each row

``` sql
SELECT name, course_id, marks
FROM students s1
WHERE marks > (
    SELECT AVG(marks)
    FROM students s2
    WHERE s1.course_id = s2.course_id
);
```

------------------------------------------------------------------------

## 🧠 5. SCALAR SUBQUERY

Returns exactly **one value**
Used in SELECT, WHERE, HAVING

``` sql
SELECT name,
       (SELECT AVG(marks) FROM students) AS avg_marks
FROM students;
```

------------------------------------------------------------------------

## 🧠 6. EXISTS SUBQUERY

Checks whether rows exist
Returns → TRUE / FALSE

``` sql
SELECT name
FROM students s
WHERE EXISTS (
    SELECT 1
    FROM enrollments e
    WHERE s.student_id = e.student_id
);
```

💡 Faster than IN for large data

------------------------------------------------------------------------

# 🔥 OPERATORS USED WITH SUBQUERIES

## 🔹 IN

Match any value

``` sql
WHERE column IN (subquery)
```

## 🔹 NOT IN

Value must not match

``` sql
WHERE column NOT IN (subquery)
```

⚠ Fails if NULL exists

## 🔹 ANY

Condition true for at least one value
```
> ANY → greater than minimum
< ANY → less than maximum
```
## 🔹 ALL
```
Condition true for every value

> ALL → greater than maximum
< ALL → less than minimum
```
## 🔹 EXISTS

Checks row existence

``` sql
WHERE EXISTS (subquery)
```

✔ Stops after first match → fast

## 🔹 NOT EXISTS

``` sql
WHERE NOT EXISTS (subquery)
```

## 🔹 COMPARISON OPERATORS

Used with single row subquery
```
= \> \< \>= \<= \<\>
```
------------------------------------------------------------------------

# 🎯 QUICK INTERVIEW SUMMARY

## ✅ Subquery Types

1.  Single row
2.  Multiple row
3.  Multiple column
4.  Correlated
5.  Scalar
6.  EXISTS

------------------------------------------------------------------------

## ✅ Operators

IN
NOT IN
ANY
ALL
EXISTS
NOT EXISTS
Comparison operators

------------------------------------------------------------------------

# 🚀 PRO LEVEL INTERVIEW POINT

## ⭐ IN vs EXISTS


| IN | EXISTS |
|----|--------|
Compares values | Checks rows |
Slower (large data) | Faster |
NULL issue | No NULL issue |

------------------------------------------------------------------------

## 🧠 6. SUBQUERY vs JOIN


| USE SUBQUERY WHEN | USE JOIN WHEN |
|-------------------|---------------|
Comparing with aggregate | Need columns from multiple tables |
Existence check | Performance critical |
Nested condition | Faster for large datasets |

------------------------------------------------------------------------

## 🧠 7. COMMON INTERVIEW QUESTIONS

-   2nd highest salary
-   Employees earning above average
-   Department with highest avg salary
-   Customers who placed orders
-   Products never sold

------------------------------------------------------------------------

## 🧠 8. PERFORMANCE NOTE

Correlated subquery = slow
Often replaced with JOIN + GROUP BY

------------------------------------------------------------------------

## 🧠 9. COMMON MISTAKES

❌ Using = with multi-row subquery\
❌ NULL issue with NOT IN\
❌ Missing alias in FROM subquery

------------------------------------------------------------------------

## 🧠 10. NOT IN vs NOT EXISTS ⭐


| NOT IN | NOT EXISTS |
|--------|------------|
Fails if NULL exists | Works correctly |

------------------------------------------------------------------------

# 🏁 FINAL SUMMARY

## Subquery Types:

1.  Single row
2.  Multi row
3.  Correlated
4.  In SELECT
5.  In FROM

## Operators:

IN / ANY / ALL / EXISTS / NOT EXISTS


# Practice 

## 🗄️ 1. CREATE DATABASE
```sql 
CREATE DATABASE sql_practice;
USE sql_practice;
```
## 🧱 2. CREATE TABLES

```
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);
```
```
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    salary INT,
    dept_id INT,
    manager_id INT,
    hire_date DATE
);
```
```
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    marks INT,
    course_id INT
);
```
```
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50)
);
```
```
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(50)
);
```
```
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    amount INT
);
```

## 🧾 3. INSERT DATA
```
INSERT INTO departments VALUES
(1,'IT'), (2,'HR'), (3,'Sales'), (4,'Admin');
```
```
INSERT INTO employees VALUES
(101,'Amit',60000,1,NULL,'2022-01-10'),
(102,'Neha',55000,1,101,'2022-02-15'),
(103,'Raj',70000,2,NULL,'2021-03-12'),
(104,'Simran',45000,2,103,'2023-07-01'),
(105,'Karan',80000,3,NULL,'2020-06-20'),
(106,'Pooja',50000,3,105,'2022-08-18'),
(107,'Rohit',40000,4,NULL,'2023-01-11');
```
```
INSERT INTO courses VALUES
(1,'Java'),(2,'Python'),(3,'SQL');
```
```
INSERT INTO students VALUES
(1,'Ankit',85,1),
(2,'Meera',90,2),
(3,'John',70,1),
(4,'Sara',88,3),
(5,'Riya',95,2);
```
```
INSERT INTO customers VALUES
(1,'Rahul'),(2,'Sneha'),(3,'Arjun'),(4,'Priya');
```
```
INSERT INTO orders VALUES
(101,1,5000),
(102,1,7000),
(103,2,3000);
```

# 🧠 SQL SUBQUERY PRACTICE QUESTIONS

---

## 🟢 BASIC (1–15)

1. Find employees earning more than average salary  
2. Find employee with highest salary  
3. Find employee with lowest salary  
4. Find students scoring above average marks  
5. Find students scoring below average marks  
6. Find departments having employees  
7. Find departments with no employees  
8. Find customers who placed orders  
9. Find customers who never placed orders  
10. Find courses with enrolled students  
11. Find courses with no students  
12. Find employees hired after the last hired employee in HR  
13. Find employees earning more than Amit  
14. Find students who scored equal to highest marks  
15. Find employees whose salary = department average  

---

## 🟡 INTERMEDIATE (16–30)

16. Find 2nd highest salary  
17. Find top 3 highest salaries using subquery  
18. Find employees earning more than their department average  
19. Find department with highest average salary  
20. Find department with lowest average salary  
21. Find employees working in department with highest avg salary  
22. Find students who scored highest in each course  
23. Find employees not working in IT department  
24. Find employees earning more than all HR employees  
25. Find employees earning more than any HR employee  
26. Find employees whose salary is greater than overall average but less than max  
27. Find managers (employees who have subordinates)  
28. Find employees who are not managers  
29. Find employees whose salary is greater than their manager  
30. Find customers who placed more than one order  

---

## 🔴 ADVANCED (31–50)

31. Find nth highest salary  
32. Find duplicate salaries  
33. Find employees with same salary as Amit  
34. Find employees working in same department as Raj  
35. Find employees in department with no manager  
36. Find highest paid employee in each department  
37. Find employees hired before department average hire date  
38. Find employees who earn the maximum in their department  
39. Find departments where avg salary > company avg salary  
40. Find employees earning less than company average but highest in their dept  
41. Find students who scored more than all students in Java  
42. Find students who scored less than any student in Python  
43. Find customers who placed orders above average order amount  
44. Find customers whose total order amount is maximum  
45. Find employees whose salary is in top 10%  
46. Find employees with salary greater than median salary  
47. Find department having maximum number of employees  
48. Find employees working in the department with minimum employees  
49. Find employees whose salary is same as department minimum  
50. Find employees whose salary is not in the list of department salaries  

---

# 🚀 HOW TO USE

✅ Solve using **subqueries**  
✅ Rewrite using **JOIN**  
✅ Compare performance  
