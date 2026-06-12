# DBS101 - UNIT 6: INDEXING AND QUERY PROCESSING

## Introduction

Databases may contain thousands or millions of records. Searching through every record each time would be very slow. To solve this problem, databases use **Indexing** and **Query Processing** techniques.

* **Indexing** helps find data quickly.
* **Query Processing** helps execute SQL queries efficiently.

---

# 6.1 Basic Concepts of Indexing

## What is Indexing?

Indexing is a technique used to speed up data retrieval in a database.

An index stores:

* Search Key
* Pointer to actual data record

Instead of searching every row, the database first checks the index and directly finds the required record.

---

## Why is Indexing Needed?

### 1. Faster Searching

Data can be located quickly.

### 2. Reduced Disk Access

Less reading from storage devices.

### 3. Better Query Performance

SELECT queries execute faster.

---

## Example

Table: Student

| ID | Name  | Age |
| -- | ----- | --- |
| 1  | Sonam | 20  |
| 2  | Karma | 21  |
| 3  | Pema  | 22  |

Query:

```sql
SELECT * FROM Student
WHERE Name='Sonam';
```

### Without Index

Database checks every row.

### With Index

Database directly finds:

```text
Sonam → Row 1
```

Result:

* Faster execution
* Less disk access

---

## Key Idea

Index stores:

```text
Search Key + Pointer
```

Example:

```text
Sonam → Record Address
Karma → Record Address
Pema → Record Address
```

---

# 6.2 Indexing Structures

Different structures are used to organize indexes.

---

## 1. Single-Level Index

A simple index containing:

```text
Key → Record Pointer
```

Example:

```text
10 → Block1
20 → Block2
30 → Block3
```

### Advantages

* Simple
* Easy to implement

### Disadvantages

* Not efficient for large databases

---

## 2. Multi-Level Index

An index built on another index.

Structure:

```text
Top Index
    ↓
Lower Index
    ↓
Data Blocks
```

### Benefit

Reduces search space dramatically.

Instead of searching thousands of entries, the database searches only a few levels.

---

# 3. Tree-Based Indexing

Most modern databases use tree structures.

Examples:

* B-Tree
* B+ Tree

---

# B-Tree

B-Tree is a balanced tree used for indexing.

Characteristics:

* Self-balancing
* Sorted nodes
* Can have more than two children
* Height automatically adjusts

---

## Properties of B-Tree

### All Leaf Nodes at Same Level

Every search takes approximately the same time.

### No Empty Subtrees

Tree remains balanced.

### Small Height

Search operations remain fast.

---

## Time Complexity

Search:

```text
O(log n)
```

Very efficient compared to linear search:

```text
O(n)
```

---

# B+ Tree (Most Important)

B+ Tree is an improved version of B-Tree.

Most DBMS systems use B+ Trees.

Examples:

* MySQL
* Oracle
* PostgreSQL

---

## Structure of B+ Tree

### Internal Nodes

Store only keys.

```text
[20 | 40 | 60]
```

Used for navigation.

---

### Leaf Nodes

Store:

* Keys
* Data pointers

Example:

```text
20 → Record
25 → Record
30 → Record
```

---

## Important Features

### All Leaves are at Same Level

Balanced tree.

### Leaf Nodes are Linked

Supports sequential access.

### Faster Range Queries

Example:

```sql
SELECT * FROM Student
WHERE Age BETWEEN 20 AND 30;
```

---

## Advantages of B+ Tree

### Fast Search

```text
O(log n)
```

### Efficient Disk Access

Fewer disk reads.

### Supports Range Queries

Excellent for database applications.

### Balanced Structure

Consistent performance.

---

# B-Tree vs B+ Tree

| Feature                | B-Tree         | B+ Tree        |
| ---------------------- | -------------- | -------------- |
| Data in Internal Nodes | Yes            | No             |
| Data in Leaf Nodes     | Yes            | Yes            |
| Range Queries          | Less Efficient | Very Efficient |
| Used in Modern DBMS    | Rarely         | Commonly       |

---

# 6.3 Ordered and Unordered Indices

---

# Ordered Index

Records are stored in sorted order.

Example:

```text
10 → A
20 → B
30 → C
```

---

## Advantages

### Fast Searching

Binary-like searching possible.

### Efficient Range Queries

Example:

```sql
Age BETWEEN 20 AND 25
```

---

## Disadvantages

### Slower Insertions

New records must be inserted in order.

---

# Unordered Index (Heap File)

Records stored randomly.

Example:

```text
30 → C
10 → A
20 → B
```

---

## Advantages

### Fast Insertions

Simply place record anywhere.

---

## Disadvantages

### Slow Searches

May require scanning entire file.

---

# Comparison

| Feature       | Ordered   | Unordered |
| ------------- | --------- | --------- |
| Search Speed  | Fast      | Slow      |
| Insert Speed  | Slow      | Fast      |
| Range Queries | Efficient | Poor      |

---

# 6.4 Indexing of Temporal and Spatial Data

---

# Temporal Data Indexing

Temporal Data = Data involving time.

Examples:

* Salary history
* Patient records
* Attendance records

---

## Example

```text
2024 → Salary Data
2025 → Salary Data
2026 → Salary Data
```

---

## Used For

### Historical Analysis

Example:

"What was the salary in 2024?"

### Time-Based Queries

Example:

"Show attendance records for March."

---

# Spatial Data Indexing

Spatial Data represents location information.

Examples:

* Maps
* GPS
* Navigation systems
* Geographic Information Systems (GIS)

---

## Specialized Structures

### R-Tree

Stores geometric objects efficiently.

### Quad-Tree

Divides regions into smaller regions.

---

## Example

```text
+-----+-----+
| A1  | A2  |
+-----+-----+
| A3  | A4  |
+-----+-----+
```

Each region indexed separately.

---

## Key Difference

Temporal Indexing:

```text
Time-Based Access
```

Spatial Indexing:

```text
Location-Based Access
```

---

# 6.5 Indexing for Search

---

## How Index Improves Search

Query:

```sql
SELECT * FROM Student
WHERE Age > 20;
```

### Without Index

* Scan entire table
* Read every record

Complexity:

```text
O(n)
```

---

### With Index

* Locate relevant records directly

Complexity:

```text
O(log n)
```

---

# Types of Searches Supported

## 1. Exact Match Search

Example:

```sql
Name='Sonam'
```

---

## 2. Range Search

Example:

```sql
Age > 20
```

---

## 3. Pattern Matching

Example:

```sql
Name LIKE 'S%'
```

Finds:

```text
Sonam
Sangay
Sita
```

---

## Important Note

Too many indexes can cause problems:

* Slower INSERT
* Slower UPDATE
* Slower DELETE

Reason:

Every index must also be updated.

---

# 6.6 Query Processing and Optimization

---

## What is Query Processing?

The process of converting an SQL query into an execution plan and producing results.

---

# Steps of Query Processing

```text
SQL Query
    ↓
Parsing
    ↓
Translation
(Relational Algebra)
    ↓
Optimization
    ↓
Execution
```

---

# Step 1: SQL Query

User writes:

```sql
SELECT name, age
FROM Student
WHERE age > 20;
```

---

# Step 2: Parsing

DBMS checks:

### Syntax

Is SQL written correctly?

### Tables

Does Student table exist?

### Columns

Do age and name exist?

---

Example Error:

```sql
SELECT name age
FROM Student;
```

Missing comma.

Parser reports error.

---

# Step 3: Translation

SQL converted into Relational Algebra.

Example:

```text
PROJECT(name, age)
        ↓
SELECT(age > 20)
        ↓
Student
```

Meaning:

1. Read Student table
2. Select students older than 20
3. Display name and age

---

# Step 4: Optimization

Optimizer chooses the best execution strategy.

Example:

### Plan A

Scan entire table.

### Plan B

Use Age index.

If table is large:

Plan B is usually faster.

---

## Optimization Goals

Reduce:

* Disk I/O
* CPU Usage
* Memory Usage
* Execution Time

---

# Step 5: Execution

DBMS runs the selected plan.

Example Output:

| Name  | Age |
| ----- | --- |
| Karma | 21  |
| Pema  | 22  |

---

# Simple Flow Summary

```text
Write Query
      ↓
Check Query
      ↓
Convert Query
      ↓
Optimize Query
      ↓
Execute Query
      ↓
Return Results
```

---

# 6.6.1 Measures of Query Cost

## What is Query Cost?

Amount of resources required to execute a query.

---

## Major Cost Factors

### Disk I/O (Most Important)

Reading data from disk is expensive.

### CPU Time

Processing operations.

### Memory Usage

Temporary storage required.

---

## Key Principle

```text
Less Disk Access = Faster Query
```

---

# 6.6.2 Evaluation of Expressions

How queries are executed internally.

---

## Example

```sql
SELECT *
FROM Student
WHERE Age > 20;
```

Execution:

```text
Read Table
      ↓
Apply Condition
      ↓
Produce Result
```

---

# Join Example

```sql
SELECT *
FROM A
JOIN B
ON A.id = B.id;
```

Execution:

1. Read A
2. Read B
3. Match IDs
4. Produce result

---

# 6.6.3 Choice of Evaluation Plans

Different methods can execute the same query.

---

# What is a Query Plan?

A strategy chosen by DBMS to execute a query.

---

## Join Strategies

### 1. Nested Loop Join

For every row in A:

Compare with every row in B.

```text
A1 → B1 B2 B3
A2 → B1 B2 B3
```

Simple but slower.

---

### 2. Hash Join

Create hash table.

```text
Hash(A)
    ↓
Match B
```

Usually much faster.

---

### 3. Sort-Merge Join

Sort both tables.

```text
Sort A
Sort B
    ↓
Merge
```

Efficient for large sorted data.

---

# Query Optimizer

Automatically selects:

* Lowest cost plan
* Fastest execution method
* Most efficient strategy

---

# Final Exam Summary

## Indexing

* Speeds up data retrieval.
* Stores key + pointer.
* Reduces disk access.

## B-Tree

* Balanced tree.
* Supports efficient searching.

## B+ Tree

* Most important indexing structure.
* Used by MySQL, Oracle, PostgreSQL.
* Internal nodes store keys only.
* Leaf nodes store data pointers.

## Ordered Index

* Fast search.
* Good for range queries.

## Unordered Index

* Fast insertion.
* Slow searching.

## Query Processing Steps

1. Parsing
2. Translation
3. Optimization
4. Execution

## Query Cost

Depends on:

* Disk I/O
* CPU Time
* Memory Usage

## Join Methods

1. Nested Loop Join
2. Hash Join
3. Sort-Merge Join

---

