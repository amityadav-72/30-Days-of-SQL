# 📅 DAY 18 — VIEWS (DETAILED MASTER THEORY)

---

# 🧠 1. INTRODUCTION TO VIEWS

A **VIEW** in SQL is a **virtual table** created using a query.

It does NOT store data physically.
Instead, it stores a SQL query.

Whenever you access the view, the database executes the stored query.

---

# 🔑 KEY CONCEPT

VIEW = STORED QUERY  
NOT STORED DATA

---

# 🧠 2. HOW VIEW WORKS INTERNALLY

When you run:

```
SELECT * FROM view_name;

```
Database internally runs:

```
SELECT columns FROM base_table;

```
So:
- View is just a layer
- Data always comes from base tables

---

# 🧠 3. WHY WE USE VIEWS

## 🔹 1. Query Simplification

Instead of writing complex queries repeatedly:

JOIN + GROUP BY + WHERE

You can create a view once and reuse it.

---

## 🔹 2. SECURITY

You can restrict access to:
- Specific columns
- Specific rows

Example:
CREATE VIEW emp_public AS
SELECT name, dept FROM employees;

👉 Salary is hidden

---

## 🔹 3. DATA ABSTRACTION

Users don't need to know:
- Table structure
- Complex joins
- Database design

---

## 🔹 4. REUSABILITY

Write once, use many times.

---

## 🔹 5. LOGICAL LAYER

Views act like:
👉 API layer between user and database

---

# 🧠 4. TYPES OF VIEWS

## 🔶 4.1 SIMPLE VIEW

- Based on single table
- No joins
- No aggregates

Example:
```
CREATE VIEW emp_view AS
SELECT name, salary FROM employees;
```

### ✅ Properties
- Updatable
- Fast
- Easy to manage

---

## 🔶 4.2 COMPLEX VIEW

- Uses joins
- Uses GROUP BY
- Uses aggregate functions

Example:
```
CREATE VIEW emp_dept AS
SELECT e.name, d.dept_name
FROM employees e
JOIN departments d
ON e.dept_id = d.id;
```

### ❌ Properties
- Not updatable
- Slower
- Complex

---

## 🔶 4.3 MATERIALIZED VIEW

- Stores data physically
- Needs refresh

| Feature | View | Materialized View |
|--------|------|------------------|
| Stores Data | ❌ | ✅ |
| Speed | Slow | Fast |
| Update | Automatic | Manual |

---

## 🔶 4.4 INLINE VIEW

Subquery inside FROM clause

Example:
```
SELECT * FROM (
    SELECT dept, AVG(salary) avg_sal
    FROM employees
    GROUP BY dept
) temp;
```
---

## 🔶 4.5 UPDATABLE VIEW

Conditions:
- Single table
- No DISTINCT
- No GROUP BY
- No aggregate

---

## 🔶 4.6 NON-UPDATABLE VIEW

If contains:
- JOIN
- GROUP BY
- SUM, AVG
- DISTINCT

---

# 🧠 5. CREATE VIEW SYNTAX

## Basic
```
CREATE VIEW view_name AS
SELECT * FROM table;
```

## With condition
```
CREATE VIEW high_salary AS
SELECT * FROM employees WHERE salary > 50000;
```
## With join
```
CREATE VIEW emp_dept AS
SELECT e.name, d.dept
FROM employees e
JOIN departments d
ON e.dept_id = d.id;
```

## With column alias
```
CREATE VIEW emp_view (name, pay) AS
SELECT emp_name, salary
FROM employees;
```
---

# 🧠 6. OPERATIONS ON VIEW

## SELECT
```
SELECT * FROM view_name;
```
## INSERT
```
INSERT INTO view_name VALUES (...);
```
## UPDATE
```
UPDATE view_name SET col = value;
```
## DELETE
```
DELETE FROM view_name WHERE condition;
```

⚠ All changes affect base table

---

# 🧠 7. DROP VIEW
```
DROP VIEW view_name;
```
---

# 🧠 8. ALTER VIEW
```
CREATE OR REPLACE VIEW view_name AS
SELECT ...;
```
---

# 🧠 9. CHECK OPTION

Prevents invalid insert/update

Example:
```
CREATE VIEW it_emp AS
SELECT * FROM employees WHERE dept = 10
WITH CHECK OPTION;
```
---

# 🧠 10. PERFORMANCE

## Normal View
- No data stored
- Query runs every time

## Complex View
- Slow if:
  - Joins
  - Aggregates

---

# 🧠 11. VIEW vs TABLE vs CTE

| Feature | View | Table | CTE |
|--------|------|------|-----|
| Stored | ❌ | ✅ | ❌ |
| Temporary | ❌ | ❌ | ✅ |
| Reusable | ✅ | ✅ | ❌ |
| Performance | Depends | Fast | Depends |

---

# 🧠 12. INDEXING WITH VIEWS

## Important Point
- Index is NOT created on normal view
- Index exists on base table

## Exception
Materialized view can be indexed

---

# 🧠 13. ADVANTAGES

- Security
- Reusability
- Simplification
- Abstraction

---

# 🧠 14. DISADVANTAGES

- Performance issues
- Dependency on base tables
- Limited updates

---

# 🧠 15. INTERVIEW QUESTIONS

Q1. What is a view?
→ Virtual table

Q2. Does view store data?
→ No

Q3. Can we update view?
→ Yes (simple view)

Q4. What is materialized view?
→ Stores data physically

---

# 🧠 16. REAL WORLD USE

- Dashboards
- Reports
- Data filtering
- Security layer

---

# 🧠 17. FINAL SUMMARY

- View is virtual
- View improves security
- View simplifies queries
- View is not storage
- View depends on base table

---


# 📅 DAY 18 — PRACTICE DATASET FOR VIEWS

---

## 🧠 DATABASE SETUP

We will use **3 tables**:
- employees  
- departments  
- locations  

---

# 🏢 1. CREATE TABLES

## 🔹 Employees Table

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    salary INT,
    dept_id INT,
    city VARCHAR(50),
    hire_date DATE
);
```

---

## 🔹 Departments Table

```sql
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50),
    location_id INT
);
```

---

## 🔹 Locations Table

```sql
CREATE TABLE locations (
    location_id INT PRIMARY KEY,
    city VARCHAR(50),
    state VARCHAR(50)
);
```

---

# 📊 2. INSERT DATA

## 🔹 Employees Data

```sql
INSERT INTO employees VALUES
(1, 'Amit', 60000, 1, 'Mumbai', '2022-01-15'),
(2, 'Riya', 45000, 2, 'Pune', '2021-06-10'),
(3, 'Karan', 70000, 1, 'Mumbai', '2020-03-20'),
(4, 'Neha', 52000, 3, 'Delhi', '2023-02-12'),
(5, 'Raj', 48000, 2, 'Pune', '2019-11-05'),
(6, 'Sneha', 80000, 4, 'Bangalore', '2022-07-19'),
(7, 'Arjun', 55000, 3, 'Delhi', '2021-09-25'),
(8, 'Pooja', 62000, 1, 'Mumbai', '2020-12-30'),
(9, 'Vikram', 40000, 2, 'Pune', '2023-05-18'),
(10, 'Anjali', 75000, 4, 'Bangalore', '2021-01-11'),
(11, 'Rohit', 53000, 3, 'Delhi', '2022-08-22'),
(12, 'Meena', 47000, 2, 'Pune', '2020-10-14'),
(13, 'Suresh', 90000, 4, 'Bangalore', '2018-04-01'),
(14, 'Priya', 61000, 1, 'Mumbai', '2023-03-03'),
(15, 'Deepak', 58000, 3, 'Delhi', '2021-07-07');
```

---

## 🔹 Departments Data

```sql
INSERT INTO departments VALUES
(1, 'IT', 101),
(2, 'HR', 102),
(3, 'Finance', 103),
(4, 'Marketing', 104);
```

---

## 🔹 Locations Data

```sql
INSERT INTO locations VALUES
(101, 'Mumbai', 'Maharashtra'),
(102, 'Pune', 'Maharashtra'),
(103, 'Delhi', 'Delhi'),
(104, 'Bangalore', 'Karnataka');
```

---

# 🔗 3. RELATIONSHIPS

- employees.dept_id → departments.dept_id  
- departments.location_id → locations.location_id  

---

# 🧪 4. TEST QUERY

```sql
SELECT e.emp_name, d.dept_name, l.city
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id
JOIN locations l ON d.location_id = l.location_id;
```

---

# 🎯 READY FOR PRACTICE

You can now:
- ✔ Create views  
- ✔ Practice joins  
- ✔ Use aggregates  
- ✔ Test updatable views  
- ✔ Build real-world queries  

---



## 🟢 LEVEL 1 — BASIC (1–15)
```
1. Create a view that shows all columns from the employees table.  

2. Create a view that shows only employee names and salaries.  

3. Create a view to display employees with salary greater than 50,000.  

4. Create a view to show employees from department 10.  

5. Retrieve all records from a created view.  

6. Create a view with column aliases (rename columns).  

7. Drop an existing view.  

8. Replace an existing view with new query logic.  

9. Create a view that filters employees based on city = 'Mumbai'.  

10. Create a view that shows employees hired after 2020.  

11. Create a view that selects distinct departments.  

12. Create a view using WHERE and ORDER BY.  

13. Check if a view reflects updated data in base table.  

14. Create multiple views on the same table.  

15. Use a view inside another SELECT query.  
```
---

## 🟡 LEVEL 2 — INTERMEDIATE (16–30)
```
16. Create a view using JOIN between employees and departments.  

17. Create a view that shows employee name with department name.  

18. Create a view with INNER JOIN and filter department = 'IT'.  

19. Create a view with LEFT JOIN showing all employees.  

20. Create a view with GROUP BY (department-wise average salary).  

21. Create a view using aggregate function SUM.  

22. Create a view using COUNT of employees per department.  

23. Create a view with HAVING clause.  

24. Try updating a simple view and observe behavior.  

25. Try updating a complex view and analyze error.  

26. Insert data using a simple view.  

27. Delete records using a view.  

28. Create a view with DISTINCT and test update behavior.  

29. Create nested view (view based on another view).  

30. Use a view inside a JOIN with another table.  
```
---

## 🔵 LEVEL 3 — ADVANCED (31–45)
```

31. Create a view with multiple joins (3 tables).  

32. Create a view combining employees, departments, and locations.  

33. Create a view with subquery inside SELECT.  

34. Create a view using correlated subquery.  

35. Create a view with CASE statement.  

36. Create a view that ranks employees using window functions.  

37. Create a view with ROW_NUMBER().  

38. Create a view using RANK() or DENSE_RANK().  

39. Create a view that filters top 5 highest salaries.  

40. Create a view using UNION of two tables.  

41. Create a view using UNION ALL.  

42. Create a view with nested aggregations.  

43. Create a view to identify duplicate records.  

44. Create a view that returns employees earning above department average.  

45. Create a view with multiple conditions and complex filtering.  
```
---

## 🔴 LEVEL 4 — EXPERT (46–50)
```

46. Create a view with WITH CHECK OPTION and test insert violation.  

47. Create a secure view hiding salary column for users.  

48. Design a reporting view for dashboard (multi-table + aggregation).  

49. Optimize a slow view (analyze joins and indexing).  

50. Compare performance of view vs direct query with EXPLAIN.
```

---

## 🧠 BONUS CHALLENGE

- Create a **complete HR dashboard view system**
- Include:
  - Employee details  
  - Department stats  
  - Salary insights  
  - Top performers  

---
