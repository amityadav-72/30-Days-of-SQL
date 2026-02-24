# 📘 DML COMMANDS (Data Manipulation Language)

## 1️⃣ What is DML?

**Definition:**  
DML (Data Manipulation Language) commands are used to:
- Insert data into tables  
- Modify existing data  
- Delete data  
- Retrieve data  

👉 **DML works on DATA, not structure.**

### Key Characteristics of DML
- Works on table data  
- Can be rolled back (in most cases)  
- Does NOT change table structure  
- Uses transactions  

### DML Commands List

| Command | Purpose |
|-------|--------|
| INSERT | Add new records |
| UPDATE | Modify existing records |
| DELETE | Remove records |
| SELECT | Retrieve records |

👉 **SELECT is part of DML (very important interview question)**

---

## 2️⃣ INSERT COMMAND

### Purpose
Used to add new rows (records) into a table.

### INSERT Syntax (All Columns)
```sql
INSERT INTO table_name
VALUES (value1, value2, value3);
```

### Example
```sql
INSERT INTO employees
VALUES (6, 'Rahul', 'IT', 55000, 'Pune');
```

⚠️ Order of values must match table structure.

### INSERT with Column Names (Best Practice)
```sql
INSERT INTO employees (emp_id, name, department, salary, city)
VALUES (7, 'Neha', 'HR', 48000, 'Mumbai');
```

### INSERT Multiple Rows
```sql
INSERT INTO employees VALUES
(8, 'Arjun', 'Finance', 65000, 'Delhi'),
(9, 'Meena', 'IT', 72000, 'Mumbai');
```

### Important INSERT Notes
- Text → 'single quotes'
- Numbers → no quotes
- Column order matters
- One INSERT = one transaction

---

## 3️⃣ UPDATE COMMAND

### Purpose
Used to modify existing data.

### UPDATE Syntax
```sql
UPDATE table_name
SET column = value
WHERE condition;
```

⚠️ WHERE is VERY IMPORTANT  
Without WHERE → all rows get updated ❌

### Examples
```sql
UPDATE employees SET salary = 60000 WHERE emp_id = 2;
UPDATE employees SET salary = 70000, city = 'Delhi' WHERE emp_id = 3;
UPDATE employees SET salary = salary + 5000 WHERE department = 'HR';
```

❌ Common Mistake
```sql
UPDATE employees SET salary = 50000;
```

---

## 4️⃣ DELETE COMMAND

### DELETE Syntax
```sql
DELETE FROM table_name WHERE condition;
```

### Examples
```sql
DELETE FROM employees WHERE emp_id = 5;
DELETE FROM employees WHERE department = 'Finance';
```

### DELETE vs TRUNCATE

| DELETE | TRUNCATE |
|------|---------|
| DML | DDL |
| WHERE allowed | WHERE not allowed |
| Slower | Faster |
| Can rollback | Cannot rollback |
| Deletes selected rows | Deletes all rows |

---

## 5️⃣ SELECT COMMAND

### Basic Syntax
```sql
SELECT column_name FROM table_name;
```

### Examples
```sql
SELECT * FROM employees;
SELECT name, salary FROM employees;
SELECT * FROM employees WHERE department = 'IT';
```

### SELECT Execution Order (Interview Gold)
**FROM → WHERE → SELECT**

---

## 6️⃣ DML SUMMARY

- INSERT → adds data  
- UPDATE → modifies data  
- DELETE → removes data  
- SELECT → retrieves data  

---

# 📘 DML PRACTICE QUESTIONS (50)

# 📘 DML PRACTICE QUESTIONS (50)

---

## 🛠️ Instruction to Create `employees` Table

Before practicing DML commands, create an `employees` table with the following columns:

- **emp_id** – Employee ID  
- **name** – Employee Name  
- **department** – Department Name  
- **salary** – Employee Salary  
- **city** – City of Work  

The table should store employee details such as ID, name, department, salary, and city.

---

## 🟢 INSERT QUESTIONS (1–12)
```
1. Add one employee with values: **1, Amit, IT, 60000, Mumbai**.
2. Add one employee with values: **2, Ravi, HR, 40000, Pune**.
3. Add one employee with values: **3, Sneha, IT, 70000, Delhi**.

4. Add two employees together with values:  
   - **4, Priya, Finance, 50000, Mumbai**  
   - **5, Karan, HR, 45000, Delhi**

5. Add three employees in one operation with values:  
   - **6, Rahul, IT, 55000, Pune**  
   - **7, Neha, HR, 48000, Mumbai**  
   - **8, Arjun, Finance, 65000, Delhi**

6. Add an employee whose salary is greater than 70000:  
   **9, Meena, IT, 72000, Mumbai**.

7. Add an employee whose salary is less than 40000:  
   **10, Suresh, HR, 38000, Pune**.

8. Add an employee working in Delhi:  
   **11, Pooja, IT, 61000, Delhi**.

9. Add an employee working in Finance department:  
   **12, Ramesh, Finance, 54000, Mumbai**.

10. Add an employee whose name starts with ‘A’:  
    **13, Ankit, HR, 42000, Pune**.

11. Add an employee with the highest salary so far:  
    **14, Kavita, IT, 75000, Delhi**.

12. Add an employee with duplicate city but different department:  
    **15, Mohit, Finance, 58000, Mumbai**.
```
---

## 🟡 UPDATE QUESTIONS (13–28)
```
13. Update the salary to **65000** for the employee where emp_id is **1**.  
14. Update the city to **Mumbai** for the employee where emp_id is **2**.  
15. Update the department to **Finance** for the employee where emp_id is **3**.  
16. Update both salary and city for the employee where emp_id is **4**.  
17. Increase the salary by **5000** for all employees working in **HR** department.  
18. Increase the salary by **10%** for all employees working in **IT** department.  
19. Update the city to **Delhi** for all employees currently working in **Pune**.  
20. Update the department to **IT** for employees whose salary is greater than **70000**.  
21. Update salary to **50000** for employees whose salary is less than **40000**.  
22. Update the city to **Mumbai** for employees working in **Finance** department.  
23. Update the department to **HR** for employees working in **Delhi**.  
24. Update salary to **60000** for employees named **Ravi**.  
25. Update salary for employees whose emp_id is **11 or 12**.  
26. Update city and department for employee where emp_id is **13**.  
27. Increase salary for all employees **except those in Finance department**.  
28. Update department for employees whose salary is **between 45000 and 55000**.
```
---

## 🔴 DELETE QUESTIONS (29–38)
```
29. Delete the employee where emp_id is **15**.  
30. Delete employees working in **HR** department.  
31. Delete employees whose salary is less than **40000**.  
32. Delete employees working in **Pune** city.  
33. Delete employees from **Finance department working in Delhi**.  
34. Delete employees whose salary is greater than **75000**.  
35. Delete employees named **Suresh**.  
36. Delete employees whose emp_id is **10 or 11**.  
37. Delete all employees **except those working in IT department**.  
38. Delete all records from the employees table.
```
---

## 🔵 SELECT QUESTIONS (39–50)
```
39. Retrieve all employee records.  
40. Retrieve only employee **names and salaries**.  
41. Retrieve employees working in **IT department**.  
42. Retrieve employees working in **Mumbai**.  
43. Retrieve employees whose salary is greater than **60000**.  
44. Retrieve employees whose salary is **between 45000 and 65000**.  
45. Retrieve employees working in **HR department and Delhi city**.  
46. Retrieve employees working in **IT or Finance department**.  
47. Retrieve employees **not working in HR department**.  
48. Retrieve employees whose salary is the **highest among all employees**.  
49. Retrieve employees whose city is **Mumbai and salary is greater than 50000**.  
50. Retrieve employees sorted by **salary in descending order**.
```
