
# 🧠 Multi-Table JOIN – Complete Guide

## 1️⃣ What is a Multi-Table JOIN?

Joining more than two tables in a single query.

### 📌 When do we use it?
When data is distributed across multiple related tables.

### 🎯 Real Example
Show:

- student name
- course name
- enrollment date

Tables involved:

- students
- enrollments
- courses

---

## 2️⃣ Basic Syntax

```sql
SELECT columns
FROM table1
JOIN table2 ON condition
JOIN table3 ON condition;
```

You can mix:

- INNER JOIN
- LEFT JOIN
- RIGHT JOIN

---

## 3️⃣ Execution Flow

Step 1 → A JOIN B → result  
Step 2 → result JOIN C  

➡ Joins execute left → right

---

## 4️⃣ Join Path (Very Important)

students → enrollments → courses  

This is called:

🔥 Join Path

Never join unrelated tables directly.

❌ students → courses  
✅ students → enrollments → courses

---

## 5️⃣ 3-Table JOIN Example

```sql
SELECT s.student_name, c.course_name, e.enroll_date
FROM students s
JOIN enrollments e
  ON s.student_id = e.student_id
JOIN courses c
  ON e.course_id = c.course_id;
```

---

## 6️⃣ 4-Table JOIN Example

```sql
SELECT cu.customer_name,
       o.order_id,
       p.product_name,
       s.amount
FROM customers cu
JOIN orders o
  ON cu.customer_id = o.customer_id
JOIN sales s
  ON o.order_id = s.order_id
JOIN products p
  ON s.product_id = p.product_id;
```

---

## 7️⃣ Mixing JOIN Types

Show all customers even if no orders

```sql
FROM customers cu
LEFT JOIN orders o ON ...
LEFT JOIN sales s ON ...
LEFT JOIN products p ON ...
```

---

## 8️⃣ Most Important Skill – Join Path Identification

Ask:

How are the tables connected?

---

## 9️⃣ Interview Scenario

```sql
SELECT e.emp_name,
       d.dept_name,
       m.emp_name AS manager
FROM employees e
LEFT JOIN departments d
  ON e.dept_id = d.dept_id
LEFT JOIN employees m
  ON e.manager_id = m.emp_id;
```

---

## 🔟 Multi JOIN + GROUP BY

```sql
SELECT cu.customer_name,
       SUM(s.amount) AS total_spent
FROM customers cu
JOIN orders o ON cu.customer_id = o.customer_id
JOIN sales s ON o.order_id = s.order_id
GROUP BY cu.customer_name;
```

---

## 1️⃣1️⃣ Multi JOIN + WHERE

Customers who bought Laptop

```sql
WHERE p.product_name = 'Laptop'
```

---

## 1️⃣2️⃣ Multi JOIN + HAVING

Customers who spent more than 50000

```sql
HAVING SUM(s.amount) > 50000
```

---

## 1️⃣3️⃣ Common Mistakes

❌ Joining wrong columns  
❌ Skipping bridge table  
❌ Cartesian product  
❌ Wrong join type  
❌ Ambiguous column names  

---

## 1️⃣4️⃣ Performance Tips

Indexes should exist on:

- Foreign keys
- Join columns

---

# 🏆 Most Asked Interview Patterns

✔ Customer total spending  
✔ Student course history  
✔ Product sales report  
✔ Employee hierarchy with department  
✔ Top selling product  

---

# 🎯 50 Multi-Table JOIN Practice Questions
# 1️⃣ CREATE TABLES

## 🎓 Students / Courses

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(100)
);

CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100),
    fee INT
);

CREATE TABLE enrollments (
    enroll_id INT PRIMARY KEY,
    student_id INT,
    course_id INT,
    enroll_date DATE
);
```

---

## 🛒 Customers / Orders / Products / Sales

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE
);

CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    price INT
);

CREATE TABLE sales (
    sale_id INT PRIMARY KEY,
    order_id INT,
    product_id INT,
    amount INT
);
```

---

## 🏢 Departments / Employees

```sql
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(100)
);

CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(100),
    salary INT,
    dept_id INT,
    manager_id INT
);
```

---

# 2️⃣ INSERT SAMPLE DATA

## 🎓 Students

```sql
INSERT INTO students VALUES
(1,'Amit'),
(2,'Neha'),
(3,'Rahul'),
(4,'Sneha'),
(5,'Karan');
```

## 📚 Courses

```sql
INSERT INTO courses VALUES
(101,'SQL',5000),
(102,'Python',7000),
(103,'Power BI',6000);
```

## 📝 Enrollments

```sql
INSERT INTO enrollments VALUES
(1,1,101,'2024-01-10'),
(2,1,102,'2024-02-15'),
(3,2,101,'2024-03-01'),
(4,3,103,'2024-01-20'),
(5,4,101,'2024-04-10');
```

---

## 👥 Customers

```sql
INSERT INTO customers VALUES
(1,'Raj'),
(2,'Simran'),
(3,'John'),
(4,'Sara');
```

## 📦 Orders

```sql
INSERT INTO orders VALUES
(101,1,'2024-01-01'),
(102,1,'2024-02-01'),
(103,2,'2024-03-05'),
(104,3,'2024-03-10');
```

---

## 🛍 Products

```sql
INSERT INTO products VALUES
(1,'Laptop',50000),
(2,'Mouse',500),
(3,'Keyboard',1500),
(4,'Monitor',12000);
```

## 💰 Sales

```sql
INSERT INTO sales VALUES
(1,101,1,50000),
(2,101,2,500),
(3,102,3,1500),
(4,103,1,50000),
(5,103,4,12000),
(6,104,2,500);
```

---

## 🏢 Departments

```sql
INSERT INTO departments VALUES
(1,'IT'),
(2,'HR'),
(3,'Finance');
```

## 👨‍💼 Employees

```sql
INSERT INTO employees VALUES
(1,'Amit',80000,1,NULL),
(2,'Neha',60000,1,1),
(3,'Rahul',55000,2,1),
(4,'Sneha',50000,2,3),
(5,'Karan',45000,3,1);
```

---

# 3️⃣ JOIN PATH REFERENCE

### 🎓 Student Queries
students → enrollments → courses

### 🛒 Customer Queries
customers → orders → sales → products

### 👨‍💼 Employee Queries
employees → departments → employees (manager)


## 🟢 BASIC (1–10)

1. Show student name and course name.
2. Show student name, course name, enroll date.
3. Show customer name and order date.
4. Show order id and product name.
5. Show product name and amount.
6. Show employee name and department name.
7. Show employee name and manager name.
8. Show sales with product price.
9. Show customers who placed orders.
10. Show students enrolled in any course.

---

## 🟡 INTERMEDIATE (11–25)

11. Show number of courses per student.  
12. Show number of students per course.  
13. Show total amount spent by each customer.  
14. Show total orders per customer.  
15. Show total sales per product.  
16. Show department-wise total salary.  
17. Show manager with number of employees.  
18. Show customers who bought Laptop.  
19. Show students enrolled in SQL.  
20. Show most popular course.  
21. Show top 3 customers by spending.  
22. Show product with highest sales.  
23. Show departments with no employees.  
24. Show customers with no orders.  
25. Show unsold products.  

---

## 🟠 ADVANCED (26–40)

26. Show students enrolled in more than 1 course.  
27. Show customers who placed more than 1 order.  
28. Show products sold more than 2 times.  
29. Show department with highest salary expense.  
30. Show course with highest enrollment.  
31. Show employee earning more than their manager.  
32. Show customers who bought multiple products.  
33. Show orders containing more than 1 product.  
34. Show most recent order per customer.  
35. Show first enrollment per student.  
36. Show highest spending customer.  
37. Show lowest selling product.  
38. Show average sales per product.  
39. Show total revenue per course.  
40. Show monthly sales report.  

---

## 🔴 HARD / INTERVIEW LEVEL (41–50)

41. Show students enrolled in ALL courses.  
42. Show customers who bought ALL products.  
43. Show product that every customer purchased.  
44. Show department where every employee earns > 50000.  
45. Show customers who never bought Laptop.  
46. Show students who enrolled after a specific date.  
47. Show manager whose team has highest salary.  
48. Show product contributing highest revenue.  
49. Show top course per student (latest enrollment).  
50. Show running total of customer spending.  
