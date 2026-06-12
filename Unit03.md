
# DBS101 – Unit 3: Introduction to SQL

# 1. What is SQL?

SQL stands for **Structured Query Language**.

It is the standard language used to communicate with relational databases.

SQL allows users to:
- Create databases and tables
- Insert data
- Retrieve data
- Update existing data
- Delete data
- Control access permissions

Examples of databases that use SQL:
- MySQL
- PostgreSQL
- Oracle Database
- Microsoft SQL Server
- SQLite

---

# 2. Why is SQL Important?

SQL is important because:

- It is the standard language for relational databases.
- Easy to learn and use.
- Can handle large amounts of data efficiently.
- Used in almost every modern application.
- Helps retrieve information quickly.

Real-life examples:
- Banking systems
- University databases
- Hospital management systems
- E-commerce websites

---

# 3. Categories of SQL Commands

## DDL – Data Definition Language

Used to define and modify database structure.

Commands:
- CREATE
- ALTER
- DROP
- TRUNCATE

Example:

CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT
);

---

## DML – Data Manipulation Language

Used to modify data inside tables.

Commands:
- INSERT
- UPDATE
- DELETE

Example:

INSERT INTO Student
VALUES (1,'John',20);

---

## DQL – Data Query Language

Used to retrieve data.

Command:
- SELECT

Example:

SELECT * FROM Student;

---

## DCL – Data Control Language

Used to manage permissions.

Commands:
- GRANT
- REVOKE

Example:

GRANT SELECT ON Student TO User1;

---

# 4. SQL Data Definition (DDL)

DDL commands define the structure of database objects.

## CREATE TABLE

Used to create a new table.

Example:

CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT
);

Explanation:
- StudentID → Unique identifier
- Name → Stores names
- Age → Stores age values

---

## ALTER TABLE

Used to modify an existing table.

### Add Column

ALTER TABLE Student
ADD Email VARCHAR(100);

Result:
A new Email column is added.

---

### Modify Column

ALTER TABLE Student
ALTER COLUMN Name VARCHAR(100);

Used to change column properties.

---

## DROP TABLE

Deletes a table permanently.

DROP TABLE Student;

Warning:
All data inside the table is removed.

---

# 5. SQL Constraints

Constraints enforce rules on data.

## PRIMARY KEY

Uniquely identifies each row.

Example:

StudentID INT PRIMARY KEY

Characteristics:
- Unique
- Cannot be NULL

---

## FOREIGN KEY

Creates relationships between tables.

Example:

CREATE TABLE Enrollment (
    StudentID INT,
    FOREIGN KEY(StudentID)
    REFERENCES Student(StudentID)
);

Purpose:
Maintains referential integrity.

---

## NOT NULL

Ensures a column always contains a value.

Example:

Name VARCHAR(50) NOT NULL

---

## UNIQUE

Prevents duplicate values.

Example:

Email VARCHAR(100) UNIQUE

---

# 6. SQL Data Manipulation (DML)

## INSERT

Adds records to a table.

Example:

INSERT INTO Student
VALUES (1,'John',20);

Output:

| StudentID | Name | Age |
|-----------|------|-----|
| 1 | John | 20 |

---

## UPDATE

Modifies existing records.

Example:

UPDATE Student
SET Age = 21
WHERE StudentID = 1;

Result:
John's age becomes 21.

---

## DELETE

Removes records.

Example:

DELETE FROM Student
WHERE StudentID = 1;

Only matching rows are deleted.

---

# 7. SQL SELECT Statement

SELECT retrieves data from tables.

## Retrieve All Columns

SELECT * FROM Student;

Meaning:
Return every column and every row.

---

## Retrieve Specific Columns

SELECT Name, Age
FROM Student;

Output contains only Name and Age.

---

# 8. WHERE Clause

Filters records based on conditions.

Example:

SELECT *
FROM Student
WHERE Age > 20;

Only students older than 20 are displayed.

---

# 9. Comparison Operators

| Operator | Meaning |
|-----------|----------|
| = | Equal |
| <> | Not Equal |
| > | Greater Than |
| < | Less Than |
| >= | Greater Than or Equal |
| <= | Less Than or Equal |

Example:

SELECT *
FROM Student
WHERE Age >= 18;

---

# 10. Logical Operators

Used to combine conditions.

## AND

SELECT *
FROM Student
WHERE Age > 18 AND Age < 25;

Both conditions must be true.

---

## OR

SELECT *
FROM Student
WHERE Age = 18 OR Age = 20;

At least one condition must be true.

---

## NOT

SELECT *
FROM Student
WHERE NOT Age = 20;

Returns students whose age is not 20.

---

# 11. ORDER BY Clause

Sorts query results.

## Ascending Order

SELECT *
FROM Student
ORDER BY Age ASC;

Smallest age first.

---

## Descending Order

SELECT *
FROM Student
ORDER BY Age DESC;

Largest age first.

---

# 12. SQL Set Operations

Set operations combine results from multiple SELECT statements.

Requirements:
- Same number of columns
- Compatible data types

---

## UNION

Combines results and removes duplicates.

SELECT Name FROM Student
UNION
SELECT Name FROM Teacher;

Result:
Duplicate names appear only once.

---

## UNION ALL

Combines results but keeps duplicates.

SELECT Name FROM Student
UNION ALL
SELECT Name FROM Teacher;

Duplicates remain.

---

## INTERSECT

Returns common rows.

SELECT Name FROM Student
INTERSECT
SELECT Name FROM Alumni;

Only names appearing in both tables are shown.

---

## EXCEPT

Returns rows in first query but not second.

SELECT Name FROM Student
EXCEPT
SELECT Name FROM Alumni;

Shows students who are not alumni.

---

# 13. Advantages of SQL

- Easy to learn
- Industry standard
- Powerful querying capabilities
- Supports large databases
- Ensures data integrity
- Works across different DBMS platforms

---



