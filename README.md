# SQL Learning Guide **🚀 Learning notes for sql via chatGPT**

## Overview

This guide provides a comprehensive overview of essential SQL topics with explanations and examples to help you become proficient in SQL programming with ChatGPT 🐾.

## Table of Contents

1. [Basic SQL Queries](#basic-sql-queries)
2. [Working with Databases and Tables](#working-with-databases-and-tables)
3. [Data Manipulation](#data-manipulation)
4. [Data Retrieval Techniques](#data-retrieval-techniques)
5. [Functions and Operators](#functions-and-operators)
6. [Indexes](#indexes)
7. [Constraints](#constraints)
8. [Transactions and Locks](#transactions-and-locks)
9. [Views](#views)
10. [Stored Procedures and Functions](#stored-procedures-and-functions)
11. [Triggers](#triggers)
12. [Database Normalization](#database-normalization)
13. [Query Optimization](#query-optimization)
14. [Data Security and Permissions](#data-security-and-permissions)
15. [Backup and Restore](#backup-and-restore)

---

## Basic SQL Queries

**SELECT Statement**

```sql
SELECT column1, column2
FROM table_name;
```

**Example:**

```sql
SELECT first_name, last_name
FROM employees;
```

**WHERE Clause**

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

**Example:**

```sql
SELECT first_name, last_name
FROM employees
WHERE department = 'Sales';
```

**ORDER BY**

```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 [ASC|DESC];
```

**Example:**

```sql
SELECT first_name, last_name
FROM employees
ORDER BY last_name ASC;
```

---

## Working with Databases and Tables

**Create Database**

```sql
CREATE DATABASE database_name;
```

**Example:**

```sql
CREATE DATABASE company_db;
```

**Create Table**

```sql
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    ...
);
```

**Example:**

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    hire_date DATE
);
```

**Drop Table**

```sql
DROP TABLE table_name;
```

**Example:**

```sql
DROP TABLE employees;
```

---

## Data Manipulation

**Insert Data**

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

**Example:**

```sql
INSERT INTO employees (employee_id, first_name, last_name, hire_date)
VALUES (1, 'John', 'Doe', '2024-01-15');
```

**Update Data**

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

**Example:**

```sql
UPDATE employees
SET hire_date = '2024-02-01'
WHERE employee_id = 1;
```

**Delete Data**

```sql
DELETE FROM table_name
WHERE condition;
```

**Example:**

```sql
DELETE FROM employees
WHERE employee_id = 1;
```

---

## Data Retrieval Techniques

**DISTINCT**

```sql
SELECT DISTINCT column1
FROM table_name;
```

**Example:**

```sql
SELECT DISTINCT department
FROM employees;
```

**LIMIT and OFFSET**

```sql
SELECT column1, column2
FROM table_name
LIMIT number OFFSET number;
```

**Example:**

```sql
SELECT first_name, last_name
FROM employees
LIMIT 10 OFFSET 20;
```

**Aggregation Functions**

```sql
SELECT AGGREGATE_FUNCTION(column)
FROM table_name
GROUP BY column;
```

**Example:**

```sql
SELECT COUNT(*)
FROM employees;
```

**JOINS**

- **INNER JOIN**

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

**Example:**

```sql
SELECT employees.first_name, departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.department_id;
```

- **LEFT JOIN**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```

**Example:**

```sql
SELECT employees.first_name, departments.department_name
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.department_id;
```

**Subqueries**

```sql
SELECT column1
FROM table_name
WHERE column2 = (SELECT column2 FROM table_name WHERE condition);
```

**Example:**

```sql
SELECT first_name
FROM employees
WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'Sales');
```

---

## Functions and Operators

**Mathematical Functions**

```sql
SELECT ROUND(column, 2)
FROM table_name;
```

**Example:**

```sql
SELECT ROUND(salary, 2)
FROM employees;
```

**String Functions**

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM employees;
```

**Example:**

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM employees;
```

**Date Functions**

```sql
SELECT CURDATE()
FROM table_name;
```

**Example:**

```sql
SELECT CURDATE();
```

**Logical Operators**

```sql
SELECT column1
FROM table_name
WHERE condition1 AND condition2;
```

**Example:**

```sql
SELECT first_name
FROM employees
WHERE department = 'Sales' AND hire_date > '2024-01-01';
```

**Comparison Operators**

```sql
SELECT column1
FROM table_name
WHERE column2 BETWEEN value1 AND value2;
```

**Example:**

```sql
SELECT first_name
FROM employees
WHERE hire_date BETWEEN '2024-01-01' AND '2024-12-31';
```

---

## Indexes

**Create Index**

```sql
CREATE INDEX index_name
ON table_name (column_name);
```

**Example:**

```sql
CREATE INDEX idx_last_name
ON employees (last_name);
```

**Primary and Unique Keys**

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name PRIMARY KEY (column_name);
```

**Example:**

```sql
ALTER TABLE employees
ADD CONSTRAINT pk_employee_id PRIMARY KEY (employee_id);
```

---

## Constraints

**NOT NULL**

```sql
ALTER TABLE table_name
MODIFY column_name datatype NOT NULL;
```

**Example:**

```sql
ALTER TABLE employees
MODIFY first_name VARCHAR(50) NOT NULL;
```

**UNIQUE**

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name UNIQUE (column_name);
```

**Example:**

```sql
ALTER TABLE employees
ADD CONSTRAINT unique_email UNIQUE (email);
```

**FOREIGN KEY**

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name FOREIGN KEY (column_name)
REFERENCES other_table (column_name);
```

**Example:**

```sql
ALTER TABLE employees
ADD CONSTRAINT fk_department
FOREIGN KEY (department_id) REFERENCES departments(department_id);
```

**DEFAULT**

```sql
ALTER TABLE table_name
ALTER COLUMN column_name SET DEFAULT default_value;
```

**Example:**

```sql
ALTER TABLE employees
ALTER COLUMN hire_date SET DEFAULT CURRENT_DATE;
```

---

## Transactions and Locks

**Begin Transaction**

```sql
BEGIN;
```

**Commit**

```sql
COMMIT;
```

**Rollback**

```sql
ROLLBACK;
```

**Example:**

```sql
BEGIN;
UPDATE employees SET salary = salary * 1.1 WHERE department = 'Sales';
COMMIT;
```

**Isolation Levels**

```sql
SET TRANSACTION ISOLATION LEVEL isolation_level;
```

**Example:**

```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

---

## Views

**Create View**

```sql
CREATE VIEW view_name AS
SELECT column1, column2
FROM table_name
WHERE condition;
```

**Example:**

```sql
CREATE VIEW sales_employees AS
SELECT first_name, last_name
FROM employees
WHERE department = 'Sales';
```

**Modify View**

```sql
CREATE OR REPLACE VIEW view_name AS
SELECT column1, column2
FROM table_name
WHERE new_condition;
```

---

## Stored Procedures and Functions

**Create Stored Procedure**

```sql
CREATE PROCEDURE procedure_name (parameters)
BEGIN
    -- SQL statements
END;
```

**Example:**

```sql
CREATE PROCEDURE get_employee_by_id (IN emp_id INT)
BEGIN
    SELECT * FROM employees WHERE employee_id = emp_id;
END;
```

**Create Function**

```sql
CREATE FUNCTION function_name (parameters)
RETURNS datatype
BEGIN
    -- SQL statements
    RETURN value;
END;
```

**Example:**

```sql
CREATE FUNCTION calculate_bonus (salary DECIMAL(10,2))
RETURNS DECIMAL(10,2)
BEGIN
    RETURN salary * 0.1;
END;
```

---

## Triggers

**Create Trigger**

```sql
CREATE TRIGGER trigger_name
BEFORE INSERT ON table_name
FOR EACH ROW
BEGIN
    -- SQL statements
END;
```

**Example:**

```sql
CREATE TRIGGER update_employee_salary
BEFORE UPDATE ON employees
FOR EACH ROW
BEGIN
    SET NEW.salary = NEW.salary * 1.05;
END;
```

---

## Database Normalization

**Normalization Forms**

- **1NF**: Ensure each column contains

 atomic values.
- **2NF**: Ensure each column depends on the whole primary key.
- **3NF**: Ensure columns depend only on the primary key.

**Example of 3NF:**

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(department_id)
);
```

---

## Query Optimization

**Explain Query**

```sql
EXPLAIN SELECT column1 FROM table_name WHERE condition;
```

**Example:**

```sql
EXPLAIN SELECT first_name FROM employees WHERE department = 'Sales';
```

**Common Pitfalls**

- Avoid `SELECT *`
- Use appropriate indexes
- Optimize JOINs and WHERE clauses

---

## Data Security and Permissions

**Grant Permissions**

```sql
GRANT permission ON table_name TO user;
```

**Example:**

```sql
GRANT SELECT ON employees TO user1;
```

**Revoke Permissions**

```sql
REVOKE permission ON table_name FROM user;
```

**Example:**

```sql
REVOKE SELECT ON employees FROM user1;
```

**Prevent SQL Injection**

- Use prepared statements
- Sanitize user inputs

**Example (Prepared Statements in MySQL):**

```sql
PREPARE stmt FROM 'SELECT * FROM employees WHERE employee_id = ?';
SET @id = 1;
EXECUTE stmt USING @id;
```

---

## Backup and Restore

**Create Backup**

```sql
BACKUP DATABASE database_name TO DISK = 'backup_path';
```

**Example:**

```sql
BACKUP DATABASE company_db TO DISK = '/backup/company_db.bak';
```

**Restore Backup**

```sql
RESTORE DATABASE database_name FROM DISK = 'backup_path';
```

**Example:**

```sql
RESTORE DATABASE company_db FROM DISK = '/backup/company_db.bak';
```

---
