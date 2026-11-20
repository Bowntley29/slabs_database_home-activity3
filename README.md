# Author:Bontle Mogapi

# 1. Software & OS Modes:
- Vertical Application Software is type of software is built specifically to serve the operational needs of a single industry segment.For example, they include software designed for hospital inventory, construction, or fast-food outlets. With the Horizontal Application Software, this is the type of software that is designed to perform general functions that are useful across a wide variety of businesses and industries. Their examples include accounting programs, word processing software and spreadsheets.
- Real-Time Processing is a type of mode that is required to respond to events immediately within a strict, fixed time interval. Because of its strict timing requirements, it is typically used in environments where immediate feedback is critical to keep operations safe, such as manufacturing plants and laboratory equipment monitoring.Batch Processing, unlike real-time systems batch processing collects transactions and processes them together in groups without any direct user interaction. It does not require immediate, fixed-interval responses to individual events as they happen.

# 2. Design Principles & Keys:
- Redundant Data is harmful to a database because of the following two reasons:
    1.) It causes storage space to be wasted, storing the same information multiple times across tables takes up unnecessary storage space.   
    2.) It creates data errors and inconsistency meaning duplicate records create inconsistencies and inaccuracies in the database. When data is flawed it com    promises the accuracy and completeness of the database, which leads to unreliable reports and poor decision-making. 
- A Primary Key is a column (such as SERIAL PRIMARY KEY) that uniquely identifies each individual row within a parent table and Foreign Key (created using theREFERENCES constraint) is placed in a child table to link a row in that child table back to a specific row in the parent table. By connecting the child tableto the parent table's primary key, the foreign key enforces valid references. This means a valid value must exist in the parent table before it can be referenced in the child table.

# 3. ER & Data Models:
# Online sourse platform 
- Two Entities  : a student and a course   
  Two Attributes: For a student: student ID and name, for the course: course code and course title/name
  One Relationship: A student enrolls in a course.
- The difference between a Conceptual and Physical data model is that a Conceptual data model defines what the system contains without focusing on technical implementation details. It is independent of any specific Database Management System (DBMS) and is typically used by business stakeholders and data architects.Then a Physical data model defines how the database is actually implemented within a specific DBMS (such as PostgreSQL). It is created by database administrators (DBAs) and developers to build the final database structure.

# Section 3: Practical PostgreSQL & DML Consolidation:

# SQL commands and outputs

```bash
psql -U postgres
```

```sql
CREATE DATABASE recap_s4_s6_db;
\c recap_s4_s6_db
```

## 2. DDL — Create Tables
```sql
CREATE TABLE courses (
    course_id SERIAL PRIMARY KEY,
    title VARCHAR(100) NOT NULL
);

CREATE TABLE enrollments (
    enrollment_id SERIAL PRIMARY KEY,
    student_name VARCHAR(100) NOT NULL,
    course_id INTEGER REFERENCES courses(course_id)
);
```

## 3. DML — Insert, Select, Update & Delete

### Insert Records
```sql
INSERT INTO courses (title)
VALUES ('Web Development'), ('Data Structures and Algorithms');

INSERT INTO enrollments (student_name, course_id)
VALUES ('Thabo Dlamini', 1), ('Kabelo Mokoena', 2), ('Zanele Nkosi', 2);
```

### View Initial Enrollments
```sql
SELECT * FROM enrollments;
```
**Output:**
```text
 enrollment_id |  student_name  | course_id
---------------+----------------+-----------
             7 | Thabo Dlamini  |         1
             8 | Kabelo Mokoena |         2
             9 | Zanele Nkosi   |         2
(3 rows)
```

### Update and Delete Records
```sql
UPDATE enrollments
SET student_name = 'Palesa Mogapi'
WHERE enrollment_id = 7;

DELETE FROM enrollments
WHERE enrollment_id = 9;
```

### Final Verification
```sql
SELECT * FROM enrollments;
```
**Output:**
```text
 enrollment_id |  student_name  | course_id
---------------+----------------+-----------
             7 | Palesa Mogapi  |         1
             8 | Kabelo Mokoena |         2
(2 rows)
```

