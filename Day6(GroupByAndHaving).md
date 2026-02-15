# 📊 SQL GROUP BY & HAVING

## 1️⃣ THEORY --- GROUP BY

### 🔹 What is GROUP BY?

`GROUP BY` is used to combine rows having the same value and apply
aggregate functions on each group.

📌 **In simple words:**

-   Without `GROUP BY` → whole table = **1 result**
-   With `GROUP BY` → each category = **1 result**

### 🔹 Example Meaning

If we group by `department`:

-   IT → one row
-   HR → one row
-   Finance → one row

### 🔹 Why do we use it?

-   Department-wise salary
-   City-wise employee count
-   Category-wise average
-   Report summaries

------------------------------------------------------------------------

## 2️⃣ GROUP BY --- SYNTAX + EXAMPLES

### 🔹 Basic GROUP BY

``` sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```

### ✅ Example

``` sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

🧠 Returns → number of employees in each department.

------------------------------------------------------------------------

### 🔹 GROUP BY with SUM

``` sql
SELECT department, SUM(salary)
FROM employees
GROUP BY department;
```

🧠 Returns → total salary of each department.

------------------------------------------------------------------------

### 🔹 GROUP BY with AVG

``` sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

🧠 Returns → average salary per department.

------------------------------------------------------------------------

### 🔹 GROUP BY with MIN / MAX

``` sql
SELECT department, MAX(salary)
FROM employees
GROUP BY department;
```

🧠 Returns → highest salary in each department.

------------------------------------------------------------------------

### 🔹 GROUP BY with WHERE

``` sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
WHERE condition
GROUP BY column_name;
```

``` sql
SELECT department, COUNT(*)
FROM employees
WHERE city = 'Mumbai'
GROUP BY department;
```

🧠 Returns → department-wise employee count only for Mumbai.

------------------------------------------------------------------------

### 🔹 GROUP BY Multiple Columns

``` sql
GROUP BY column1, column2;
```

``` sql
SELECT department, city, COUNT(*)
FROM employees
GROUP BY department, city;
```

🧠 Returns → employee count for each department in each city.

------------------------------------------------------------------------

## 3️⃣ HAVING CLAUSE

### 🔹 What is HAVING?

HAVING is used to filter grouped data.

📌 WHERE → filters rows
📌 HAVING → filters groups

------------------------------------------------------------------------

### 🔹 Syntax

``` sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

### 🔹 Example

``` sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 2;
```

🧠 Returns → departments having more than 2 employees.

------------------------------------------------------------------------

### 🔹 HAVING with SUM

``` sql
SELECT department, SUM(salary)
FROM employees
GROUP BY department
HAVING SUM(salary) > 100000;
```

🧠 Returns → departments whose total salary is greater than 100000.

------------------------------------------------------------------------

## 🔥 WHERE vs HAVING

| Feature             | WHERE                    | HAVING                 |
|---------------------|--------------------------|------------------------|
| Purpose             | Filters rows             | Filters groups         |
| Execution Order     | Used **before** GROUP BY | Used **after** GROUP BY|
| Aggregate Functions | ❌ Cannot use            | ✅ Can use             |
| Works on            | Individual rows          | Grouped result         |
| Used with           | SELECT, UPDATE, DELETE   | SELECT only            |
| Example Condition   | `salary > 50000`         | `COUNT(*) > 5`         |

------------------------------------------------------------------------

## ⭐ SQL Execution Order

FROM
→ WHERE
→ GROUP BY
→ HAVING
→ SELECT
→ ORDER BY

----

# 📊 SQL GROUP BY — Step-by-Step Visualization (Beginner Friendly)

This guide shows **what actually happens inside SQL** when we use:

- WHERE
- GROUP BY
- HAVING

We will move **step by step** using a small table.

---

## 🧾 Original Table — `employees`

| emp_id | name   | department | city   | salary |
|--------|--------|------------|--------|--------|
| 1      | Amit   | IT         | Mumbai | 60000  |
| 2      | Neha   | HR         | Pune   | 40000  |
| 3      | Raj    | IT         | Mumbai | 70000  |
| 4      | Simran | Finance    | Delhi  | 50000  |
| 5      | Karan  | IT         | Pune   | 65000  |
| 6      | Pooja  | HR         | Mumbai | 45000  |

---

# 🔹 STEP 1 — WHERE (Filters Rows First)

### 🧠 Meaning:
`WHERE` removes the rows that do not match the condition.

### ✅ Query

```sql
SELECT *
FROM employees
WHERE city = 'Mumbai';
```
###  Result

| emp_id | name  | department | city   | salary |
|--------|-------|------------|--------|--------|
| 1      | Amit  | IT         | Mumbai | 60000  |
| 3      | Raj   | IT         | Mumbai | 70000  |
| 6      | Pooja | HR         | Mumbai | 45000  |

👉 All non-Mumbai rows are removed.

## 🔹 STEP 2 — GROUP BY (Creates Groups)

### 🧠 Meaning

`GROUP BY` puts similar values into groups.

### ✅ Query

```
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```
🧠 Internally SQL makes groups like this
1. IT Group
- Amit, Raj, Karan

2. HR Group
- Neha, Pooja

3. Finance Group
- Simran

## ✅ Final Output
| department | count |
|------------|-------|
| IT         | 3     |
| HR         | 2     |
| Finance    | 1     |

👉 One row per department.

## 🔹 STEP 3 — HAVING (Filters Groups)
🧠 Meaning
HAVING removes entire groups based on a condition.

### ✅ Query
```
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 2;
```
🧠 After GROUP BY
| department | count |
|------------|-------|
| IT         | 3     |
| HR         | 2     |
| Finance    | 1     |

🧠 After HAVING
| department | count |
|------------|-------|
| IT         | 3     |

👉 Only the group that matches the condition remains.

## 🎯 FULL FLOW — WHERE → GROUP BY → HAVING
✅ Query
```
SELECT department, COUNT(*)
FROM employees
WHERE city = 'Mumbai'
GROUP BY department
HAVING COUNT(*) > 1;
```
## 🧠 Step 1 — WHERE

### Only Mumbai employees:

| name  | department |
|-------|------------|
| Amit  | IT         |
| Raj   | IT         |
| Pooja | HR         |

---

## 🧠 Step 2 — GROUP BY

IT → 2 employees  
HR → 1 employee  

---

## 🧠 Step 3 — HAVING

**Condition:** `COUNT(*) > 1`

IT → ✅ Keep  
HR → ❌ Remove  

---

## ✅ Final Output

| department | count |
|------------|-------|
| IT         | 2     |

---

# ⭐ SQL Execution Order (Very Important)

SQL does **NOT** run from top to bottom.

## ✅ Actual execution order
```
FROM
WHERE
GROUP BY
HAVING
SELECT
ORDER BY
```

- Data comes from → `FROM`

- Row filtering → `WHERE`

- Groups are created → `GROUP BY`

- Group filtering → `HAVING`

- Columns selected → `SELECT`

Final sorting → ORDER BY
--------

# 📊 SQL GROUP BY Practice Questions

## 🟢 LEVEL 1 — BASIC GROUP BY (1–10)

1. Count employees in each department  
2. Count employees in each city  
3. Find total salary of each department  
4. Find average salary of each department  
5. Find minimum salary in each department  
6. Find maximum salary in each department  
7. Count employees in each city  
8. Find total salary of each city  
9. Find average salary of each city  
10. Find highest salary in each city  

---

## 🟢 LEVEL 2 — GROUP BY + ORDER BY (11–15)

11. Count employees in each department and sort by count descending  
12. Total salary of each department sorted from highest to lowest  
13. Average salary of each city sorted ascending  
14. Maximum salary of each department sorted descending  
15. Count employees in each city sorted alphabetically  

---

## 🟢 LEVEL 3 — GROUP BY + WHERE (16–20)

16. Count employees in each department from Mumbai  
17. Total salary of each department where city is Delhi  
18. Average salary of each department where salary > 50000  
19. Count employees in each city where department is IT  
20. Maximum salary in each city where department is HR  

---

## 🟢 LEVEL 4 — HAVING (21–30)

21. Departments having more than 1 employee  
22. Cities having more than 2 employees  
23. Departments where total salary > 100000  
24. Departments where average salary > 50000  
25. Cities where maximum salary > 60000  
26. Departments where minimum salary < 40000  
27. Cities having total salary greater than 120000  
28. Departments having more than 2 employees from Mumbai  
29. Cities where average salary is less than 50000  
30. Departments where highest salary is greater than 65000  

---

## 🟢 LEVEL 5 — MULTIPLE COLUMN GROUP BY (31–35)

31. Count employees by department and city  
32. Find total salary by department and city  
33. Find average salary by department and city  
34. Find maximum salary by department and city  
35. Find minimum salary by department and city  

---

## 🟢 LEVEL 6 — MIXED (36–45)

36. Count employees in each department where city is not NULL  
37. Total salary of each department except HR  
38. Average salary of each city for IT department  
39. Maximum salary in each department for Mumbai employees  
40. Minimum salary in each city where salary > 40000  
41. Department-wise employee count sorted by department name  
42. City-wise total salary sorted descending  
43. Department-wise average salary sorted ascending  
44. Cities having more than 1 employee from HR  
45. Departments where total salary is between 90000 and 150000  

---

## 🟢 LEVEL 7 — INTERVIEW LEVEL THINKING (46–50)

46. Department having highest total salary  
47. City having lowest average salary  
48. Department with maximum number of employees  
49. City with highest salary paid  
50. Departments where average salary is greater than overall average salary  

--- 
