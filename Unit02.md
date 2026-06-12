# DBS101 – Unit 2: Database Design 

# 1. Introduction to Database Design

Database Design is the process of creating a database structure that stores data efficiently while maintaining:

- Data Integrity
- Data Consistency
- Minimal Redundancy
- Good Performance

### Main Goal
Create a database schema that supports applications and queries efficiently.

---

# 2. Database Design Process

The design process is usually divided into four stages.

## Stage 1: Requirements Collection and Analysis

This stage focuses on understanding what data the organization needs.

### Activities
- Identify user requirements
- Understand business rules
- Determine relationships among data
- Consult stakeholders

### Example
University Database:

Need information about:
- Students
- Courses
- Instructors
- Enrollments

### Output
A clear list of requirements.

---

## Stage 2: Conceptual Database Design

This stage creates a high-level model of the database.

### Characteristics
- Independent of DBMS
- Represents real-world objects
- Focuses on entities, attributes, and relationships

### Tool Used
Entity Relationship (ER) Model

### Output
ER Diagram

---

## Stage 3: Logical Database Design

Converts the ER model into relational tables.

### Activities
- Define tables
- Define attributes
- Assign primary keys
- Create foreign keys
- Apply normalization

### Example

Student(StudentID, Name, Major)

Course(CourseID, CourseName)

Enrollment(StudentID, CourseID)

---

## Stage 4: Physical Database Design

Determines how the database will be stored physically.

### Includes
- Storage structures
- Indexes
- Access paths
- Performance optimization

### Goal
Fast retrieval and efficient storage.

---

# 3. Relational Modeling

The Relational Model organizes data into tables.

A table is called a Relation.

---

## Relation

A relation is a table containing rows and columns.

Example:

| StudentID | Name | Major |
|------------|---------|-------|
| 101 | Sonam | IT |
| 102 | Karma | CS |

---

## Tuple

A tuple is a row in a table.

Example:

(101, Sonam, IT)

---

## Attribute

An attribute is a column in a table.

Examples:
- StudentID
- Name
- Major

---

## Domain

A domain is the set of allowed values for an attribute.

Example:

Age Domain = 0 to 120

Only values within this range are accepted.

---

# 4. Properties of Relations

Every relation must satisfy these rules:

### 1. Order of Rows Does Not Matter

Rows can appear in any order.

### 2. Each Row Must Be Unique

Duplicate records are not allowed.

### 3. Atomic Values

Each cell contains only one value.

Correct:
Phone = 17123456

Incorrect:
Phone = 17123456, 17234567

### 4. Every Attribute Has a Domain

Each column must have a valid range of values.

---

# 5. Entity-Relationship (ER) Model

The ER Model is used during conceptual database design.

It represents real-world data using:

- Entities
- Attributes
- Relationships

---

# 6. Entity

An Entity is a real-world object about which data is stored.

Examples:
- Student
- Course
- Instructor
- Department

Example:

Student:
- StudentID
- Name
- Age

---

# 7. Entity Set

An Entity Set is a collection of similar entities.

Example:

All students in a university form the Student Entity Set.

---

# 8. Attributes

Attributes describe properties of an entity.

Example:

Student Entity:

- StudentID
- Name
- Address
- Age

---

# 9. Types of Attributes

## A. Simple Attribute

Cannot be divided further.

Examples:
- Age
- Gender
- Salary

---

## B. Composite Attribute

Can be broken into smaller components.

Example:

Address
- Street
- City
- Country

Name
- First Name
- Middle Name
- Last Name

---

## C. Multivalued Attribute

Can have multiple values.

Example:

Phone Numbers

Student:
Phone = {17123456, 17234567}

---

## D. Derived Attribute

Obtained from another attribute.

Example:

DateOfBirth → Age

Age is calculated from DateOfBirth.

---

# 10. Relationships

Relationships describe associations between entities.

Example:

Student ENROLLS IN Course

Student -------- Enrolls -------- Course

---

# 11. Mapping Cardinalities

Cardinality specifies how many entities participate in a relationship.

---

## One-to-One (1:1)

One entity relates to exactly one other entity.

Example:

Person ↔ Passport

One person has one passport.

---

## One-to-Many (1:N)

One entity relates to many entities.

Example:

Department → Employees

One department can have many employees.

---

## Many-to-One (N:1)

Many entities relate to one entity.

Example:

Students → Department

Many students belong to one department.

---

## Many-to-Many (M:N)

Many entities relate to many entities.

Example:

Students ↔ Courses

A student can take many courses.
A course can have many students.

---

# 12. Keys in Relational Databases

Keys uniquely identify records.

---

## Primary Key

A Primary Key uniquely identifies each row.

Characteristics:
- Unique
- Cannot be NULL
- Minimal

Example:

| StudentID | Name |
|------------|------|
| 101 | Sonam |

Primary Key = StudentID

---

## Candidate Key

Any attribute that can uniquely identify a record.

Example:

Student:
- StudentID
- Email

Both may uniquely identify students.

---

## Composite Key

A key made from multiple attributes.

Example:

Enrollment Table
(StudentID, CourseID)
Together they uniquely identify enrollment records.

---

# 13. Redundancy

Redundancy means storing the same data multiple times.

Example:
Student department name stored repeatedly for every record.

---

## Problems Caused by Redundancy

### Data Inconsistency

Different copies may contain different values.

### Update Anomaly

Need to update data in many places.

### Storage Waste

Repeated information consumes extra storage.

---

# 14. Importance of Removing Redundancy

Benefits:

- Better consistency
- Easier maintenance
- Less storage usage
- Improved database quality

Normalization is commonly used to remove redundancy.

---

# 15. ER Diagram Symbols 

Rectangle = Entity
Oval = Attribute
Double Oval = Multivalued Attribute
Dashed Oval = Derived Attribute
Diamond = Relationship
Underline Attribute = Primary Key
Line = Connection

---