# Unit 5: Relational Database Design 

## Introduction

Relational Database Design focuses on organizing data efficiently to:

* Reduce redundancy (duplicate data)
* Avoid anomalies (update, insertion, deletion problems)
* Improve consistency
* Make databases easier to maintain

---

# 5.1 Features of Good Relational Designs

A good database design should have:

## 1. Minimal Redundancy

* Avoid storing the same information multiple times.
* Saves storage space.
* Reduces inconsistency.

### Example

Instead of storing department office details for every student, store them once in a separate department table.

---

## 2. No Data Anomalies

### Update Anomaly

Same information appears in many rows and must be updated everywhere.

**Example:**
If CSE office changes from Block A to Block C, every student record must be updated.

### Insertion Anomaly

Cannot insert a fact without another unrelated fact.

**Example:**
Cannot add a new department until a student joins it.

### Deletion Anomaly

Deleting one record removes useful information.

**Example:**
Deleting the last ECE student removes ECE department information.

---

## 3. Lossless Join Decomposition

After splitting a table into smaller tables, we should be able to reconstruct the original table perfectly using JOIN operations.

---

## 4. Dependency Preservation

Functional dependencies should remain enforceable after decomposition without requiring expensive joins.

---

# 5.2 Decomposition Using Functional Dependencies

## What is Decomposition?

Decomposition means breaking a large relation into smaller relations.

### Why Decompose?

* Remove redundancy
* Eliminate anomalies
* Achieve higher normal forms

---

## Properties of Good Decomposition

### Lossless Join

When decomposed tables are joined:

Original Relation = Joined Relation

No extra tuples should appear.

### Dependency Preservation

All original functional dependencies should still be enforceable.

---

### Example

Relation:

R(A, B, C)

Functional Dependency:

A → B

Decompose into:

R1(A, B)

R2(A, C)

Result:

* Lossless Join ✓
* Dependency Preserved ✓

---

# 5.3 Normal Forms

## What is Normalization?

Normalization is the process of organizing data to reduce redundancy and avoid anomalies.

Normalization mainly uses:

* Keys
* Functional Dependencies (FD)
* Multivalued Dependencies (MVD)
* Join Dependencies

---

# First Normal Form (1NF)

## Definition

A relation is in 1NF if:

* Every cell contains a single value.
* No repeating groups.
* No multivalued attributes.

---

### Not in 1NF

| StudentID | Name  | PhoneNumbers       |
| --------- | ----- | ------------------ |
| S1        | Sonam | 17111111, 17222222 |

PhoneNumbers contains multiple values.

---

### Convert to 1NF

| StudentID | Name  | PhoneNumber |
| --------- | ----- | ----------- |
| S1        | Sonam | 17111111    |
| S1        | Sonam | 17222222    |

Now each cell contains only one value.

---

## Key Point

1NF = Atomic Values

---

# Second Normal Form (2NF)

## Definition

A relation is in 2NF if:

1. It is already in 1NF.
2. Every non-prime attribute depends on the whole candidate key.

---

## Important Terms

### Prime Attribute

Part of a candidate key.

### Non-Prime Attribute

Not part of any candidate key.

### Partial Dependency

When an attribute depends on only part of a composite key.

---

### Example

ENROLLMENT(
StudentID,
CourseID,
StudentName,
CourseName,
Grade
)

Composite Key:

(StudentID, CourseID)

FDs:

StudentID → StudentName

CourseID → CourseName

(StudentID, CourseID) → Grade

Problem:

* StudentName depends only on StudentID.
* CourseName depends only on CourseID.

Partial dependencies exist.

Therefore NOT in 2NF.

---

### Convert to 2NF

STUDENT(StudentID, StudentName)

COURSE(CourseID, CourseName)

ENROLLMENT(StudentID, CourseID, Grade)

Now all attributes depend on the full key.

---

## Key Point

2NF removes Partial Dependency.

---

# Third Normal Form (3NF)

## Definition

A relation is in 3NF if:

1. It is already in 2NF.
2. No transitive dependency exists.

---

## What is Transitive Dependency?

When:

Key → Non-key Attribute

and

Non-key Attribute → Another Non-key Attribute

Then indirect dependency exists.

---

### Example

EMPLOYEE(
EmpID,
EmpName,
DeptID,
DeptName
)

FDs:

EmpID → EmpName, DeptID

DeptID → DeptName

Thus:

EmpID → DeptName

This is a transitive dependency.

Not in 3NF.

---

### Convert to 3NF

EMPLOYEE(
EmpID,
EmpName,
DeptID
)

DEPARTMENT(
DeptID,
DeptName
)

Now transitive dependency is removed.

---

## Key Point

3NF removes Transitive Dependency.

---

# BCNF (Boyce-Codd Normal Form)

## Definition

A relation is in BCNF if:

Every determinant is a superkey.

---

### Simple Rule

For every FD:

X → Y

X must be a superkey.

---

## BCNF vs 3NF

| 3NF                           | BCNF                             |
| ----------------------------- | -------------------------------- |
| Less strict                   | More strict                      |
| May allow some redundancy     | Removes more redundancy          |
| Preserves dependencies better | May lose dependency preservation |

---

# 4NF (Fourth Normal Form)

## Purpose

Removes redundancy caused by Multivalued Dependencies (MVDs).

---

### Example

Student, Hobby, Language

Student can have:

* Multiple hobbies
* Multiple languages

Independent of each other.

MVDs:

Student ↠ Hobby

Student ↠ Language

This creates repeated combinations.

4NF solves this.

---

# 5NF (Fifth Normal Form)

Also called:

Project Join Normal Form (PJNF)

---

## Purpose

Removes redundancy caused by Join Dependencies.

Used only in advanced situations.

---

# Summary of Normal Forms

| Normal Form | Removes                          |
| ----------- | -------------------------------- |
| 1NF         | Repeating groups                 |
| 2NF         | Partial dependency               |
| 3NF         | Transitive dependency            |
| BCNF        | Determinants not being superkeys |
| 4NF         | Multivalued dependency           |
| 5NF         | Join dependency                  |

---

# 5.4 Functional Dependency Theory

## Functional Dependency (FD)

X → Y

Means:

If two tuples have the same X value,
they must have the same Y value.

X determines Y.

---

## Terminology

### Determinant

Left side of FD.

Example:

StudentID → Name

StudentID = Determinant

---

### Dependent

Right side of FD.

Name = Dependent

---

### Trivial FD

AB → A

Right side already belongs to left side.

---

### Non-Trivial FD

A → B

B is not part of A.

---

## Superkey

A set of attributes that uniquely identifies tuples.

---

## Candidate Key

A minimal superkey.

No attribute can be removed.

---

# Armstrong's Axioms

Used to infer new functional dependencies.

---

## 1. Reflexivity

If Y ⊆ X

Then

X → Y

---

## 2. Augmentation

If

X → Y

Then

XZ → YZ

---

## 3. Transitivity

If

X → Y

and

Y → Z

Then

X → Z

---

# Derived Rules

## Union

If:

X → Y

X → Z

Then:

X → YZ

---

## Decomposition

If:

X → YZ

Then:

X → Y

and

X → Z

---

## Pseudotransitivity

If:

X → Y

and

WY → Z

Then:

WX → Z

---

# Attribute Closure

Notation:

X⁺

Means:

All attributes functionally determined by X.

Used for:

* Finding candidate keys
* Testing superkeys
* Checking implied FDs

---

# Canonical Cover

A minimal equivalent set of functional dependencies.

Characteristics:

* No redundant FD
* No extra attributes
* Simpler representation

---

# 5.5 Decomposition Algorithms

## BCNF Decomposition

When FD:

X → Y

violates BCNF,

decompose into:

R1 = X ∪ Y

R2 = R − (Y − X)

Repeat until BCNF achieved.

---

### Advantage

Lossless Join Guaranteed.

### Disadvantage

May not preserve dependencies.

---

## 3NF Synthesis Algorithm

Steps:

1. Compute Canonical Cover
2. Create relation for each FD
3. Add candidate key relation if needed
4. Remove redundant relations

Guarantees:

* Lossless Join
* Dependency Preservation
* 3NF Relations

---

# 5.6 Multivalued Dependencies (MVD)

Notation:

X ↠ Y

Meaning:

One X can have multiple independent Y values.

---

### Example

Student ↠ Hobby

Student ↠ Language

Hobbies and languages are independent.

Storing them together creates redundancy.

4NF solves this issue.

---

# 5.7 Additional Normal Forms

## DKNF (Domain-Key Normal Form)

A relation is in DKNF if every constraint comes only from:

* Domain constraints
* Key constraints

Very ideal but rarely used.

---

# 5.8 Atomic Domains and 1NF

## Atomic Domain

Values are indivisible.

Examples:

Good:

* 17111111

Bad:

* 17111111, 17222222

---

### Why Atomic Values Matter

They make:

* Searching easier
* Joining easier
* Normalization easier

---

# 5.9 Database Design Process

## Step 1: Requirements Analysis

Identify:

* Users
* Data
* Reports
* Business rules

---

## Step 2: Conceptual Design

Create ER Diagram.

Includes:

* Entities
* Relationships
* Constraints

---

## Step 3: Logical Design

Convert ER model into relational schema.

Define:

* Tables
* Keys
* Constraints

---

## Step 4: Schema Refinement

Normalize relations.

Apply:

* FDs
* MVDs
* Normal Forms

---

## Step 5: Physical Design

Decide:

* Storage
* Indexes
* File organization

---

## Step 6: Security and Application Design

Implement:

* Access control
* Transactions
* Views
* Application logic

---

## Important Exam Point

Database Design is Iterative.

Designers often revisit previous stages and improve the schema.

---

# 5.10 Modelling Temporal Data

Temporal Data = Data associated with time.

---

## Valid Time

Time during which a fact is true in the real world.

Example:

Employee lives at an address from
2023–2026.

---

## Transaction Time

Time during which data exists in the database.

Useful for:

* Auditing
* Recovery

---

## Bitemporal Data

Stores:

* Valid Time
* Transaction Time

Together.

---

## Snapshot

Database state at a specific time.

---

## Example

EmployeeSalary(
EmployeeID,
Salary,
StartDate,
EndDate
)

Used to store salary history.

---

## Benefits of Temporal Data

* Track history
* Auditing
* Legal compliance
* Historical reporting

Example Question:

"What was the salary on 1 January 2025?"

instead of

"What is the salary now?"

---


