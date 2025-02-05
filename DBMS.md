# DBMS vs RDBMS

## 1. DBMS (Database Management System)
### Definition
A **DBMS** is a software system that manages databases, allowing users to store, retrieve, update, and manage data.

### Types
DBMS can be:
- **Relational (RDBMS)**
- **Non-relational (NoSQL)**

### Structure
Can store data in various formats:
- Hierarchical
- Network-based
- Document-based
- Flat-file storage

### Examples
- Microsoft Access
- MongoDB
- Firebase
- XML databases

### Example of a Simple DBMS (Flat-File)
```plaintext
Name | Age | City
-----------------
John | 25  | NY
Jane | 30  | LA
```
🔹 No structured relationships, just raw data storage.

---

## 2. RDBMS (Relational Database Management System)
### Definition
An **RDBMS** is a type of DBMS that organizes data in tables with relationships based on **primary** and **foreign keys**.

### Structure
- Uses **tables** (rows & columns) with a predefined schema.
- Supports **SQL** as the standard query language.

### Examples
- MySQL
- PostgreSQL
- Microsoft SQL Server
- Oracle
- SQLite

### Example of RDBMS (Relational Structure)
```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(50),
    City VARCHAR(50)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```
🔹 Here, `Customers` and `Orders` are related through `CustomerID`.

---

## Key Differences Between DBMS & RDBMS

| Feature            | DBMS                            | RDBMS                                            |
|-------------------|--------------------------------|------------------------------------------------|
| **Data Storage**  | Unstructured or hierarchical  | Stored in tables (structured)                  |
| **Relationships** | No relationships              | Uses keys (Primary, Foreign) to relate tables  |
| **Data Integrity**| Lower                         | High (Constraints like PK, FK, ACID compliance) |
| **Query Language**| No strict SQL usage          | Uses SQL for queries                            |
| **Scalability**   | Good for small data          | Suitable for large, complex data               |

---

## Conclusion
- **DBMS** is a broad category of database management systems (**can be relational or non-relational**).
- **RDBMS** is a **specific type of DBMS** that organizes data into tables with relationships.
- If you're working with **structured, relational data**, you need **RDBMS** (e.g., MySQL, PostgreSQL).
- If you're handling **unstructured or semi-structured data**, a **non-relational DBMS** (e.g., MongoDB, Firebase) might be better.

Would you like an example of using SQL queries in an RDBMS? 🚀
