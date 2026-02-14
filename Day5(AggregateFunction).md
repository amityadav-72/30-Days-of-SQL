# 📘 DAY 5 --- SQL AGGREGATE FUNCTIONS



Aggregate functions are used to perform calculations on multiple rows
and return a **single summarized value**.

------------------------------------------------------------------------

## 🔹 COUNT(*)

### 📖 Theory

Counts the **total number of rows** in a table, including rows that
contain NULL values.

### 🧾 Syntax

``` sql
SELECT COUNT(*) FROM table_name;
```

### 💡 Example

``` sql
SELECT COUNT(*) FROM employees;
```

### ✅ Result

Total number of records in the employees table.

------------------------------------------------------------------------

## 🔹 COUNT(column_name)

### 📖 Theory

Counts only **non-NULL values** in a specific column.

### 🧾 Syntax

``` sql
SELECT COUNT(column_name) FROM table_name;
```

### 💡 Example

``` sql
SELECT COUNT(city) FROM employees;
```

### ✅ Result

Number of employees whose city is not NULL.

------------------------------------------------------------------------

## 🔹 COUNT(DISTINCT column_name)

### 📖 Theory

Counts **unique non-NULL values** in a column.

### 🧾 Syntax

``` sql
SELECT COUNT(DISTINCT column_name) FROM table_name;
```

### 💡 Example

``` sql
SELECT COUNT(DISTINCT department) FROM employees;
```

### ✅ Result

Number of different departments.

------------------------------------------------------------------------
## 📊 COUNT() COMPARISON

| Function                | Counts NULL? | Counts Duplicate? | Purpose          |
|-------------------------|-------------|-------------------|------------------|
| COUNT(*)                | ✅ Yes      | ✅ Yes            | Total rows       |
| COUNT(column)           | ❌ No       | ✅ Yes            | Non-NULL values  |
| COUNT(DISTINCT column)  | ❌ No       | ❌ No             | Unique values    |


------------------------------------------------------------------------

## 🔹 SUM(column_name)

### 📖 Theory

Calculates the **total of a numeric column**.

### 🧾 Syntax

``` sql
SELECT SUM(column_name) FROM table_name;
```

### 💡 Example

``` sql
SELECT SUM(salary) FROM employees;
```

### ✅ Result

Total salary of all employees.

------------------------------------------------------------------------

## 🔹 AVG(column_name)

### 📖 Theory

Calculates the **average value** of a numeric column.

### 🧾 Syntax

``` sql
SELECT AVG(column_name) FROM table_name;
```

### 💡 Example

``` sql
SELECT AVG(salary) FROM employees;
```

### ✅ Result

Average salary of all employees.

⚠️ **AVG ignores NULL values**

------------------------------------------------------------------------

## 🔹 MIN(column_name)

### 📖 Theory

Returns the **smallest value** in a column.

### 🧾 Syntax

``` sql
SELECT MIN(column_name) FROM table_name;
```

### 💡 Example

``` sql
SELECT MIN(salary) FROM employees;
```

### ✅ Result

Lowest salary in the employees table.

------------------------------------------------------------------------

## 🔹 MAX(column_name)

### 📖 Theory

Returns the **largest value** in a column.

### 🧾 Syntax

``` sql
SELECT MAX(column_name) FROM table_name;
```

### 💡 Example

``` sql
SELECT MAX(salary) FROM employees;
```

### ✅ Result

Highest salary in the employees table.

------------------------------------------------------------------------
## 📊 AGGREGATE FUNCTION NULL BEHAVIOR

| Function        | Ignores NULLs? |
|-----------------|---------------|
| COUNT(*)        | ❌ No          |
| COUNT(column)   | ✅ Yes         |
| SUM()           | ✅ Yes         |
| AVG()           | ✅ Yes         |
| MIN()           | ✅ Yes         |
| MAX()           | ✅ Yes         |

------------------------------------------------------------------------

## 🔹 AGGREGATE WITH WHERE

### 📖 Theory

The `WHERE` clause filters rows **before aggregation**.

### 🧾 Syntax

``` sql
SELECT COUNT(*) 
FROM table_name 
WHERE condition;
```

### 💡 Example

``` sql
SELECT COUNT(*) 
FROM employees 
WHERE city = 'Mumbai';
```

### ✅ Result

Number of employees from Mumbai.

------------------------------------------------------------------------

## 🔹 MULTIPLE AGGREGATES IN ONE QUERY

### 🧾 Syntax

``` sql
SELECT 
COUNT(*),
SUM(column_name),
AVG(column_name),
MIN(column_name),
MAX(column_name)
FROM table_name;
```

### 💡 Example

``` sql
SELECT 
COUNT(*),
SUM(salary),
AVG(salary),
MIN(salary),
MAX(salary)
FROM employees;
```

### ✅ Result

| Metric            | Description            |
|-------------------|------------------------|
| Total Employees   | Number of rows         |
| Total Salary      | Sum of all salaries    |
| Average Salary    | Mean salary            |
| Lowest Salary     | Minimum salary         |
| Highest Salary    | Maximum salary         |


------------------------------------------------------------------------

## 🧠 INTERVIEW NOTES

### 🔸 Execution Order

FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY

### 🔸 Why WHERE cannot use aggregates?

Because WHERE executes **before aggregation**.

### 🔸 Use HAVING for aggregate filtering

``` sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

------------------------------------------------------------------------

## 🚀 SUMMARY TABLE

| Function | Purpose        |
|----------|---------------|
| COUNT()  | Count rows    |
| SUM()    | Total value   |
| AVG()    | Average value |
| MIN()    | Smallest value|
| MAX()    | Largest value |


------------------------------------------------------------------------

## ✅ REAL-WORLD USE CASES

-   Company total salary expense
-   Average employee salary
-   Highest paid employee
-   Number of departments
-   Employees per location

------------------------------------------------------------------------

# 🏁 DAY 5 Questions

------------------------------------------------------------------------

📘 Employees Practice Dataset
# 🔹 Create Table
```
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(50),
    city VARCHAR(50),
    salary INT
);
```

# 🔹 Insert Data
```
INSERT INTO employees VALUES
(1,  'Amit',     'IT',       'Mumbai',    60000),
(2,  'Neha',     'HR',       'Delhi',     45000),
(3,  'Raj',      'Finance',  'Mumbai',    70000),
(4,  'Sneha',    'IT',       'Pune',      52000),
(5,  'Karan',    'Sales',    'Delhi',     48000),
(6,  'Pooja',    'HR',       'Mumbai',    46000),
(7,  'Vikas',    'IT',       'Delhi',     75000),
(8,  'Rohit',    'Finance',  'Pune',      80000),
(9,  'Anjali',   'Sales',    'Mumbai',    49000),
(10, 'Suresh',   'IT',       'Delhi',     53000),
(11, 'Meena',    'HR',       'Pune',      47000),
(12, 'Arjun',    'Finance',  'Mumbai',    72000),
(13, 'Komal',    'Sales',    'Delhi',     51000),
(14, 'Nikhil',   'IT',       'Mumbai',    68000),
(15, 'Swati',    'HR',       'Delhi',     44000),
(16, 'Rahul',    'Finance',  'Pune',      66000),
(17, 'Ayesha',   'Sales',    'Mumbai',    50000),
(18, 'Manish',   'IT',       NULL,        61000),
(19, 'Sara',     'HR',       NULL,        43000),
(20, 'Tarun',    'Sales',    'Pune',      55000);
```

----------------------------

## 🟢 LEVEL 1 — COUNT()

1. Count total employees  
2. Count employees in IT  
3. Count employees in HR  
4. Count employees from Mumbai  
5. Count employees from Delhi  
6. Count employees whose salary > 50000  
7. Count employees whose salary < 45000  
8. Count distinct departments  
9. Count distinct cities  
10. Count employees where city is NULL  

---

## 🟢 LEVEL 2 — SUM()

1. Total salary of all employees  
2. Total salary of IT department  
3. Total salary of HR department  
4. Total salary of Mumbai employees  
5. Total salary of Delhi employees  
6. Total salary where salary > 50000  
7. Total salary where salary < 60000  
8. Total salary except HR  
9. Total salary of employees whose name starts with 'A'  
10. Total salary where city IN ('Mumbai', 'Delhi')  

---

## 🟢 LEVEL 3 — AVG()

1. Average salary of all employees  
2. Average salary of IT department  
3. Average salary of HR  
4. Average salary of Mumbai employees  
5. Average salary where salary > 45000  
6. Average salary where salary BETWEEN 40000 AND 70000  
7. Average salary except Finance  
8. Average salary of employees whose name starts with 'S'  
9. Average salary where city = 'Delhi'  
10. Average salary where department IN ('IT', 'HR')  

---

## 🟢 LEVEL 4 — MIN / MAX

1. Lowest salary in company  
2. Highest salary in company  
3. Lowest salary in IT  
4. Highest salary in HR  
5. Lowest salary in Mumbai  
6. Highest salary in Delhi  
7. Difference between max and min salary  
8. Minimum salary where salary > 40000  
9. Maximum salary where city = 'Mumbai'  
10. Highest salary except Finance  

---

## 🟢 LEVEL 5 — MIXED AGGREGATES

1. Total employees and total salary  
2. Average salary and total employees  
3. Max salary and min salary together  
4. Count employees and average salary in IT  
5. Total salary and highest salary in HR  
6. Count distinct departments and total salary  
7. Average salary and lowest salary in Mumbai  
8. Count employees whose name starts with 'A' and sum salary  
9. Total salary where department = 'IT' and city = 'Mumbai'  
10. Count employees whose salary between 40000 and 60000  

---

## 🎯 INTERVIEW QUESTIONS

1. Difference between COUNT(*) and COUNT(column)  
2. Why does AVG ignore NULL values?  
3. Can we use aggregate functions without GROUP BY?  
4. What is the execution order of a query with aggregates?  
5. Why can’t we use aggregate functions in WHERE?  
6. Difference between WHERE and HAVING  
7. Which aggregate function is fastest and why?  
8. Can MIN() / MAX() work on text columns?  
9. COUNT(1) vs COUNT(*)  
10. How to count NULL values in a column? 
---

## 🚀 Challenge Rule
Solve all queries using the **employees** table.

---
