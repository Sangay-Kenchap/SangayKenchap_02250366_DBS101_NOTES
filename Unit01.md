# DBS101 – Unit 1: Introduction to Database Systems 

# 1. What is Data?
Data refers to raw facts, figures, observations, or values that have not yet been processed.

Examples:
- Student Name: Sangay
- Age: 20
- Marks: 85

Data by itself may not be meaningful.

Information = Processed and organized data that is useful for decision-making.

Example:
"The average mark of DBS101 students is 78%"

---

# 2. What is a Database?

A Database is a structured collection of related data stored electronically and organized so that it can be easily accessed, managed, and updated.

Example:
A university database may store:
- Student details
- Course information
- Grades
- Attendance records

Benefits:
- Easy storage
- Fast retrieval
- Better organization
- Improved security

---

# 3. What is a DBMS (Database Management System)?

A DBMS is software that allows users to create, manage, and interact with databases.

Examples:
- MySQL
- PostgreSQL
- Oracle Database
- Microsoft SQL Server
- SQLite

Functions of DBMS:
- Store data
- Retrieve data
- Update data
- Delete data
- Control access
- Backup and recovery

---

# 4. View of Data (Levels of Data Abstraction)

Database systems hide complex storage details from users through abstraction.

## A. Physical Level (Lowest Level)

Describes how data is physically stored.

Includes:
- Files
- Storage blocks
- Indexes
- Hard drives and SSDs

Example:
How student records are saved on disk.

Users usually do not interact with this level.

---

## B. Logical Level

Describes:
- What data is stored
- Relationships between data

Example:

Student
(Student_ID, Name, Department)

Course
(Course_ID, Course_Name)

Enrollment
(Student_ID, Course_ID)

Database designers and administrators mainly work here.

---

## C. View Level (Highest Level)

Shows only the information needed by a specific user.

Examples:
- Lecturer sees grades
- Student sees own results
- Accountant sees fee records

Advantages:
- Better security
- Simpler interface
- Hides unnecessary details

---

# 5. Purpose of Database Systems

Database systems were developed to solve problems found in traditional file systems.

## A. Reduce Data Redundancy

Data redundancy means duplicate copies of data.

Problem:
Student information stored in many files.

Solution:
Store data once in a centralized database.

Benefits:
- Saves storage space
- Easier maintenance

---

## B. Improve Data Consistency

Consistency means data remains accurate everywhere.

Example:
Student phone number updated once and reflected throughout the system.

---

## C. Data Sharing

Many users can access the same database simultaneously.

Example:
- Students register courses
- Lecturers upload marks
- Admin staff manage records

All use the same database.

---

## D. Data Integrity

Integrity ensures data remains correct and valid.

Examples:
- Student ID must be unique.
- Age cannot be negative.

---

## E. Data Security

Protects sensitive information.

Methods:
- User accounts
- Passwords
- Access permissions

---

## F. Backup and Recovery

Protects data from:
- System failures
- Hardware damage
- Human mistakes

Allows restoration of lost data.

---

# 6. History of Database Systems

## 1. Early File Systems (1950s–1960s)

Characteristics:
- Data stored in separate files
- Each application maintained its own data

Problems:
- High redundancy
- Poor sharing
- Difficult maintenance

---

## 2. Hierarchical Database Model (1960s)

Structure:
Tree-like organization

Parent → Child relationship

Example:
University
 └── Department
      └── Student

Features:
- One parent
- Many children

Example System:
IBM IMS

Limitation:
Child cannot easily have multiple parents.

---

## 3. Network Database Model (1970s)

Improvement over hierarchical model.

Features:
- Records can have multiple parents
- Many-to-many relationships supported

Example:
Student ↔ Course

Model:
CODASYL

Advantage:
More flexible than hierarchical databases.

---

## 4. Relational Database Model (1970s – Present)

Proposed by:
Edgar F. Codd

Stores data in tables (relations).

Example:

Student Table

| ID | Name |
|----|------|
| 1  | Sonam |
| 2  | Sangay |

Advantages:
- Simple structure
- Easy querying
- Reduced redundancy
- Uses SQL

Most popular model today.

---

## 5. Modern Database Systems

Types:

### Object-Oriented Databases
Store objects instead of simple rows.

### NoSQL Databases
Handle large-scale and unstructured data.

Examples:
- MongoDB
- Cassandra

### Distributed Databases
Data stored across multiple locations.

### Cloud Databases
Hosted on cloud platforms.

Examples:
- Amazon RDS
- Google Cloud SQL

---

# 7. Database-System Applications

## Banking
- Customer accounts
- Transactions
- Loans

## Airlines
- Flight schedules
- Ticket booking
- Reservations

## Universities
- Student records
- Registration
- Grades

## E-Commerce
- Products
- Orders
- Customers
- Payments

## Healthcare
- Patient records
- Appointments
- Medical history

## Telecommunications
- Billing systems
- Network usage

---

# 8. Database Languages

## A. DDL (Data Definition Language)

Used to define database structure.

Commands:
- CREATE
- ALTER
- DROP

Example:

CREATE TABLE Student (
    ID INT,
    Name VARCHAR(50)
);

---

## B. DML (Data Manipulation Language)

Used to manipulate stored data.

Commands:
- INSERT
- UPDATE
- DELETE
- SELECT

Example:

SELECT * FROM Student;

---

## C. DCL (Data Control Language)

Controls user permissions.

Commands:
- GRANT
- REVOKE

Example:

GRANT SELECT ON Student TO User1;

---

## D. TCL (Transaction Control Language)

Controls transactions.

Commands:
- COMMIT
- ROLLBACK

Example:

COMMIT;

Purpose:
Ensures database reliability.

---

# 9. SQL (Structured Query Language)

The standard language used with relational databases.

Main Functions:
- Create tables
- Insert records
- Retrieve data
- Update data
- Delete data
- Manage permissions

Example:

SELECT Name
FROM Student
WHERE ID = 1;

---

# 10. Database Design

Database design organizes data efficiently and minimizes redundancy.

## Stage 1: Conceptual Design

Focus:
Understanding business requirements.

Tool:
Entity Relationship (ER) Model

Example Entities:
- Student
- Course
- Enrollment

Questions:
- What data is needed?
- How are entities related?

---

## Stage 2: Logical Design

Convert ER model into relational tables.

Example:

Student Table
Course Table
Enrollment Table

Relationships are clearly defined.

---

## Stage 3: Physical Design

Focus:
How data is stored physically.

Includes:
- Storage methods
- Indexes
- Performance optimization

Goal:
Efficient retrieval and storage.

---

