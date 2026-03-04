# SQL Subquery Practice Questions

## Create Database

```sql
CREATE DATABASE subquery_practice;
USE subquery_practice;
```

---

# Departments Table

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50),
    location VARCHAR(50),
    created_at DATE
);
```

```sql
INSERT INTO departments VALUES
(10,'HR','Mumbai','2019-01-01'),
(20,'IT','Delhi','2021-03-15'),
(30,'Sales','Pune','2018-07-20'),
(40,'Finance','Mumbai','2022-02-10'),
(50,'Marketing','Delhi','2023-05-05');
```

---

# Employees Table

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    salary INT,
    department_id INT,
    manager_id INT,
    hire_date DATE
);
```

```sql
INSERT INTO employees VALUES
(1,'Amit',60000,20,NULL,'2021-05-10'),
(2,'Rahul',50000,10,1,'2022-01-15'),
(3,'Sneha',70000,20,1,'2020-07-12'),
(4,'Priya',45000,30,2,'2023-03-21'),
(5,'Vikas',80000,30,2,'2019-11-30'),
(6,'Anjali',55000,40,3,'2021-09-05'),
(7,'Karan',40000,50,3,'2022-06-18'),
(8,'Neha',65000,20,1,'2018-08-11'),
(9,'Rohit',72000,40,3,'2020-12-25'),
(10,'Meena',48000,10,1,'2024-01-10');
```

---

# Students Table

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    class VARCHAR(10),
    section VARCHAR(5),
    marks INT
);
```

```sql
INSERT INTO students VALUES
(1,'Arjun','A','A',85),
(2,'Pooja','A','B',72),
(3,'Riya','B','A',91),
(4,'Kabir','B','B',67),
(5,'Sahil','A','A',88),
(6,'Neel','C','A',76),
(7,'Simran','C','B',83),
(8,'Aditya','B','A',79);
```

---

# Courses Table

```sql
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50),
    department_id INT,
    credits INT,
    professor VARCHAR(50)
);
```

```sql
INSERT INTO courses VALUES
(101,'SQL Basics',20,4,'John'),
(102,'Python Programming',20,5,'David'),
(103,'Data Science',20,5,'John'),
(104,'Marketing Strategy',50,3,'Emma'),
(105,'Finance Management',40,4,'Robert'),
(106,'HR Analytics',10,3,'Sophia');
```

---

# Enrollments Table

```sql
CREATE TABLE enrollments (
    enrollment_id INT PRIMARY KEY,
    student_id INT,
    course_id INT
);
```

```sql
INSERT INTO enrollments VALUES
(1,1,101),
(2,1,102),
(3,2,101),
(4,3,103),
(5,4,102),
(6,5,103),
(7,6,105),
(8,7,104),
(9,8,101);
```

---

# Categories Table

```sql
CREATE TABLE categories (
    category_id INT PRIMARY KEY,
    category_name VARCHAR(50)
);
```

```sql
INSERT INTO categories VALUES
(1,'Electronics'),
(2,'Stationery'),
(3,'Clothing'),
(4,'Furniture');
```

---

# Products Table

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(50),
    price INT,
    category_id INT
);
```

```sql
INSERT INTO products VALUES
(1,'Laptop',70000,1),
(2,'Mouse',500,1),
(3,'Notebook',200,2),
(4,'Pen',50,2),
(5,'Chair',3000,4),
(6,'Table',8000,4),
(7,'T-Shirt',1200,3),
(8,'Headphones',2500,1);
```

---

# Customers Table

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(50),
    city VARCHAR(50)
);
```

```sql
INSERT INTO customers VALUES
(1,'Raj','Delhi'),
(2,'Anita','Mumbai'),
(3,'Suresh','Pune'),
(4,'Megha','Delhi'),
(5,'Ravi','Nagpur');
```

---

# Orders Table

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    product_id INT,
    amount INT,
    quantity INT,
    order_date DATE
);
```

```sql
INSERT INTO orders VALUES
(1,1,1,70000,1,'2024-01-10'),
(2,2,3,200,5,'2024-02-05'),
(3,3,5,3000,1,'2024-03-15'),
(4,1,8,2500,2,'2024-04-20'),
(5,4,2,500,3,'2024-01-25'),
(6,5,6,8000,1,'2024-02-11'),
(7,2,7,1200,2,'2024-03-30'),
(8,3,4,50,10,'2024-04-05');
```

---

# Sales Table

```sql
CREATE TABLE sales (
    sale_id INT PRIMARY KEY,
    product_id INT,
    sale_date DATE
);
```

```sql
INSERT INTO sales VALUES
(1,1,'2024-01-10'),
(2,2,'2024-02-05'),
(3,5,'2024-03-15'),
(4,8,'2024-04-20');
```

---

# Premium Products Table

```sql
CREATE TABLE premium_products (
    product_id INT,
    price INT
);
```

```sql
INSERT INTO premium_products VALUES
(1,70000),
(6,8000);
```

---

# Luxury Products Table

```sql
CREATE TABLE luxury_products (
    product_id INT,
    price INT
);
```

```sql
INSERT INTO luxury_products VALUES
(1,70000),
(6,8000);
```

---

# Competitor Products Table

```sql
CREATE TABLE competitor_products (
    product_id INT,
    price INT
);
```

```sql
INSERT INTO competitor_products VALUES
(101,60000),
(102,9000);
```

---

## 🟢 BASIC LEVEL (1–15)

**Focus: `IN` operator**

1. Find employees who work in departments located in Mumbai.
2. Find students enrolled in courses offered by department 101.
3. Find customers who placed orders in 2024.
4. Find products belonging to categories Electronics or Furniture using a subquery.
5. Find employees whose department name is IT or HR.
6. Find students enrolled in courses whose credits > 3.
7. Find customers who purchased products costing more than 5000.
8. Find employees who work in departments with more than 10 employees.
9. Find products that appear in the sales table.
10. Find orders placed by customers from Delhi.
11. Find employees whose `manager_id` appears in the employees table.
12. Find students who enrolled in courses available in the course table.
13. Find products belonging to categories that have more than 5 products.
14. Find employees working in departments that were created after 2020.
15. Find students who enrolled in any course taught by professor **John**.

---

## 🟡 INTERMEDIATE LEVEL (16–30)

**Focus: `ANY` operator**

16. Find employees whose salary is greater than **ANY salary in department 10**.
17. Find products priced higher than **ANY product in category 'Stationery'**.
18. Find students whose marks are higher than **ANY student in class A**.
19. Find employees whose salary is lower than **ANY manager salary**.
20. Find orders with amount greater than **ANY order placed in January**.
21. Find customers who spent more than **ANY customer from Mumbai**.
22. Find products whose price is greater than **ANY product sold last month**.
23. Find employees earning more than **ANY employee hired before 2022**.
24. Find students who scored higher than **ANY student in another section**.
25. Find customers whose order amount exceeds **ANY order of customer 101**.
26. Find employees whose salary equals **ANY salary in department 20**.
27. Find products cheaper than **ANY premium product**.
28. Find students whose marks exceed **ANY student who failed**.
29. Find employees whose salary is greater than **ANY average department salary**.
30. Find orders with quantity greater than **ANY order from last week**.

---

## 🟠 ADVANCED LEVEL (31–40)

**Focus: `ALL` operator**

31. Find employees whose salary is greater than **ALL salaries in department 20**.
32. Find products priced higher than **ALL products in category 'Furniture'**.
33. Find students whose marks exceed **ALL students in section B**.
34. Find customers whose purchase amount is greater than **ALL purchases made last week**.
35. Find employees whose salary is lower than **ALL managers' salaries**.
36. Find products cheaper than **ALL luxury products**.
37. Find orders whose amount is greater than **ALL orders placed yesterday**.
38. Find students who scored higher than **ALL students in class A**.
39. Find employees whose salary is greater than **ALL employees hired in 2023**.
40. Find products whose price is lower than **ALL competitor products**.

---

## 🔴 HARD / INTERVIEW LEVEL (41–50)

**Focus: Complex logic using multi-row subqueries**

41. Find employees earning more than all employees in their own department except themselves.
42. Find customers who bought **all products in a category**.
43. Find products whose price is greater than **all products in the same category**.
44. Find departments whose **average salary is greater than any other department**.
45. Find students who scored higher than **all students in another class**.
46. Find products whose **sales are greater than all products sold last month**.
47. Find customers who spent **more than all customers in the same city**.
48. Find employees whose salary is **greater than all managers in the company**.
49. Find courses whose **enrollment count is greater than any other course in the department**.
50. Find products purchased by **every customer**.
