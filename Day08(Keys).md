# 📘 DAY 8 --- KEYS & CONSTRAINTS (THEORY BLOCK 1)

------------------------------------------------------------------------

# 🧠 1. SUPER KEY

## ✅ CONCEPT

A super key is any column or combination of columns that uniquely
identifies a row in a table.

It may contain extra attributes that are not required for uniqueness.

So:

-   All candidate keys are super keys
-   But not all super keys are candidate keys

## ❗ SQL IMPLEMENTATION

There is no direct SQL syntax for a super key because it exists at the
logical level.


## ✅ EXAMPLE TABLE --- students

| roll_no | email        | phone      | name |
|--------:|-------------|------------|------|
| 1       | a@gmail.com | 9991110000 | Amit |
| 2       | b@gmail.com | 8882220000 | Neha |

------------------------------------------------------------------------

## ✅ POSSIBLE SUPER KEYS
```
-   roll_no
-   email
-   phone
-   roll_no + name
-   email + name
-   roll_no + email + phone
```
All uniquely identify rows → all are super keys.


## ✅ EXPLANATION

- Even if extra columns are added, uniqueness is maintained.

- But database design prefers minimal keys → Candidate Key.

------------------------------------------------------------------------

# 🧠 2. CANDIDATE KEY

## ✅ CONCEPT

A candidate key is a minimal super key.

Minimal means: If any column is removed → uniqueness is lost.



## ✅ FROM PREVIOUS EXAMPLE

Candidate keys:
```
-   roll_no
-   email
-   phone
```
Not a candidate key:

-   roll_no + name ❌



## ❗ SQL IMPLEMENTATION

Candidate keys are implemented using:

-   PRIMARY KEY
-   UNIQUE



## ✅ EXPLANATION

A table can have:

-   Multiple candidate keys
-   Only one primary key

------------------------------------------------------------------------

# 🧠 3. PRIMARY KEY

## ✅ CONCEPT

The candidate key chosen to uniquely identify each row.



## ✅ PROPERTIES

-   Unique
-   Not NULL
-   Only one per table
-   Automatically indexed
-   Should not change frequently



## ✅ SYNTAX --- INLINE
```
CREATE TABLE students (
    roll_no INT PRIMARY KEY,
    name VARCHAR(50)
);
```

## ✅ SYNTAX --- TABLE LEVEL
```
CREATE TABLE students (
    roll_no INT,
    name VARCHAR(50),
    PRIMARY KEY (roll_no)
);
```


## ✅ SYNTAX --- NAMED

```
CREATE TABLE students (
roll_no INT,
name VARCHAR(50),
CONSTRAINT
pk_students PRIMARY KEY (roll_no)
);
```


## ❌ DUPLICATE TEST

```
INSERT INTO students VALUES (1,'Amit');
INSERT INTO students VALUES (1,'Neha');
```
Error → duplicate primary key



## ❌ NULL TEST
```
INSERT INTO students VALUES (NULL,'Amit');
```
Not allowed.



## ✅ WHY PRIMARY KEY?

-   Unique identity
-   No duplicates
-   Fast searching (index)

------------------------------------------------------------------------

# 🧠 4. AUTO_INCREMENT

## ✅ CONCEPT

Automatically generates the next numeric value.

Used when user should not manually enter ID.



## ✅ SYNTAX
```
CREATE TABLE students (
id INT AUTO_INCREMENT PRIMARY KEY,
name
VARCHAR(50)
);
```
## ✅ INSERT
```
INSERT INTO students (name) VALUES ('Amit');
INSERT INTO students (name) VALUES ('Neha');
```


## ✅ RESULT

 | id | name |
|---:|------|
| 1  | Amit |
| 2  | Neha |



## ✅ SET START VALUE
```
ALTER TABLE students AUTO_INCREMENT = 100;
```


## ✅ EXPLANATION

Database automatically maintains:

-   Uniqueness
-   Sequence

------------------------------------------------------------------------

# 🧠 5. UNIQUE KEY

## ✅ CONCEPT

Ensures all values in a column are unique.



## 🔥 PRIMARY KEY vs UNIQUE KEY

 | PRIMARY KEY        | UNIQUE KEY              |
|--------------------|--------------------------|
| Only one allowed   | Multiple allowed         |
| Cannot be NULL     | One NULL allowed         |
| Main identifier    | Alternate unique column  |



## ✅ SYNTAX
```
CREATE TABLE users ( id INT PRIMARY KEY, email VARCHAR(100) UNIQUE );
```


## ❌ DUPLICATE TEST
```
INSERT INTO users VALUES (1,'a@gmail.com');
INSERT INTO users VALUES (2,'a@gmail.com');
```
Not allowed.



## ✅ NULL CASE
```
INSERT INTO users VALUES (3,NULL);
```
Allowed.


## ✅ USAGE

Used for:

-   Email
-   Phone
-   Username

------------------------------------------------------------------------

# 🧠 6. NOT NULL

## ✅ CONCEPT

Ensures column cannot store NULL.



## ✅ SYNTAX
```
CREATE TABLE students (
 id INT PRIMARY KEY,
name VARCHAR(50)
NOT NULL
);
```


## ❌ TEST
```
INSERT INTO students (id) VALUES (1);
```
Error → name required.

------------------------------------------------------------------------

# 🧠 7. DEFAULT

## ✅ CONCEPT

Provides automatic value if user does not insert any value.


## ✅ SYNTAX
```
CREATE TABLE users (
id INT PRIMARY KEY,
status VARCHAR(20) DEFAULT 'active'
);
```

## ✅ RESULT

status → active

------------------------------------------------------------------------

# 🧠 8. FOREIGN KEY

## ✅ CONCEPT

A foreign key is a column that references the primary key of another
table.



## ✅ PARENT TABLE
```
CREATE TABLE departments (
dept_id INT PRIMARY KEY,
 dept_name VARCHAR(50)
);
```

## ✅ CHILD TABLE
```
CREATE TABLE employees (
emp_id INT PRIMARY KEY,
emp_name VARCHAR(50),
dept_id INT,
FOREIGN KEY (dept_id)
REFERENCES departments(dept_id)
 );
```


## ✅ VALID INSERT
```
INSERT INTO departments VALUES (1,'HR');
INSERT INTO employees VALUES (101,'Amit',1);
```


## ❌ INVALID INSERT
```
INSERT INTO employees VALUES (102,'Neha',5);
```
Dept 5 does not exist.



# 🔐 REFERENTIAL INTEGRITY

Foreign key ensures:

-   No invalid reference
-   Relationship safety
-   Consistent database

------------------------------------------------------------------------

# 🎯 INTERVIEW QUICK REVISION

-   Super Key → Unique (can have extra columns)
-   Candidate Key → Minimal super key
-   Primary Key → Selected candidate key
-   Unique Key → Alternate unique column
-   Foreign Key → Creates relationship
-   Not Null → Mandatory field
-   Default → Automatic value
-   Auto Increment → Automatic numeric sequence

------------------------------------------------------------------------

