# README: Constraints in MySQL

This guide provides an in-depth look at constraints in MySQL, complete with syntax, examples, and best practices. Constraints are rules enforced on data columns to ensure the integrity, accuracy, and reliability of data in your MySQL tables. By the end of this guide, you will understand how to apply constraints effectively to maintain data consistency.

## Table of Contents
1. [Introduction](#introduction)
2. [Types of Constraints in MySQL](#types-of-constraints-in-mysql)
   - [NOT NULL Constraint](#not-null-constraint)
   - [UNIQUE Constraint](#unique-constraint)
   - [PRIMARY KEY Constraint](#primary-key-constraint)
   - [FOREIGN KEY Constraint](#foreign-key-constraint)
   - [CHECK Constraint](#check-constraint)
   - [DEFAULT Constraint](#default-constraint)
   - [AUTO_INCREMENT Constraint](#auto_increment-constraint)
3. [Enforcing Constraints](#enforcing-constraints)
4. [Best Practices](#best-practices)
5. [Conclusion](#conclusion)

---

## Introduction

Constraints in MySQL are rules applied to table columns that ensure the integrity of the data stored in a database. They help to ensure data accuracy, consistency, and reliability by enforcing specific requirements on the data. There are several types of constraints in MySQL, each serving a unique purpose. This guide will cover each constraint type, its usage, and examples.

---

## Types of Constraints in MySQL

### 1. NOT NULL Constraint
- **Definition**: Ensures that a column cannot have a `NULL` value. Every row must contain a value for this column.
- **Use Case**: Use this constraint when a column must have a value, such as `email` in a user table.

- **Syntax**:
  ```sql
  CREATE TABLE users (
      id INT,
      email VARCHAR(255) NOT NULL
  );
  ```

- **Example**:
  ```sql
  INSERT INTO users (id, email) VALUES (1, NULL); 
  -- This will result in an error because 'email' cannot be NULL.
  ```

### 2. UNIQUE Constraint
- **Definition**: Ensures that all values in a column are unique across rows, preventing duplicate values.
- **Use Case**: Use this constraint for columns where values must be distinct, such as usernames or email addresses.

- **Syntax**:
  ```sql
  CREATE TABLE products (
      product_id INT,
      serial_number VARCHAR(50) UNIQUE
  );
  ```

- **Example**:
  ```sql
  INSERT INTO products (product_id, serial_number) VALUES (1, 'SN1234');
  INSERT INTO products (product_id, serial_number) VALUES (2, 'SN1234');
  -- The second insert will fail because 'serial_number' must be unique.
  ```

### 3. PRIMARY KEY Constraint
- **Definition**: Combines `NOT NULL` and `UNIQUE`, ensuring that a column (or a set of columns) has unique, non-null values. A table can have only one primary key.
- **Use Case**: Use this constraint to uniquely identify rows in a table, such as the `id` column.

- **Syntax**:
  ```sql
  CREATE TABLE employees (
      employee_id INT PRIMARY KEY,
      name VARCHAR(100)
  );
  ```

- **Composite Key Syntax**:
  ```sql
  CREATE TABLE orders (
      order_id INT,
      product_id INT,
      PRIMARY KEY (order_id, product_id)
  );
  ```

- **Example**:
  ```sql
  INSERT INTO employees (employee_id, name) VALUES (1, 'John');
  INSERT INTO employees (employee_id, name) VALUES (1, 'Jane'); 
  -- The second insert will fail because 'employee_id' must be unique.
  ```

### 4. FOREIGN KEY Constraint
- **Definition**: Establishes a relationship between two tables by linking a column in one table to the primary key of another table. It ensures referential integrity.
- **Use Case**: Use this constraint when you need to create relationships between tables, like linking an `order` to a `customer`.

- **Syntax**:
  ```sql
  CREATE TABLE orders (
      order_id INT PRIMARY KEY,
      customer_id INT,
      CONSTRAINT fk_customer
      FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
  );
  ```

- **Example**:
  ```sql
  -- First, create the referenced table (customers):
  CREATE TABLE customers (
      customer_id INT PRIMARY KEY,
      name VARCHAR(100)
  );

  -- Then, create the referencing table (orders):
  CREATE TABLE orders (
      order_id INT PRIMARY KEY,
      customer_id INT,
      FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
  );

  INSERT INTO orders (order_id, customer_id) VALUES (1, 999); 
  -- This will fail because there is no customer with customer_id = 999.
  ```

### 5. CHECK Constraint
- **Definition**: Ensures that a column's value meets a specific condition.
- **Use Case**: Use this constraint when you need to enforce certain business rules, like a salary being greater than zero.

- **Syntax**:
  ```sql
  CREATE TABLE employees (
      employee_id INT,
      salary DECIMAL(10, 2),
      CONSTRAINT chk_salary
      CHECK (salary > 0)
  );
  ```

- **Example**:
  ```sql
  INSERT INTO employees (employee_id, salary) VALUES (1, -5000);
  -- This will fail because the salary must be greater than 0.
  ```

### 6. DEFAULT Constraint
- **Definition**: Provides a default value for a column when no value is specified.
- **Use Case**: Use this constraint when you want to set a default value for columns like `created_at` or `status`.

- **Syntax**:
  ```sql
  CREATE TABLE orders (
      order_id INT,
      order_status VARCHAR(50) DEFAULT 'Pending'
  );
  ```

- **Example**:
  ```sql
  INSERT INTO orders (order_id) VALUES (1);
  -- 'order_status' will automatically be set to 'Pending' because of the DEFAULT constraint.
  ```

### 7. AUTO_INCREMENT Constraint
- **Definition**: Automatically generates a unique value for the column when a new row is inserted. It is typically used for primary keys.
- **Use Case**: Use this constraint to create a unique identifier for each row, such as `id`.

- **Syntax**:
  ```sql
  CREATE TABLE customers (
      customer_id INT AUTO_INCREMENT,
      name VARCHAR(100),
      PRIMARY KEY (customer_id)
  );
  ```

- **Example**:
  ```sql
  INSERT INTO customers (name) VALUES ('John Doe');
  -- 'customer_id' will be automatically assigned the next available integer.
  ```

---

## Enforcing Constraints

When constraints are violated (such as inserting a duplicate value into a column with a `UNIQUE` constraint), MySQL will throw an error, preventing the invalid data from being entered. This ensures the integrity and reliability of the database.

If you need to temporarily disable foreign key checks, for example, when loading large amounts of data, you can use the following commands:

- **Disable Foreign Key Checks**:
  ```sql
  SET FOREIGN_KEY_CHECKS = 0;
  ```

- **Re-enable Foreign Key Checks**:
  ```sql
  SET FOREIGN_KEY_CHECKS = 1;
  ```

---

## Best Practices
- **Use Constraints for Data Integrity**: Constraints are crucial for ensuring that the data in your database is valid. Always use constraints where appropriate to enforce business rules.
  
- **Name Constraints Clearly**: Use meaningful names for your constraints (e.g., `fk_customer` for foreign keys) so that your schema is self-explanatory.

- **Composite Keys for Uniqueness**: If you need a combination of two or more columns to be unique, use a composite primary key or a `UNIQUE` constraint across multiple columns.

- **Leverage AUTO_INCREMENT**: Use the `AUTO_INCREMENT` constraint for primary keys to automatically generate unique identifiers for rows.

- **Use Foreign Keys for Referential Integrity**: Always define foreign keys when creating relationships between tables to prevent orphaned rows and maintain data consistency.

---

## Conclusion

Constraints in MySQL are essential tools for maintaining data integrity, consistency, and reliability. By applying the appropriate constraints, you can enforce business rules directly in the database and ensure that the data adheres to the expected standards. This guide covered the key constraints available in MySQL, along with practical examples to help you understand their usage.

Happy coding! 😊

---