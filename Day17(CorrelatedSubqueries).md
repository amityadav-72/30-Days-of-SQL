# DAY 17 --- Correlated Subqueries

## 1️⃣ What is a Correlated Subquery?

A **correlated subquery** is a subquery that **depends on the outer
query for its values**.

That means:

-   The inner query **cannot run independently first**
-   The inner query **uses values from the outer query**
-   The inner query **runs once for every row of the outer query**

✅ This is the biggest difference from a normal subquery.

------------------------------------------------------------------------

## 2️⃣ Normal Subquery vs Correlated Subquery

### Normal Subquery

``` sql
SELECT emp_name
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

### Execution Process

The inner query runs only **once**:

``` sql
SELECT AVG(salary) FROM employees;
```

Suppose average salary = **55000**

Then outer query becomes:

``` sql
SELECT emp_name
FROM employees
WHERE salary > 55000;
```

So every row is compared with one fixed value.

------------------------------------------------------------------------

## 3️⃣ Correlated Subquery

``` sql
SELECT emp_name
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE dept_id = e.dept_id
);
```

Here:

``` sql
e.dept_id
```

comes from the outer query.

So the inner query depends on the current outer row.

------------------------------------------------------------------------

## 4️⃣ Why It Is Called Correlated?

Because:

The inner query is directly linked (correlated) with the outer query.

Without outer row values, the inner query cannot execute properly.

------------------------------------------------------------------------

## 5️⃣ Execution Process (Very Important)

Suppose the `employees` table is:

| emp_name | salary | dept_id |
|----------|--------|---------|
| Amit     | 50000  | 10      |
| Neha     | 70000  | 10      |
| Raj      | 60000  | 20      |

------------------------------------------------------------------------

### Query

``` sql
SELECT emp_name
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE dept_id = e.dept_id
);
```

------------------------------------------------------------------------

### Step-by-Step Execution

### Row 1 → Amit

Outer row:

``` sql
dept_id = 10
```

Inner query becomes:

``` sql
SELECT AVG(salary)
FROM employees
WHERE dept_id = 10;
```

Average = **60000**

Comparison:

``` sql
50000 > 60000 → false
```

❌ Amit not selected

------------------------------------------------------------------------

### Row 2 → Neha

Again inner query runs:

``` sql
SELECT AVG(salary)
FROM employees
WHERE dept_id = 10;
```

Average = **60000**

Comparison:

``` sql
70000 > 60000 → true
```

✅ Neha selected

------------------------------------------------------------------------

### Row 3 → Raj

Inner query:

``` sql
SELECT AVG(salary)
FROM employees
WHERE dept_id = 20;
```

Average = **60000**

Comparison:

``` sql
60000 > 60000 → false
```

❌ Raj not selected

------------------------------------------------------------------------

## Final Result

``` text
Neha
```

------------------------------------------------------------------------

## 6️⃣ Key Rule

A correlated subquery runs:

✅ **For every outer row**

That is why correlated subqueries can be slower on large tables.

------------------------------------------------------------------------

## 7️⃣ General Syntax Pattern

``` sql
SELECT outer_columns
FROM table1 outer_alias
WHERE condition (
    SELECT aggregate
    FROM table2
    WHERE inner_column = outer_alias.column
);
```

------------------------------------------------------------------------

## 8️⃣ Most Common Real Interview Use Cases

### Find employees earning above department average

``` sql
SELECT emp_name
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE dept_id = e.dept_id
);
```

------------------------------------------------------------------------

### Find products priced above category average

``` sql
SELECT product_name
FROM products p
WHERE price > (
    SELECT AVG(price)
    FROM products
    WHERE category_id = p.category_id
);
```

------------------------------------------------------------------------

### Find students scoring above class average

``` sql
SELECT student_name
FROM students s
WHERE marks > (
    SELECT AVG(marks)
    FROM students
    WHERE class_id = s.class_id
);
```

------------------------------------------------------------------------

## 9️⃣ Interview Difference (Very Frequently Asked)

  Type                  Inner Query Runs
  --------------------- ------------------
  Normal Subquery       Once
  Correlated Subquery   Multiple Times

------------------------------------------------------------------------

## 🔟 Performance Note

Correlated subqueries are slower because:

-   Every outer row triggers inner query execution
-   Large tables cause repeated scanning

✅ In interviews they often ask how to convert correlated subqueries
into JOINs.

------------------------------------------------------------------------

## 1️⃣1️⃣ Equivalent JOIN Idea

Correlated version:

``` sql
SELECT emp_name
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE dept_id = e.dept_id
);
```

JOIN version uses:

-   `GROUP BY`
-   `JOIN`

We study that separately later.

------------------------------------------------------------------------

## 1️⃣2️⃣ Common Mistakes

❌ Forgetting alias

❌ Not linking inner query to outer query

❌ Wrong outer alias reference

------------------------------------------------------------------------

## 1️⃣3️⃣ Practice Thinking Question

``` sql
SELECT student_name
FROM students s
WHERE marks > (
    SELECT AVG(marks)
    FROM students
    WHERE section = s.section
);
```

------------------------------------------------------------------------

## ✅ Answer: What Does This Query Find?

This query finds:

**Students whose marks are greater than the average marks of their own
section.**

------------------------------------------------------------------------

### Step-by-Step Logic

For each student:

1.  Take student's section
2.  Calculate average marks of that section
3.  Compare student's marks with section average
4.  If marks are greater → select student

------------------------------------------------------------------------

## Example

  student_name   marks   section
  -------------- ------- ---------
  Amit           80      A
  Neha           90      A
  Raj            70      B

------------------------------------------------------------------------

### For Amit

Section A average:

``` text
(80 + 90) / 2 = 85
```

Compare:

``` text
80 > 85 → false
```

❌ Not selected

------------------------------------------------------------------------

### For Neha

``` text
90 > 85 → true
```

✅ Selected

------------------------------------------------------------------------

### For Raj

Section B average:

``` text
70
```

Compare:

``` text
70 > 70 → false
```

❌ Not selected

------------------------------------------------------------------------

## Final Result

``` text
Neha
```

------------------------------------------------------------------------

## ✅ Core Memory Trick

Think:

> **Outer row gives value → inner query recalculates → compare**

That is the heart of correlated subqueries.

------------------------------------------------------------------------


# 📅 Day 17 — Correlated Subquery Practice (50 Questions)

## 🟢 BASIC LEVEL (1–15)

1. Find employees whose salary is greater than the average salary of their department.  
2. Find students whose marks are higher than the average marks of their class.  
3. Find products whose price is greater than the average price of their category.  
4. Find employees whose salary is less than the average salary of their department.  
5. Find students scoring below the average marks of their section.  
6. Find products cheaper than the average price of their category.  
7. Find employees whose salary equals the maximum salary in their department.  
8. Find students whose marks equal the highest marks in their class.  
9. Find products whose price equals the minimum price in their category.  
10. Find employees hired after the latest hire date in their department.  
11. Find students who enrolled after the first enrollment date of their course.  
12. Find products added after the earliest product in their category.  
13. Find employees earning exactly the department average salary.  
14. Find students whose marks equal the class average.  
15. Find products whose price equals category average price.  

## 🟡 INTERMEDIATE LEVEL (16–30)

16. Find employees whose salary is greater than every employee in their own department except themselves.  
17. Find students scoring higher than every student in their section except themselves.  
18. Find products priced above all products in their category except themselves.  
19. Find employees whose salary is lower than all other employees in their department.  
20. Find students with the second highest marks in their class using correlated logic.  
21. Find products with second highest price in each category.  
22. Find employees whose salary is greater than department minimum but less than department maximum.  
23. Find students whose marks lie between section average and section maximum.  
24. Find products whose price lies between category average and category max.  
25. Find employees whose salary is above department average and hired after department average joining date.  
26. Find students whose marks are above class average and attendance above class average.  
27. Find products priced above category average and stock above category average.  
28. Find employees who belong to departments where average salary exceeds company average.  
29. Find students belonging to sections where average marks exceed school average.  
30. Find products belonging to categories where average price exceeds overall average.  

## 🟠 ADVANCED LEVEL (31–40)

31. Find employees earning more than their manager.  
32. Find employees whose salary is greater than the average salary of employees under the same manager.  
33. Find students whose marks exceed the average marks of students enrolled in the same course.  
34. Find products priced above the average price of products sold in the same month.  
35. Find customers whose order amount exceeds their own average order amount.  
36. Find orders whose amount exceeds customer average order amount.  
37. Find employees whose salary exceeds department average but not company maximum.  
38. Find students whose marks exceed section average but not class maximum.  
39. Find products priced above category average but below company max price.  
40. Find employees hired earlier than the average joining date of their department.  

## 🔴 HARD / INTERVIEW LEVEL (41–50)

41. Find highest paid employee in each department using correlated subquery.  
42. Find lowest scoring student in each class using correlated subquery.  
43. Find most expensive product in each category using correlated subquery.  
44. Find second highest paid employee in each department using correlated logic only.  
45. Find second highest scoring student in each class.  
46. Find second most expensive product in each category.  
47. Find employees whose salary is greater than all employees in departments other than their own.  
48. Find students whose marks exceed all students in other classes.  
49. Find products whose price exceeds all products in other categories.  
50. Find departments where every employee earns above company average.  
