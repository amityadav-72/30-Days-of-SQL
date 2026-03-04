# SQL Subquery Practice Questions (IN, ANY, ALL)


## SQL Subquery Practice Database

```
CREATE DATABASE subquery_practice;
USE subquery_practice;
```

##  DEPARTMENTS TABLE
```
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50),
    location VARCHAR(50)
);

INSERT INTO departments VALUES
(10,'HR','Mumbai'),
(20,'IT','Delhi'),
(30,'Sales','Pune'),
(40,'Finance','Mumbai'),
(50,'Marketing','Delhi');
```


 ##  EMPLOYEES TABLE

```
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    salary INT,
    department_id INT,
    manager_id INT,
    hire_date DATE
);

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


  ##  STUDENTS TABLE

```
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    class VARCHAR(10),
    section VARCHAR(5),
    marks INT
);

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

 ##   COURSES TABLE

```
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50),
    department_id INT
);

INSERT INTO courses VALUES
(101,'SQL Basics',20),
(102,'Python Programming',20),
(103,'Data Science',20),
(104,'Marketing Strategy',50),
(105,'Finance Management',40),
(106,'HR Analytics',10);
```


  ##   ENROLLMENTS TABLE

```
CREATE TABLE enrollments (
    enrollment_id INT PRIMARY KEY,
    student_id INT,
    course_id INT
);

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


   ##  CATEGORIES TABLE
```

CREATE TABLE categories (
    category_id INT PRIMARY KEY,
    category_name VARCHAR(50)
);

INSERT INTO categories VALUES
(1,'Electronics'),
(2,'Stationery'),
(3,'Clothing'),
(4,'Furniture');
```


  ##   PRODUCTS TABLE

```
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(50),
    price INT,
    category_id INT
);

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

 ## CUSTOMERS TABLE
```
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(50),
    city VARCHAR(50)
);

INSERT INTO customers VALUES
(1,'Raj','Delhi'),
(2,'Anita','Mumbai'),
(3,'Suresh','Pune'),
(4,'Megha','Delhi'),
(5,'Ravi','Nagpur');
```

 ##    ORDERS TABLE
```
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    product_id INT,
    amount INT,
    order_date DATE
);

INSERT INTO orders VALUES
(1,1,1,70000,'2024-01-10'),
(2,2,3,200,'2024-02-05'),
(3,3,5,3000,'2024-03-15'),
(4,1,8,2500,'2024-04-20'),
(5,4,2,500,'2024-01-25'),
(6,5,6,8000,'2024-02-11'),
(7,2,7,1200,'2024-03-30'),
(8,3,4,50,'2024-04-05');
```

## 🟢 BASIC LEVEL (1–15)

These focus mainly on **IN operator with subqueries**.

1. Find employees whose department is HR or IT using a subquery.  
2. Find students enrolled in courses that exist in the courses table.  
3. Find employees working in departments located in Mumbai.  
4. Find products whose category exists in the categories table.  
5. Find students enrolled in SQL or Python courses using subquery.  
6. Find customers who placed orders.  
7. Find employees working in departments with more than 5 employees.  
8. Find products that were ordered by customers.  
9. Find students who enrolled in any available course.  
10. Find employees whose department id appears in the departments table.  
11. Find orders placed by customers from Delhi.  
12. Find students who took courses offered by department 101.  
13. Find employees whose manager_id exists in the employees table.  
14. Find customers who bought products priced above 5000.  
15. Find students enrolled in courses that start with ‘Data’.

---

## 🟡 INTERMEDIATE LEVEL (16–30)

These start using **ANY** and **ALL operators**.

16. Find employees whose salary is greater than ANY salary in the HR department.  
17. Find employees whose salary is greater than ALL salaries in the Sales department.  
18. Find products whose price is greater than ANY price in electronics category.  
19. Find employees whose salary is lower than ALL managers’ salaries.  
20. Find students whose marks are greater than ANY student in class A.  
21. Find products more expensive than ANY product in category ‘Stationery’.  
22. Find employees earning more than ALL employees in department 10.  
23. Find orders with amount greater than ANY order in January.  
24. Find customers who spent more than ALL customers in a specific city.  
25. Find employees whose salary equals ANY salary in department 20.  
26. Find students whose marks are higher than ALL students in section B.  
27. Find products priced lower than ALL premium products.  
28. Find employees earning more than ANY employee hired before 2020.  
29. Find customers whose purchase amount exceeds ALL purchases by customer 101.  
30. Find employees whose salary matches ANY salary of employees in department 30.

---

## 🟠 ADVANCED LEVEL (31–40)

These combine **joins + multi-row subqueries**.

31. Find employees whose department appears in a department list where average salary > 60000.  
32. Find students enrolled in courses that have more than 3 students.  
33. Find customers who bought products belonging to multiple categories.  
34. Find employees working in departments where max salary exceeds 70000.  
35. Find products ordered by customers from multiple cities.  
36. Find students who enrolled in courses with highest enrollment count.  
37. Find customers who purchased products that appear in top-selling products list.  
38. Find employees whose salary is greater than ANY average department salary.  
39. Find products that were purchased by customers who placed more than 2 orders.  
40. Find students whose marks are higher than ANY class topper from other sections.

---

## 🔴 HARD / INTERVIEW LEVEL (41–50)

These simulate **real interview scenarios**.

41. Find employees earning more than all employees in their own department except themselves.  
42. Find products whose price is greater than all products in the same category.  
43. Find customers who bought all products in a specific category.  
44. Find employees whose salary is higher than any manager’s salary.  
45. Find departments whose average salary is greater than any other department.  
46. Find students who scored higher than all students in another class.  
47. Find products whose sales are higher than all products sold last month.  
48. Find employees whose salary is greater than any employee hired in 2022.  
49. Find customers who placed orders greater than all orders of customer 105.  
50. Find courses whose enrollment count is greater than any other course in the same department.


## SQL Subquery Theory Interview Questions

### Basic Level

1. What is a **subquery in SQL**?
2. What are the **different types of subqueries**?
3. What is the difference between a **subquery and a join**?
4. Where can subqueries be used in an SQL statement?
5. What is a **single-row subquery**?
6. What is a **multi-row subquery**?
7. What is a **correlated subquery**?
8. What is the difference between **IN and EXISTS** in subqueries?
9. Can a subquery return multiple columns?
10. What happens if a subquery returns **more than one value when a single value is expected**?

---

### Intermediate Level

11. What is the difference between **ANY and ALL operators** in subqueries?
12. How does the **IN operator work with subqueries**?
13. What is the difference between **EXISTS and NOT EXISTS**?
14. When should you use a **correlated subquery instead of a normal subquery**?
15. What are **nested subqueries**?
16. Can subqueries be used in the **SELECT clause**?
17. Can subqueries be used in the **FROM clause**?
18. What is a **derived table** in SQL?
19. What are the **performance implications of using subqueries**?
20. How can subqueries affect query optimization?

---

### Advanced / Interview Level

21. What is the difference between **correlated and non-correlated subqueries**?
22. Why are **joins often faster than subqueries**?
23. What is a **scalar subquery**?
24. How does SQL execute a **correlated subquery internally**?
25. What are the limitations of subqueries?
26. Can subqueries be used in **UPDATE or DELETE statements**?
27. What is the difference between **subquery vs CTE (Common Table Expression)**?
28. What is the difference between **subquery vs window functions**?
29. How can you improve the **performance of subqueries**?
30. What are common **mistakes developers make while using subqueries**?
