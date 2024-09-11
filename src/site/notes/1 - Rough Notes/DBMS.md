---
{"dg-publish":true,"permalink":"/1-rough-notes/dbms/"}
---


# DBMS

11-09-2024 07:58

Status: 

Tags: 

Preparing for a technical interview on Database Management Systems (DBMS) involves understanding a wide range of topics, from the basics of databases to more advanced concepts like indexing, normalization, ACID properties, transactions, and query optimization. Let's dive deep into each of these topics step-by-step, making sure to use intuitive analogies to break down complex concepts into simpler, digestible parts.

### 1. **What is a Database and a DBMS?**

**Database**: Think of a database as a digital filing cabinet where information is stored in an organized way. Just like in a library, where books (data) are categorized by sections and organized in shelves, a database stores data in tables, which are like the bookshelves holding different types of information.

**DBMS (Database Management System)**: Now, imagine the librarian who manages the library—this librarian not only keeps track of where each book is but also helps people find books, borrow them, and ensures that borrowed books are returned in good condition. The DBMS is like this librarian; it is software that manages, retrieves, and manipulates the database efficiently. Examples include MySQL, PostgreSQL, MongoDB, and Oracle.

### 2. **Relational Model and SQL (Structured Query Language)**

A **Relational Database** is the most common type of database, and it organizes data into tables (like spreadsheets), where each table has rows and columns. Here are key points:

- **Tables**: Imagine a table as a grid. Each row in the table represents a record (like a single entry in a spreadsheet), and each column represents an attribute of that record (like "Name," "Age," "Email").
- **Primary Key**: This is a unique identifier for each record in a table. It's like a student's roll number in a classroom; no two students can have the same roll number.
- **Foreign Key**: Think of this as a reference. If one table refers to another table's primary key, that's a foreign key. Like how a student ID in the "Enrollment" table might reference the "Students" table.
  
**SQL (Structured Query Language)** is the language used to interact with relational databases. Key SQL commands include:
- **SELECT**: Fetch data from a database.
- **INSERT**: Add new data to a database.
- **UPDATE**: Modify existing data.
- **DELETE**: Remove data from a database.
  
Example:
```sql
SELECT * FROM Students WHERE Age > 18;
```
This query fetches all records from the `Students` table where the `Age` column is greater than 18.

### 3. **Normalization: Organizing Data Efficiently**

Imagine you have a closet where you store all your clothes, but instead of neatly folding them or hanging them up, everything is just thrown in there. It would be hard to find what you need! **Normalization** is the process of organizing data in a database to reduce redundancy and improve data integrity.

Normalization has several "normal forms" (NF):
- **1st Normal Form (1NF)**: Ensure each column contains atomic (indivisible) values. No repeating groups.
- **2nd Normal Form (2NF)**: Achieve 1NF and ensure no partial dependency (a non-key attribute depending on only part of a composite primary key).
- **3rd Normal Form (3NF)**: Achieve 2NF and remove transitive dependencies (non-key attributes depending on other non-key attributes).

**Example**: If a "Student" table has columns like `StudentID`, `Name`, and `Course1`, `Course2`, etc., we'd normalize by creating separate tables for "Students" and "Courses" and then linking them with a foreign key.

### 4. **ACID Properties: Ensuring Reliable Transactions**

When you transfer money from one bank account to another, you want to be sure that either the money is successfully transferred or not transferred at all—no halfway states. This reliability is achieved using **ACID properties**:
- **Atomicity**: Transactions are all-or-nothing.
- **Consistency**: Transactions bring the database from one valid state to another.
- **Isolation**: Concurrent transactions occur as if they were sequential.
- **Durability**: Once a transaction is committed, it remains even in case of a crash.

### 5. **Indexes: Speeding Up Data Retrieval**

An **Index** is like a book's index, where instead of flipping through every page to find a topic, you use the index to jump directly to the page number. In a database, an index improves the speed of data retrieval operations. However, they also take up extra space and can slow down `INSERT` or `UPDATE` operations because the index itself must be updated.

- **Types of Indexes**:
  - **Primary Index**: Built on a table's primary key.
  - **Secondary Index**: Built on non-key columns.
  - **Clustered Index**: Alters the physical order of the table.
  - **Non-Clustered Index**: A separate structure that points to the actual data.

### 6. **Joins: Combining Data from Multiple Tables**

A **JOIN** operation is like merging different sections of a library's catalog to provide a unified view. Types of joins include:
- **INNER JOIN**: Only returns records with matching values in both tables.
- **LEFT JOIN**: Returns all records from the left table and matched records from the right table.
- **RIGHT JOIN**: Opposite of LEFT JOIN.
- **FULL OUTER JOIN**: Returns records when there is a match in one of the tables.

### 7. **Transactions and Concurrency Control**

Transactions in DBMS ensure data integrity when multiple operations are performed. Think of a transaction as a safe box where all operations inside it must succeed for the whole transaction to succeed.

- **Locks**: Like a library that allows only one person at a time to borrow a book, locks ensure that only one transaction accesses data at a time.
- **Deadlock**: When two transactions wait on each other to release resources, like two people holding two parts of a torn book waiting for each other to release their parts.

### 8. **NoSQL Databases: An Alternative to Relational Databases**

NoSQL databases are like modern libraries without strict catalog rules. They are non-relational and designed to handle unstructured or semi-structured data, offering flexibility, scalability, and performance.

- **Types of NoSQL Databases**:
  - **Document-based** (e.g., MongoDB): Stores data in JSON-like documents.
  - **Key-Value Stores** (e.g., Redis): Data stored as key-value pairs.
  - **Column Family Stores** (e.g., Cassandra): Data stored in columns instead of rows.
  - **Graph Databases** (e.g., Neo4j): Stores data in nodes and edges, ideal for relationship-heavy data.

### 9. **Query Optimization**

Query optimization is like figuring out the fastest route to your destination using a GPS. The DBMS’s **query optimizer** evaluates different query plans to find the most efficient way to execute a given query.

- **Execution Plan**: Shows the steps the DBMS will take to execute a query.
- **Cost-Based Optimization**: Chooses the query plan with the lowest cost, based on factors like I/O operations and CPU usage.
  
### 10. **CAP Theorem in Distributed Databases**

For distributed databases, the **CAP Theorem** states that it is impossible for a distributed data store to simultaneously provide:
- **Consistency**: Every read receives the most recent write.
- **Availability**: Every request receives a response.
- **Partition Tolerance**: The system works despite network partitions.

### 11. **Common Database Design Patterns**

- **Star Schema**: Used in data warehousing, with a central fact table connected to dimension tables.
- **Snowflake Schema**: A more normalized version of the Star Schema with dimension tables further split into related tables.

### 12. **Backup and Recovery**

Just like you'd keep photocopies of important documents in case you lose the originals, databases need backup strategies. Types of backups include:
- **Full Backup**: Complete copy of the entire database.
- **Incremental Backup**: Only copies data that has changed since the last backup.
- **Differential Backup**: Copies all changes since the last full backup.

---

### Gauging Your Understanding

To ensure you have a solid foundation on these topics, please let me know your familiarity with the following concepts:

1. **Relational Database Basics (Tables, Keys, SQL)**
2. **Normalization and Data Integrity**
3. **ACID Properties and Transactions**
4. **Indexes and Query Optimization**
5. **NoSQL Databases and CAP Theorem**
6. **Database Design Patterns and Backup Strategies**

Feel free to specify any particular areas where you need a deeper dive or have questions.

Great! Let’s dive deeper into **Normalization** and the **ER (Entity-Relationship) Model** in DBMS, as these are fundamental concepts for designing efficient and well-structured databases.

### 1. **ER Model and ER Diagrams in DBMS**

The **Entity-Relationship (ER) Model** is a conceptual framework used to describe the structure of a database. It focuses on entities (things that need to be represented in the database), their attributes (properties of these entities), and the relationships between these entities. ER modeling helps in visualizing and planning how data is connected, which is crucial when designing databases.

#### **Key Components of ER Diagrams:**
- **Entities**: These are objects or things that exist independently and have attributes. Entities are represented by rectangles in ER diagrams. For example, in a university database, entities could be `Student`, `Course`, and `Instructor`.
- **Attributes**: Attributes are properties or details of an entity. They are represented by ovals connected to their respective entity. For example, `Student` might have attributes like `StudentID`, `Name`, `Age`, and `Email`.
- **Primary Key**: A unique identifier for each entity, underlined in ER diagrams. For example, `StudentID` could be the primary key for the `Student` entity.
- **Relationships**: These are associations between entities. They are represented by diamonds in ER diagrams. For example, `Enrolls` could be a relationship between `Student` and `Course`.
- **Cardinality**: This defines the number of instances of one entity that can be associated with another. Cardinality can be one-to-one (1:1), one-to-many (1:M), or many-to-many (M:N).

#### **Example of an ER Diagram: University Database**
Let's say we are creating a database for a university. The ER diagram might look like this:

1. **Entities**: `Student`, `Course`, `Instructor`
2. **Attributes**:
   - `Student`: `StudentID` (Primary Key), `Name`, `Age`, `Email`
   - `Course`: `CourseID` (Primary Key), `CourseName`, `Credits`
   - `Instructor`: `InstructorID` (Primary Key), `Name`, `Department`
3. **Relationships**:
   - `Enrolls`: between `Student` and `Course` (Many-to-Many)
   - `Teaches`: between `Instructor` and `Course` (One-to-Many)

### 2. **Normalization in Detail: 1NF, 2NF, and 3NF**

**Normalization** is a process of organizing data in a database to avoid redundancy and ensure data integrity. It involves dividing large tables into smaller, more manageable tables and defining relationships between them.

#### **Step-by-Step Normalization Process:**

Let's consider a dummy database to understand the normalization forms: 

### **Dummy Database Example:**

Suppose we have a table named `StudentCourses` with the following columns:

| StudentID | Name       | CourseID | CourseName       | InstructorName | InstructorDept |
|-----------|------------|----------|------------------|----------------|----------------|
| 101       | Alice      | CSE101   | Data Structures  | Dr. Smith      | Computer Science|
| 102       | Bob        | CSE101   | Data Structures  | Dr. Smith      | Computer Science|
| 103       | Charlie    | MAT201   | Calculus         | Dr. Jones      | Mathematics     |
| 101       | Alice      | MAT201   | Calculus         | Dr. Jones      | Mathematics     |

This table has redundant data and can be normalized step-by-step.

#### **1st Normal Form (1NF): Ensure Atomicity and Uniqueness**

**Definition**: A table is in **1NF** if:
- It contains only atomic (indivisible) values; no repeating groups or arrays.
- Each column contains only one value per row.

**Applying 1NF to `StudentCourses` Table**:
- Our table already satisfies atomicity because each field has only one value.
- However, we still have redundant data (e.g., `Dr. Smith` and `Computer Science` repeating for `CourseID CSE101`).

### **Resulting 1NF Table:**

| StudentID | Name    | CourseID | CourseName        | InstructorName | InstructorDept |
|-----------|---------|----------|-------------------|----------------|----------------|
| 101       | Alice   | CSE101   | Data Structures   | Dr. Smith      | Computer Science|
| 102       | Bob     | CSE101   | Data Structures   | Dr. Smith      | Computer Science|
| 103       | Charlie | MAT201   | Calculus          | Dr. Jones      | Mathematics     |
| 101       | Alice   | MAT201   | Calculus          | Dr. Jones      | Mathematics     |

*1NF does not remove redundancy; it just ensures that the structure is flat.*

#### **2nd Normal Form (2NF): Eliminate Partial Dependencies**

**Definition**: A table is in **2NF** if:
- It is in 1NF.
- There is no **partial dependency** (no non-key attribute depends on a part of a composite primary key).

In our case:
- The `StudentID` and `CourseID` together form a composite primary key for `StudentCourses`. 
- However, `CourseName`, `InstructorName`, and `InstructorDept` depend only on `CourseID`, not on the combination of `StudentID` and `CourseID`.

**To achieve 2NF**, we need to separate the table into two tables:
- **StudentCourses** with only `StudentID` and `CourseID`.
- **Courses** with `CourseID`, `CourseName`, `InstructorName`, `InstructorDept`.

### **Resulting 2NF Tables:**

**StudentCourses Table:**

| StudentID | CourseID |
|-----------|----------|
| 101       | CSE101   |
| 102       | CSE101   |
| 103       | MAT201   |
| 101       | MAT201   |

**Courses Table:**

| CourseID | CourseName       | InstructorName | InstructorDept  |
|----------|------------------|----------------|-----------------|
| CSE101   | Data Structures  | Dr. Smith      | Computer Science|
| MAT201   | Calculus         | Dr. Jones      | Mathematics     |

Now, `CourseName`, `InstructorName`, and `InstructorDept` are fully dependent on `CourseID` and no longer have partial dependencies.

#### **3rd Normal Form (3NF): Remove Transitive Dependencies**

**Definition**: A table is in **3NF** if:
- It is in 2NF.
- There is no **transitive dependency** (non-key attributes do not depend on other non-key attributes).

In the `Courses` table:
- `InstructorDept` depends on `InstructorName`, not directly on `CourseID`. This is a transitive dependency.

**To achieve 3NF**, we create a separate table for instructors:

### **Resulting 3NF Tables:**

**StudentCourses Table:**

| StudentID | CourseID |
|-----------|----------|
| 101       | CSE101   |
| 102       | CSE101   |
| 103       | MAT201   |
| 101       | MAT201   |

**Courses Table:**

| CourseID | CourseName       | InstructorName |
|----------|------------------|----------------|
| CSE101   | Data Structures  | Dr. Smith      |
| MAT201   | Calculus         | Dr. Jones      |

**Instructors Table:**

| InstructorName | InstructorDept  |
|----------------|-----------------|
| Dr. Smith      | Computer Science|
| Dr. Jones      | Mathematics     |

Now, each table is in 3NF:
- `StudentCourses` has no partial or transitive dependencies.
- `Courses` has no partial or transitive dependencies.
- `Instructors` table is also normalized with no unnecessary dependencies.

### **Summary of Normalization Steps:**

1. **1NF**: Ensure that all columns are atomic and there are no repeating groups.
2. **2NF**: Remove partial dependencies by ensuring that non-key attributes depend on the entire primary key.
3. **3NF**: Remove transitive dependencies by ensuring that non-key attributes depend only on the primary key and not on other non-key attributes.

### **Benefits of Normalization:**
- **Reduced Data Redundancy**: No repeating data, which saves storage space.
- **Improved Data Integrity**: Changes in one place propagate correctly, avoiding inconsistencies.
- **Easier Maintenance**: Easier to manage and update normalized databases.

Would you like to explore any specific normalization forms further, or perhaps dive into practical examples of SQL commands that manipulate these normalized tables?

Let's analyze the table in the image to determine which normal forms it satisfies. The table named **Player_Inventory** has the following columns:

- `Player_ID`: Identifier for each player.
- `Item_Type`: Type of item a player possesses.
- `Item_Quantity`: Quantity of the item that the player possesses.

### Step-by-step Analysis:

#### **1st Normal Form (1NF): Atomic Values**
- **Requirement**: Each column must have atomic (indivisible) values, and each entry in the table must contain only one value.
- **Analysis**: 
  - All columns (`Player_ID`, `Item_Type`, `Item_Quantity`) have atomic values. There are no repeating groups or arrays.
- **Conclusion**: The table **satisfies 1NF**.

#### **2nd Normal Form (2NF): Eliminate Partial Dependencies**
- **Requirement**: The table must be in 1NF, and there should be no partial dependency of any column on the primary key.
  - A **partial dependency** occurs when a non-key attribute is dependent on only a part of a composite primary key.
- **Primary Key Analysis**:
  - In this table, there isn't a composite primary key; `Player_ID` and `Item_Type` together can uniquely identify each row.
  - No non-key attribute (`Item_Quantity`) depends on just one part of the composite key (`Player_ID` or `Item_Type`). It depends on both.
- **Conclusion**: The table **satisfies 2NF**.

#### **3rd Normal Form (3NF): Eliminate Transitive Dependencies**
- **Requirement**: The table must be in 2NF, and there should be no transitive dependency between non-key attributes.
  - A **transitive dependency** occurs when a non-key attribute depends on another non-key attribute rather than depending on the primary key.
- **Analysis**:
  - `Item_Quantity` directly depends on the combination of `Player_ID` and `Item_Type`, and there are no non-key attributes depending on each other.
- **Conclusion**: The table **satisfies 3NF**.

### **Final Conclusion:**
This table satisfies **1NF, 2NF, and 3NF**. 

If you have any more questions or want to go deeper into normalization or other DBMS concepts, let me know!

Let's dive into SQL queries using the normalized tables from our earlier **university database** example. We'll cover a range of SQL queries from basic to advanced, gradually increasing in complexity to help you prepare for your technical interview.

### Recap of the Normalized Tables

We have three normalized tables in **3NF**:

**1. `StudentCourses` Table:**

| StudentID | CourseID |
|-----------|----------|
| 101       | CSE101   |
| 102       | CSE101   |
| 103       | MAT201   |
| 101       | MAT201   |

**2. `Courses` Table:**

| CourseID | CourseName       | InstructorName |
|----------|------------------|----------------|
| CSE101   | Data Structures  | Dr. Smith      |
| MAT201   | Calculus         | Dr. Jones      |

**3. `Instructors` Table:**

| InstructorName | InstructorDept  |
|----------------|-----------------|
| Dr. Smith      | Computer Science|
| Dr. Jones      | Mathematics     |

### Basic SQL Queries

1. **Selecting All Records from a Table:**

   ```sql
   SELECT * FROM StudentCourses;
   ```
   This query retrieves all rows and columns from the `StudentCourses` table.

2. **Selecting Specific Columns:**

   ```sql
   SELECT StudentID, CourseID FROM StudentCourses;
   ```
   This query retrieves only the `StudentID` and `CourseID` columns from the `StudentCourses` table.

3. **Filtering Data Using `WHERE` Clause:**

   ```sql
   SELECT * FROM Courses
   WHERE InstructorName = 'Dr. Smith';
   ```
   This query retrieves courses taught by "Dr. Smith".

4. **Sorting Results Using `ORDER BY`:**

   ```sql
   SELECT * FROM Courses
   ORDER BY CourseName ASC;
   ```
   This query retrieves all courses sorted in ascending order by `CourseName`.

### Intermediate SQL Queries

5. **Using `JOIN` to Combine Tables:**

   To find out which students are enrolled in which courses:

   ```sql
   SELECT SC.StudentID, C.CourseName
   FROM StudentCourses SC
   JOIN Courses C ON SC.CourseID = C.CourseID;
   ```
   This query combines `StudentCourses` and `Courses` using the `CourseID` key.

6. **Filtering with `JOIN`:**

   Find out which students are enrolled in "Data Structures":

   ```sql
   SELECT SC.StudentID, C.CourseName
   FROM StudentCourses SC
   JOIN Courses C ON SC.CourseID = C.CourseID
   WHERE C.CourseName = 'Data Structures';
   ```

7. **Using `GROUP BY` and `COUNT` for Aggregation:**

   To count the number of students enrolled in each course:

   ```sql
   SELECT C.CourseName, COUNT(SC.StudentID) AS StudentCount
   FROM StudentCourses SC
   JOIN Courses C ON SC.CourseID = C.CourseID
   GROUP BY C.CourseName;
   ```
   This query groups the results by `CourseName` and counts the number of students in each course.

8. **Using `HAVING` to Filter Aggregated Results:**

   To get courses with more than one student enrolled:

   ```sql
   SELECT C.CourseName, COUNT(SC.StudentID) AS StudentCount
   FROM StudentCourses SC
   JOIN Courses C ON SC.CourseID = C.CourseID
   GROUP BY C.CourseName
   HAVING COUNT(SC.StudentID) > 1;
   ```

### Advanced SQL Queries

9. **Using Subqueries:**

   Find students who are enrolled in all courses taught by "Dr. Smith":

   ```sql
   SELECT StudentID
   FROM StudentCourses
   WHERE CourseID IN (
       SELECT CourseID
       FROM Courses
       WHERE InstructorName = 'Dr. Smith'
   );
   ```
   This query uses a subquery to first find `CourseID`s taught by "Dr. Smith" and then retrieves the `StudentID`s enrolled in those courses.

10. **Correlated Subqueries:**

    List students who have taken more than one course:

    ```sql
    SELECT DISTINCT SC1.StudentID
    FROM StudentCourses SC1
    WHERE (
        SELECT COUNT(DISTINCT SC2.CourseID)
        FROM StudentCourses SC2
        WHERE SC2.StudentID = SC1.StudentID
    ) > 1;
    ```
    Here, for each student (`SC1`), we count the number of distinct courses they have taken (`SC2`) and filter those with more than one.

11. **Using `CASE` for Conditional Logic:**

    Get the list of courses and classify them as "Beginner" or "Advanced" based on the course name (example logic):

    ```sql
    SELECT CourseName,
           CASE
               WHEN CourseName = 'Data Structures' THEN 'Advanced'
               WHEN CourseName = 'Calculus' THEN 'Beginner'
               ELSE 'Unknown'
           END AS CourseLevel
    FROM Courses;
    ```
    This query uses `CASE` to perform conditional checks and output a new column called `CourseLevel`.

12. **Complex `JOIN` Operations with Multiple Tables:**

    Find all instructors and the number of students enrolled in their courses:

    ```sql
    SELECT I.InstructorName, COUNT(SC.StudentID) AS StudentCount
    FROM Instructors I
    JOIN Courses C ON I.InstructorName = C.InstructorName
    JOIN StudentCourses SC ON C.CourseID = SC.CourseID
    GROUP BY I.InstructorName;
    ```
    This query involves multiple `JOIN` operations between `Instructors`, `Courses`, and `StudentCourses` tables to find the number of students each instructor teaches.

### Summary

These SQL queries range from basic `SELECT` statements to more advanced `JOIN`, `GROUP BY`, and subqueries. The complexity increases as we start combining tables, filtering results with aggregates, and using subqueries for more dynamic data retrieval.

If you'd like to explore any particular type of SQL query in more detail or want to practice with additional examples, feel free to ask!

Great question! The concepts of **vertical scalability** and **horizontal scalability** are key to understanding the architectural differences between SQL (relational) databases and NoSQL (non-relational) databases.

### **Vertical Scalability (Scaling Up)**

When we say that **SQL databases are vertically scalable**, it means that to handle an increasing load or more data, we typically scale up by adding more resources (e.g., CPU, RAM, storage) to a single server where the database is hosted.

- **Example:** Imagine you have a computer that runs a relational database like MySQL or PostgreSQL. As your data grows or more users start accessing your application, you might find that the database starts to slow down. To deal with this, you could upgrade the computer to one with a faster processor, more memory, or a larger hard drive.

- **Advantages:**
  - Consistency: Vertical scaling typically maintains strong ACID (Atomicity, Consistency, Isolation, Durability) properties, which is a hallmark of relational databases.
  - Simplicity: Managing a single, powerful server can be simpler from a software and operations perspective.
  
- **Disadvantages:**
  - **Limits:** There is a physical limit to how much you can scale vertically. There’s only so much CPU power or memory that can be added to a single machine.
  - **Cost:** High-end hardware can be very expensive.

### **Horizontal Scalability (Scaling Out)**

When we say that **NoSQL databases are horizontally scalable**, it means that to handle more data or an increasing load, you can scale out by adding more servers (nodes) to your database cluster. The data is distributed across multiple servers.

- **Example:** Imagine you're running a NoSQL database like MongoDB or Cassandra. As your application grows and needs to store more data or handle more requests, you can add more servers to your cluster. The database system automatically distributes data and load across these servers.

- **Advantages:**
  - **Flexibility:** Horizontal scaling allows you to scale out indefinitely as long as you can keep adding more machines. This makes it possible to handle extremely large datasets and high traffic volumes.
  - **Cost-Effective:** You can use multiple low-cost commodity servers instead of a single, expensive, high-end server.
  - **Fault Tolerance:** With data spread across multiple servers, the system can be designed to tolerate failures of individual servers, improving overall system availability.

- **Disadvantages:**
  - **Consistency:** Ensuring data consistency across a distributed system can be more challenging. NoSQL databases often use eventual consistency models rather than strong consistency.
  - **Complexity:** Managing a distributed system can be more complex. It may involve dealing with issues like data replication, partitioning, and network latency.

### **Summary**

- **SQL databases** are traditionally **vertically scalable**, meaning you scale by adding more power to a single server. This works well for applications that need strong consistency and don't need to scale beyond the capabilities of a single machine.
  
- **NoSQL databases** are designed to be **horizontally scalable**, allowing you to add more servers to handle more data and traffic. This makes them suitable for applications that need to scale massively or handle large amounts of unstructured data across many servers.

Each approach has its strengths and trade-offs, and the choice between them often depends on the specific needs and constraints of your application.


## References