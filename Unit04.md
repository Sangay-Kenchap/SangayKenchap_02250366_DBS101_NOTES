# Unit IV: Intermediate and Advanced SQL

## Introduction

Structured Query Language (SQL) is the standard language used to communicate with relational databases. Advanced SQL features help manage complex data operations, improve performance, maintain data integrity, and support application development.

---

# 4.1 Join Expressions

## What is a Join?

A JOIN combines rows from two or more tables based on a related column.

### Example Tables

#### Student

| StudentID | Name |
|------------|------|
| 1 | John |
| 2 | Alice |

#### Enrollment

| StudentID | Course |
|------------|---------|
| 1 | DBMS |
| 2 | OS |

---

## Types of Joins

### 1. INNER JOIN

Returns matching records from both tables.

```sql
SELECT Student.Name, Enrollment.Course
FROM Student
INNER JOIN Enrollment
ON Student.StudentID = Enrollment.StudentID;
```

### 2. LEFT JOIN

Returns all records from the left table and matching records from the right table.

```sql
SELECT *
FROM Student
LEFT JOIN Enrollment
ON Student.StudentID = Enrollment.StudentID;
```

### 3. RIGHT JOIN

Returns all records from the right table and matching records from the left table.

```sql
SELECT *
FROM Student
RIGHT JOIN Enrollment
ON Student.StudentID = Enrollment.StudentID;
```

### 4. FULL OUTER JOIN

Returns all matching and non-matching records from both tables.

```sql
SELECT *
FROM Student
FULL OUTER JOIN Enrollment
ON Student.StudentID = Enrollment.StudentID;
```

### 5. SELF JOIN

A table joins with itself.

```sql
SELECT A.Name, B.Name
FROM Employee A, Employee B
WHERE A.ManagerID = B.EmployeeID;
```

---

# 4.2 Views

## What is a View?

A View is a virtual table created from a SQL query.

### Advantages

- Simplifies complex queries
- Enhances security
- Provides data abstraction

### Create View

```sql
CREATE VIEW StudentView AS
SELECT Name, Department
FROM Student;
```

### Use View

```sql
SELECT * FROM StudentView;
```

### Delete View

```sql
DROP VIEW StudentView;
```

---

# 4.3 Transactions

## What is a Transaction?

A transaction is a sequence of SQL operations performed as a single unit of work.

### ACID Properties

### A - Atomicity

Either all operations occur or none occur.

### C - Consistency

Database remains valid before and after transaction.

### I - Isolation

Transactions do not interfere with each other.

### D - Durability

Committed changes are permanent.

### Transaction Commands

#### Start Transaction

```sql
START TRANSACTION;
```

#### Commit

```sql
COMMIT;
```

#### Rollback

```sql
ROLLBACK;
```

### Example

```sql
START TRANSACTION;

UPDATE Account
SET Balance = Balance - 500
WHERE AccountID = 1;

UPDATE Account
SET Balance = Balance + 500
WHERE AccountID = 2;

COMMIT;
```

---

# 4.4 Integrity Constraints

## What are Integrity Constraints?

Rules that ensure accuracy and consistency of data.

---

## 1. NOT NULL

Column cannot contain NULL values.

```sql
Name VARCHAR(50) NOT NULL
```

---

## 2. UNIQUE

Prevents duplicate values.

```sql
Email VARCHAR(100) UNIQUE
```

---

## 3. PRIMARY KEY

Uniquely identifies each row.

```sql
StudentID INT PRIMARY KEY
```

---

## 4. FOREIGN KEY

Maintains relationship between tables.

```sql
FOREIGN KEY(StudentID)
REFERENCES Student(StudentID)
```

---

## 5. CHECK

Restricts values.

```sql
Age INT CHECK (Age >= 18)
```

---

## 6. DEFAULT

Assigns a default value.

```sql
Status VARCHAR(20) DEFAULT 'Active'
```

---

# 4.5 SQL Data Types and Schemas

## SQL Data Types

### Numeric Types

| Data Type | Description |
|------------|-------------|
| INT | Integer |
| SMALLINT | Small integer |
| DECIMAL | Fixed precision number |
| FLOAT | Floating point number |

### Character Types

| Data Type | Description |
|------------|-------------|
| CHAR(n) | Fixed-length string |
| VARCHAR(n) | Variable-length string |
| TEXT | Large text |

### Date and Time Types

| Data Type | Description |
|------------|-------------|
| DATE | Date only |
| TIME | Time only |
| DATETIME | Date and time |
| TIMESTAMP | Timestamp value |

---

## Schema

A schema is a logical container that organizes database objects.

### Create Schema

```sql
CREATE SCHEMA University;
```

### Create Table Inside Schema

```sql
CREATE TABLE University.Student
(
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50)
);
```

---

# 4.6 Index Definition in SQL

## What is an Index?

An index improves the speed of data retrieval operations.

### Advantages

- Faster searching
- Faster sorting
- Faster joins

### Create Index

```sql
CREATE INDEX idx_name
ON Student(Name);
```

### Unique Index

```sql
CREATE UNIQUE INDEX idx_email
ON Student(Email);
```

### Remove Index

```sql
DROP INDEX idx_name;
```

### Disadvantage

Indexes require additional storage and slow INSERT, UPDATE, DELETE operations.

---

# 4.7 Authorization

## What is Authorization?

Authorization controls access to database resources.

---

## Grant Privileges

```sql
GRANT SELECT, INSERT
ON Student
TO user1;
```

### Common Privileges

- SELECT
- INSERT
- UPDATE
- DELETE
- ALL PRIVILEGES

---

## Revoke Privileges

```sql
REVOKE INSERT
ON Student
FROM user1;
```

---

# 4.8 Accessing SQL from a Programming Language

Applications communicate with databases using database APIs.

---

## Example using Python

```python
import mysql.connector

conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="password",
    database="college"
)

cursor = conn.cursor()

cursor.execute("SELECT * FROM Student")

for row in cursor:
    print(row)

conn.close()
```

---

## Steps

1. Connect to database
2. Create cursor
3. Execute SQL query
4. Fetch results
5. Close connection

---

# 4.9 Functions and Stored Procedures

## Functions

A function returns a value.

### Example

```sql
CREATE FUNCTION Square(num INT)
RETURNS INT
BEGIN
    RETURN num * num;
END;
```

### Call Function

```sql
SELECT Square(5);
```

---

## Stored Procedures

A stored procedure is a precompiled collection of SQL statements.

### Create Procedure

```sql
CREATE PROCEDURE GetStudents()
BEGIN
    SELECT * FROM Student;
END;
```

### Execute Procedure

```sql
CALL GetStudents();
```

### Advantages

- Faster execution
- Reusable code
- Improved security

---

# 4.10 Triggers

## What is a Trigger?

A trigger automatically executes when a specified event occurs.

---

## Trigger Events

- INSERT
- UPDATE
- DELETE

---

## Example

```sql
CREATE TRIGGER StudentLog
AFTER INSERT
ON Student
FOR EACH ROW
INSERT INTO AuditLog
VALUES ('New student added');
```

### Benefits

- Automatic auditing
- Data validation
- Business rule enforcement

---

# 4.11 Recursive Queries

## What is a Recursive Query?

A query that refers to itself to solve hierarchical problems.

Examples:

- Employee hierarchy
- Organization chart
- Family tree

---

## Example using WITH RECURSIVE

```sql
WITH RECURSIVE EmployeeHierarchy AS
(
    SELECT EmployeeID,
           Name,
           ManagerID
    FROM Employee
    WHERE ManagerID IS NULL

    UNION ALL

    SELECT E.EmployeeID,
           E.Name,
           E.ManagerID
    FROM Employee E
    JOIN EmployeeHierarchy EH
    ON E.ManagerID = EH.EmployeeID
)
SELECT * FROM EmployeeHierarchy;
```

---

# 4.12 Advanced Aggregation Features

Aggregation performs calculations on groups of rows.

---

## Common Aggregate Functions

### COUNT()

```sql
SELECT COUNT(*) FROM Student;
```

### SUM()

```sql
SELECT SUM(Salary) FROM Employee;
```

### AVG()

```sql
SELECT AVG(Marks) FROM Student;
```

### MAX()

```sql
SELECT MAX(Salary) FROM Employee;
```

### MIN()

```sql
SELECT MIN(Marks) FROM Student;
```

---

## GROUP BY

Groups rows based on a column.

```sql
SELECT Department,
       COUNT(*)
FROM Employee
GROUP BY Department;
```

---

## HAVING

Filters grouped records.

```sql
SELECT Department,
       COUNT(*)
FROM Employee
GROUP BY Department
HAVING COUNT(*) > 5;
```

---

## ROLLUP

Generates subtotals and grand totals.

```sql
SELECT Department,
       SUM(Salary)
FROM Employee
GROUP BY ROLLUP(Department);
```

---

## CUBE

Generates all possible aggregations.

```sql
SELECT Department,
       JobTitle,
       SUM(Salary)
FROM Employee
GROUP BY CUBE(Department, JobTitle);
```

