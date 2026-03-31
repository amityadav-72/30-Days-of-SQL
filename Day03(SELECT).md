# 📘 SQL DAY 3 --- SELECT CORE COMMANDS

## FULL THEORY + PRACTICE + INTERVIEW GUIDE

------------------------------------------------------------------------

## 🎯 DAY 3 --- LEARNING OBJECTIVE

Today you learn the **core data retrieval tools in SQL**.

These commands are used in almost every SQL query and are **frequently
asked in interviews**.

You will master:

-   SELECT
-   WHERE
-   AND / OR / NOT
-   DISTINCT
-   ORDER BY
-   LIMIT

------------------------------------------------------------------------

# 1️⃣ SELECT COMMAND

## ✅ Purpose

Used to **retrieve (fetch) data from a table**.

-   Does NOT modify data
-   Read-only operation
-   Most frequently used SQL command

------------------------------------------------------------------------

## ✅ Basic Syntax

``` sql
SELECT column_name
FROM table_name;
```

## ✅ Example

``` sql
SELECT name FROM employees;
```

Shows only employee names.

------------------------------------------------------------------------

## ✅ Select Multiple Columns

``` sql
SELECT name, salary
FROM employees;
```

------------------------------------------------------------------------

## ✅ Select All Columns

``` sql
SELECT *
FROM employees;
```

-   means everything.

------------------------------------------------------------------------

## 🧠 Important Notes

-   Safe command (no data modification)
-   Can retrieve specific columns
-   Can be combined with filtering and sorting

------------------------------------------------------------------------

# 2️⃣ WHERE CLAUSE

## ✅ Purpose

Used to filter rows based on a condition.

------------------------------------------------------------------------

## ✅ Syntax

``` sql
SELECT columns
FROM table
WHERE condition;
```

------------------------------------------------------------------------

## ✅ Example

``` sql
SELECT * FROM employees
WHERE department = 'IT';
```

Shows only IT employees.

------------------------------------------------------------------------

## ✅ Comparison Operators

| Operator | Meaning |
|---|---|
| = | Equal |
| > | Greater than |
| < | Less than |
| >= | Greater or equal |
| <= | Less or equal |
| <> or != | Not equal |


------------------------------------------------------------------------

## 🧠 Important Notes

-   Filters rows
-   Works with numbers and text
-   Essential for conditional retrieval

------------------------------------------------------------------------

# 3️⃣ AND OPERATOR

## ✅ Purpose

All conditions must be TRUE.

------------------------------------------------------------------------

## ✅ Syntax

``` sql
SELECT columns
FROM table
WHERE condition1 AND condition2;
```

------------------------------------------------------------------------

## ✅ Example

``` sql
SELECT * FROM employees
WHERE department = 'IT'
AND city = 'Mumbai';
```

------------------------------------------------------------------------

# 4️⃣ OR OPERATOR

## ✅ Purpose

At least ONE condition must be TRUE.

------------------------------------------------------------------------

## ✅ Syntax

``` sql
SELECT columns
FROM table
WHERE condition1 OR condition2;
```

------------------------------------------------------------------------

## ✅ Example

``` sql
SELECT * FROM employees
WHERE city = 'Mumbai'
OR city = 'Delhi';
```

------------------------------------------------------------------------

# 5️⃣ NOT OPERATOR

## ✅ Purpose

Reverses condition.

------------------------------------------------------------------------

## ✅ Syntax

``` sql
SELECT columns
FROM table
WHERE NOT condition;
```

------------------------------------------------------------------------

## ✅ Example

``` sql
SELECT * FROM employees
WHERE NOT department = 'HR';
```

------------------------------------------------------------------------

# 6️⃣ DISTINCT KEYWORD

## ✅ Purpose

Removes duplicate values and shows unique results.

------------------------------------------------------------------------

## ✅ Syntax

``` sql
SELECT DISTINCT column_name
FROM table_name;
```

------------------------------------------------------------------------

## ✅ Example

``` sql
SELECT DISTINCT department
FROM employees;
```

------------------------------------------------------------------------

# 7️⃣ ORDER BY (SORTING)

## ✅ Purpose

Sorts result set.

------------------------------------------------------------------------

## ✅ Syntax

``` sql
SELECT columns
FROM table
ORDER BY column_name ASC;
```

``` sql
SELECT columns
FROM table
ORDER BY column_name DESC;
```

------------------------------------------------------------------------

## ✅ Example

``` sql
SELECT * FROM employees
ORDER BY salary DESC;
```

------------------------------------------------------------------------

## ✅ Multiple Column Sorting

``` sql
SELECT columns
FROM table
ORDER BY column1, column2 DESC;
```

Example:

``` sql
SELECT * FROM employees
ORDER BY city, salary DESC;
```

------------------------------------------------------------------------

# 8️⃣ LIMIT CLAUSE

## ✅ Purpose

Restricts number of rows returned.

------------------------------------------------------------------------

## ✅ Syntax

``` sql
SELECT columns
FROM table
LIMIT number;
```

------------------------------------------------------------------------

## ✅ Example

``` sql
SELECT * FROM employees
LIMIT 5;
```

------------------------------------------------------------------------

## ✅ LIMIT with ORDER BY (Top N Records)

``` sql
SELECT columns
FROM table
ORDER BY column_name DESC
LIMIT number;
```

Example:

``` sql
SELECT * FROM employees
ORDER BY salary DESC
LIMIT 3;
```

------------------------------------------------------------------------


# 🧪 DAY 3 PRACTICE QUESTIONS

----
## Create Database
```
CREATE DATABASE employee_practice;

USE employee_practice;
```

## Create Table 
```
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(50),
    salary INT,
    city VARCHAR(50)
);
```

## Insert Sample Data
```
INSERT INTO employees VALUES
(1, 'Amit', 'IT', 60000, 'Mumbai'),
(2, 'Neha', 'HR', 45000, 'Delhi'),
(3, 'Rahul', 'Finance', 55000, 'Mumbai'),
(4, 'Pooja', 'IT', 70000, 'Delhi'),
(5, 'Suresh', 'HR', 38000, 'Pune'),
(6, 'Kavita', 'IT', 75000, 'Delhi'),
(7, 'Ankit', 'HR', 42000, 'Pune'),
(8, 'Ramesh', 'Finance', 54000, 'Mumbai'),
(9, 'Priya', 'IT', 48000, 'Pune'),
(10, 'Mohit', 'Finance', 58000, 'Mumbai'),
(11, 'Sneha', 'HR', 62000, 'Delhi'),
(12, 'Vikas', 'IT', 52000, 'Pune'),
(13, 'Arjun', 'Finance', 61000, 'Delhi'),
(14, 'Deepak', 'IT', 40000, 'Mumbai'),
(15, 'Nisha', 'HR', 47000, 'Pune');
```

---

## 🟢 LEVEL 1 — BASIC SELECT
```
1. Show all employee records  
2. Show only employee names  
3. Show name and salary  
4. Show emp_id, name, and city  
5. Show department and salary only  
```
---


## 🟢 LEVEL 2 — WHERE CONDITIONS
```
6. Show employees from IT department  
7. Show employees from Mumbai  
8. Show employees whose salary > 50000  
9. Show employees whose salary < 45000  
10. Show employees whose salary = 60000  
```
---

## 🟢 LEVEL 3 — AND CONDITIONS
```
11. Employees from IT AND Mumbai  
12. HR employees salary > 40000  
13. Finance employees in Delhi  
14. Salary > 50000 AND city Pune  
15. IT employees salary > 60000  
```
---

## 🟢 LEVEL 4 — OR CONDITIONS
```
16. Mumbai OR Delhi employees  
17. IT OR HR department  
18. Salary > 70000 OR city Pune  
19. Finance OR salary < 40000  
20. City Delhi OR HR  
```
---

## 🟢 LEVEL 5 — NOT CONDITIONS
```
21. Employees NOT in HR  
22. Employees NOT from Mumbai  
23. Salary NOT greater than 60000  
24. Employees NOT in Finance  
25. NOT Delhi AND salary > 50000  
```
---

## 🟢 LEVEL 6 — DISTINCT
```
26. Unique departments  
27. Unique cities  
28. Distinct department + city  
29. Unique salaries  
30. Count unique departments  
```
---

## 🟢 LEVEL 7 — ORDER BY
```
31. Salary ascending  
32. Salary descending  
33. Name alphabetical  
34. City then salary  
35. Highest salary first  
```
---

## 🟢 LEVEL 8 — LIMIT
```
36. First 3 employees  
37. Top 5 highest salaries  
38. Lowest salary employee  
39. Second highest salary  
40. Top 3 IT employees  
```
---

## 🟢 LEVEL 9 — MIXED PRACTICE
```
41. IT employees sorted by salary desc  
42. Mumbai employees salary > 50000 sorted by name  
43. Top 3 Finance salaries  
44. Not HR sorted by salary  
45. Distinct cities sorted  
```
---

## 🟢 LEVEL 10 — THINKING / INTERVIEW STYLE
```
46. Employee with max salary  
47. Employee with min salary  
48. Salary above average  
49. Same city as Amit  
50. Departments with more than one employee  
```
---

# 🎯 INTERVIEW QUESTIONS
```
1. Difference between WHERE and HAVING  
2. Difference between ORDER BY and GROUP BY  
3. SQL execution order  
4. How to find second highest salary  
5. How DISTINCT works internally  
6. Can WHERE be used without SELECT?  
7. Can ORDER BY be used without WHERE?  
8. Difference between AND and OR  
9. How to remove duplicate rows  
10. How to sort by multiple columns  
11. LIMIT vs TOP vs FETCH  
12. How to get top N records  
13. What is SQL execution plan  
14. Why SELECT is read-only  
15. How to filter multiple conditions efficiently  
```
---

Q 30 Solution 
```
SELECT count(DISTINCT dept) as unq_dept
FROM employees;
```

Q 39 Solution 
```
SELECT salary as second_highest FROM employees
ORDER BY salary ASC
LIMIT 1 OFFSET 1;

```
---


## 🔹 1️⃣ Salary Above Average

### ✅ Query
```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```
💡 Explanation
- Subquery finds the average salary

- Outer query returns employees earning more than average

## 🔹 2️⃣ Employees from Same City as Amit
✅ Query
```
SELECT *
FROM employees
WHERE city = (
    SELECT city
    FROM employees
    WHERE name = 'Amit'
);
```
### 💡 If multiple Amit exist → use this (safer)
```
SELECT *
FROM employees
WHERE city IN (
    SELECT city
    FROM employees
    WHERE name = 'Amit'
);
```
## 🔹 3️⃣ Departments with More Than One Employee
✅ Query
```
SELECT dept, COUNT(*) AS total_employees
FROM employees
GROUP BY dept
HAVING COUNT(*) > 1;
```
💡 Explanation
GROUP BY dept → creates department groups
HAVING COUNT(*) > 1 → filters groups with more than one employee

## 🔥 Interview Upgrade Version
Show full employee details from departments having more than 1 employee
```
SELECT *
FROM employees
WHERE dept IN (
    SELECT dept
    FROM employees
    GROUP BY dept
    HAVING COUNT(*) > 1
);
```

🚀 Placement Tip
These 3 cover concepts of:

Question	Concept
- Salary above average	Subquery + Aggregate
- Same city as Amit	Scalar subquery
- Dept > 1 employee	GROUP BY + HAVING
