# 🧠 SQL Practice Questions (DDL + DML + SELECT)

---

## 🟢 DDL – Data Definition Language (1–10)

1. Show all databases.
2. Create a database called `company_db`.
3. Use the `company_db` database.
4. Show all tables in the database.
5. Create a table `employees` with columns:
   (emp_id, name, dept, salary, city, joining_date).
6. Describe the structure of the employees table.
7. Add a new column `email` to the employees table.
8. Modify the salary column to BIGINT.
9. Rename the column `name` to `emp_name`.
10. Drop the column `email` from the table.

---

## 🟡 DML – Data Manipulation Language (11–20)

11. Insert a single record into the employees table.
12. Insert multiple records into the employees table.
13. Update the salary of an employee whose emp_id = 101.
14. Increase salary by 10% for all employees in the IT department.
15. Change city to 'Mumbai' where emp_id = 102.
16. Delete a record where emp_id = 103.
17. Delete employees whose salary is less than 25000.
18. Remove all records from the table without deleting the table.
19. Restore deleted data using ROLLBACK.
20. Make changes permanent using COMMIT.

---

# 🧠 SQL Practice Questions

---

## 🟡 EASY LEVEL (16–25)

16. Show employees whose salary is between 30000 and 60000.  
17. Show employees whose city is NULL.  
18. Show employees whose name starts with 'A'.  
19. Show employees ordered by salary (high → low).  
20. Count total number of employees.  
21. Show maximum salary.  
22. Show minimum salary.  
23. Show average salary.  
24. Show total salary paid to all employees.  
25. Show total number of employees in each department.  

---

## 🟠 MEDIUM LEVEL (26–40)

26. Show department-wise total salary.  
27. Show department-wise average salary.  
28. Show departments having more than 3 employees.  
29. Show departments where average salary > 60000.  
30. Show highest salary in each department.  
31. Show lowest salary in each department.  
32. Show city-wise employee count.  
33. Show cities having more than 2 employees.  
34. Show employees earning more than average salary.  
35. Show employees earning less than average salary.  
36. Show the second highest salary.  
37. Show employee(s) who earn the highest salary.  
38. Show top 3 highest-paid employees.  
39. Show employees who joined after 2022.  
40. Show year-wise employee count.  

---

## 🔴 HARD LEVEL (41–55)

41. Show the third highest salary.  
42. Show top 3 highest distinct salaries.  
43. Show employees who earn more than their department average.  
44. Show department having the highest total salary.  
45. Show department having the highest average salary.  
46. Show employees who earn the second highest salary.  
47. Show duplicate employee names.  
48. Show employees having the same salary.  
49. Show difference between highest and lowest salary.  
50. Show departments where minimum salary > 30000.  
51. Show departments where no employee earns less than 30000.  
52. Show city with highest number of employees.  
53. Show department-wise employee count in descending order.  
54. Show departments contributing more than 50% of total salary.  
55. Show employees whose salary is greater than the overall average but less than the department maximum.  

----
# 🎯 SQL Theory Interview Questions (Based on Completed Topics)

## 🟢 DDL – Data Definition Language

1. What is DDL?
2. Name all DDL commands.
3. What is the purpose of the CREATE command?
4. What is the difference between CREATE and ALTER?
5. What does the DROP command do?
6. What is the difference between DROP and TRUNCATE?
7. Can we rollback a DROP command?
8. What does the RENAME command do?
9. What is the use of the DESC (DESCRIBE) command?
10. How is TRUNCATE different from DELETE?

---

## 🟡 DML – Data Manipulation Language

11. What is DML?
12. Name all DML commands.
13. What is the purpose of the INSERT command?
14. What is the difference between INSERT and UPDATE?
15. What does the DELETE command do?
16. What is the difference between DELETE and TRUNCATE?
17. Can we rollback a DELETE command?
18. What is COMMIT?
19. What is ROLLBACK?
20. What is the use of the WHERE clause in DML?

---

## 🔵 SELECT STATEMENT

21. What is the SELECT statement?
22. What is the correct order of execution of a SELECT query?
23. What is the use of DISTINCT?
24. What is the difference between * and column names in SELECT?
25. What is column aliasing?
26. What is the use of ORDER BY?
27. What is the default sorting order in ORDER BY?
28. Can we sort by multiple columns?
29. What is the use of LIMIT / TOP?
30. What is the difference between WHERE and ORDER BY?

---

## 🟣 FILTERING (WHERE CLAUSE)

31. What is the WHERE clause?
32. What is the difference between WHERE and HAVING?
33. What are comparison operators?
34. What is the BETWEEN operator?
35. What is the IN operator?
36. What is the LIKE operator?
37. What is the difference between % and _ in LIKE?
38. How do you check for NULL values?
39. Why can’t we use = NULL?
40. What is the NOT operator?

---

## 🟠 AGGREGATE FUNCTIONS

41. What are aggregate functions?
42. Name commonly used aggregate functions.
43. What is the difference between COUNT(*) and COUNT(column)?
44. Does COUNT() include NULL values?
45. What does the SUM() function do?
46. What does the AVG() function do?
47. What is the difference between MAX() and MIN()?
48. Can we use aggregate functions without GROUP BY?
49. What is the use of aggregate functions in real-world scenarios?
50. Can aggregate functions be used in the WHERE clause?

---

## 🔴 GROUP BY & HAVING

51. What is GROUP BY?
52. Why do we use GROUP BY?
53. What is the difference between GROUP BY and DISTINCT?
54. What is the HAVING clause?
55. Why is HAVING used instead of WHERE with aggregate functions?
56. What is the difference between WHERE and HAVING?
57. Can we use ORDER BY with GROUP BY?
58. What happens if we select a column that is not in GROUP BY?
59. Can GROUP BY be used without aggregate functions?
60. What is the logical execution order of GROUP BY and HAVING?

--------
# 🎯 SQL Interview Questions (Based on Your Completed Topics)

## 🟢 BASIC LEVEL

1. What is DDL?
2. Name all DDL commands.
3. Difference between CREATE and ALTER.
4. Difference between DROP and TRUNCATE.
5. What is DML?
6. Difference between DELETE and TRUNCATE.
7. What is SELECT used for?
8. What is the default order of ORDER BY?
9. Difference between WHERE and HAVING.
10. What is the use of DISTINCT?

---

## 🟡 EASY QUERY-BASED QUESTIONS

11. Write a query to display all records from a table.
12. Write a query to display specific columns.
13. Write a query to find unique department names.
14. Write a query to filter employees with salary greater than 50000.
15. Write a query to display employees whose city is NULL.
16. Write a query to sort employees by salary in descending order.
17. Write a query to count total number of employees.
18. Write a query to find maximum salary.
19. Write a query to find minimum salary.
20. Write a query to find average salary.

---

## 🟠 MEDIUM LEVEL

21. Write a query to find total salary of all employees.
22. Write a query to count number of employees in each department.
23. Write a query to find department-wise average salary.
24. Write a query to display departments having more than 3 employees.
25. Write a query to display departments where average salary > 60000.
26. Write a query to find highest salary in each department.
27. Write a query to find lowest salary in each department.
28. Write a query to display city-wise employee count.
29. Write a query to display employees earning more than average salary.
30. Write a query to display employees earning less than average salary.

---

## 🔴 HARD LEVEL

31. Write a query to find the second highest salary.
32. Write a query to find the third highest salary.
33. Write a query to display employee(s) who earn the highest salary.
34. Write a query to display top 3 highest salaries.
35. Write a query to display department having the highest total salary.
36. Write a query to display department having the highest average salary.
37. Write a query to display duplicate employee names.
38. Write a query to display employees having the same salary.
39. Write a query to display departments where minimum salary > 30000.
40. Write a query to display city having the highest number of employees.

---

## 🧠 SCENARIO-BASED (FRESHER INTERVIEW FAVORITES)

41. How do you delete all records from a table but keep the structure?
42. How do you remove duplicate rows using SELECT?
43. How do you find the total number of rows in a table?
44. How do you fetch the first 5 highest-paid employees?
45. How do you find employees whose salary is between a given range?
46. How do you find employees who joined after a specific date?
47. How do you find department-wise total salary and sort it?
48. How do you display only those departments where total salary is greater than 2 lakh?
49. How do you find the difference between highest and lowest salary?
50. How do you count how many employees belong to each city?

------ 


