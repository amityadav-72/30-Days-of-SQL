# 📘 DAY 4 — ADVANCED FILTERING

## 🎯 YOU WILL MASTER

- LIKE
- Wildcards (`%`, `_`)
- IN
- BETWEEN
- IS NULL / IS NOT NULL

These are **very frequently used in real projects + interviews**.

---

# 1️⃣ LIKE OPERATOR

## ✅ Purpose
Used for **pattern matching (searching text)**.

## ✅ Syntax
```sql
SELECT column_name
FROM table_name
WHERE column_name LIKE pattern;
```

## ✅ Wildcards

| Wildcard | Meaning |
|---|---|
| % | Any number of characters |
| _ | Exactly one character |

## ✅ Examples

### Starts with 'A'
```sql
SELECT * FROM employees
WHERE name LIKE 'A%';
```

### Ends with 'a'
```sql
SELECT * FROM employees
WHERE name LIKE '%a';
```

### Contains 'it'
```sql
SELECT * FROM employees
WHERE department LIKE '%it%';
```

### Second letter is 'a'
```sql
SELECT * FROM employees
WHERE name LIKE '_a%';
```

## 🧠 Interview Notes

- LIKE is **case-insensitive in MySQL**
- Used in **search features**

---

# 2️⃣ IN OPERATOR

## ✅ Purpose
Used to match **multiple values**.

## ✅ Syntax
```sql
SELECT column_name
FROM table_name
WHERE column_name IN (value1, value2, value3);
```

## ✅ Example
```sql
SELECT * FROM employees
WHERE city IN ('Mumbai', 'Delhi');
```

## 🧠 Why IN is better than OR

Instead of:

```sql
city = 'Mumbai' OR city = 'Delhi'
```

Use:

```sql
city IN ('Mumbai', 'Delhi')
```
_Use `IN` when comparing the same column with multiple values because it is more readable, maintainable, and works efficiently with subqueries._
- Cleaner & faster.

---

# 3️⃣ BETWEEN OPERATOR

## ✅ Purpose
Used for **range filtering (numbers, dates)**.

## ✅ Syntax
```sql
SELECT column_name
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

## ✅ Example
```sql
SELECT * FROM employees
WHERE salary BETWEEN 40000 AND 60000;
```

## 🧠 Important
BETWEEN is **inclusive**  
👉 Includes both values.

---

# 4️⃣ IS NULL

## ❌ Wrong
```sql
WHERE city = NULL
```

## ✅ Correct
```sql
SELECT * FROM employees
WHERE city IS NULL;
```

---

# 5️⃣ IS NOT NULL

```sql
SELECT * FROM employees
WHERE city IS NOT NULL;
```

## 🧠 NULL CONCEPT

NULL means:

- Not empty
- Not zero
- Not blank
- **Unknown value**

---

# 🔥 COMBINED REAL QUERY

```sql
SELECT name, salary
FROM employees
WHERE city IN ('Mumbai', 'Delhi')
AND salary BETWEEN 40000 AND 70000
AND name LIKE 'A%';
```

---

# 🧠 QUICK MEMORY BOX

```
LIKE      → pattern search
%         → any characters
_         → single character
IN        → multiple values
BETWEEN   → range (inclusive)
IS NULL   → missing values
```

---

# 🧪 DAY 4 PRACTICE QUESTIONS

## 🟢 LEVEL 1 — LIKE

1. Names starting with 'A'  
2. Names ending with 'a'  
3. Names containing 'r'  
4. Department starting with 'F'  
5. Names where second letter is 'a'  

---

## 🟢 LEVEL 2 — IN

6. Employees from Mumbai or Pune  
7. Employees from HR or IT  
8. Employees with salary in (40000, 50000, 60000)  
9. Employees whose emp_id in (1,3,5)  
10. Cities in Delhi and Mumbai  

---

## 🟢 LEVEL 3 — BETWEEN

11. Salary between 40000 and 60000  
12. Salary between 45000 and 70000  
13. emp_id between 2 and 4  
14. Salary NOT between 40000 and 60000  
15. Employees between id 1 and 3 from IT  

---

## 🟢 LEVEL 4 — NULL

16. Employees where city is NULL  
17. Employees where city is NOT NULL  
18. Employees where salary is NULL  
19. Employees where department is NOT NULL  
20. Count employees where city is NULL  

---

## 🟢 LEVEL 5 — MIXED

21. Employees from Mumbai & salary between 40000–70000  
22. Names starting with 'S' and city Delhi  
23. HR employees with salary > 40000  
24. Employees from Mumbai or salary > 60000  
25. Names containing 'a' and salary < 60000  

---

## 🟢 LEVEL 6 — REAL THINKING

26. Names not starting with 'A'  
27. Salary not between 40000 and 60000  
28. Cities except Mumbai & Delhi  
29. Employees whose name length is 5  
30. Employees whose name starts and ends with vowel  

---

# 🎯 INTERVIEW QUESTIONS

1. Difference between IN and BETWEEN  
2. Difference between LIKE and =  
3. Why NULL cannot be compared using =  
4. Which wildcard is faster % or _  
5. Is BETWEEN inclusive?

---
Q 20 
```
SELECT  COUNT(*) AS count
FROM employees
WHERE city is NULL;
```

Q 29 
```
SELECT *
FROM employees
WHERE LENGTH(name) = 5;
```

Q 30 
```
SELECT *
FROM employees
WHERE name REGEXP '^[AEIOUaeiou].*[AEIOUaeiou]$';

```
