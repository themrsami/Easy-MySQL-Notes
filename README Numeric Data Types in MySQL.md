# README: Numeric Data Types in MySQL

This guide provides an in-depth look at all 13 numeric data types in MySQL, complete with examples, syntax, and practical use cases. By the end of this guide, you will have a clear understanding of how to store and handle numeric data effectively in MySQL.

## Table of Contents
1. [Introduction](#introduction)
2. [Numeric Data Types in MySQL](#numeric-data-types-in-mysql)
   - [TINYINT](#tinyint)
   - [SMALLINT](#smallint)
   - [MEDIUMINT](#mediumint)
   - [INT (INTEGER)](#int-integer)
   - [BIGINT](#bigint)
   - [DECIMAL (DEC)](#decimal-dec)
   - [FLOAT](#float)
   - [DOUBLE](#double)
   - [BIT](#bit)
   - [BOOL (BOOLEAN)](#bool-boolean)
   - [SERIAL](#serial)
   - [UNSIGNED](#unsigned)
   - [ZEROFILL](#zerofill)
3. [Numeric Functions in MySQL](#numeric-functions-in-mysql)
4. [Best Practices](#best-practices)
5. [Conclusion](#conclusion)

---

## Introduction

MySQL offers a variety of numeric data types to store integer, floating-point, and exact numeric values. Choosing the correct data type for your numeric data is crucial for optimizing performance, minimizing storage, and ensuring accuracy. This guide covers both signed and unsigned types, and it explains the precision and range of each data type.

---

## Numeric Data Types in MySQL

### 1. TINYINT
- **Definition**: `TINYINT` is a small integer that can store values from `-128` to `127` (signed) or `0` to `255` (unsigned).
- **Syntax**:
  ```sql
  TINYINT[(M)] [UNSIGNED] [ZEROFILL]
  ```

- **Example**:
  ```sql
  CREATE TABLE test (
      age TINYINT
  );

  INSERT INTO test (age) VALUES (25);

  SELECT age FROM test; -- Output: 25
  ```

### 2. SMALLINT
- **Definition**: `SMALLINT` is used for slightly larger integers, ranging from `-32,768` to `32,767` (signed) or `0` to `65,535` (unsigned).
- **Syntax**:
  ```sql
  SMALLINT[(M)] [UNSIGNED] [ZEROFILL]
  ```

- **Example**:
  ```sql
  CREATE TABLE employee_salaries (
      salary SMALLINT
  );

  INSERT INTO employee_salaries (salary) VALUES (15000);

  SELECT salary FROM employee_salaries; -- Output: 15000
  ```

### 3. MEDIUMINT
- **Definition**: `MEDIUMINT` stores medium-sized integers. It has a range of `-8,388,608` to `8,388,607` (signed) or `0` to `16,777,215` (unsigned).
- **Syntax**:
  ```sql
  MEDIUMINT[(M)] [UNSIGNED] [ZEROFILL]
  ```

- **Example**:
  ```sql
  CREATE TABLE account_balance (
      balance MEDIUMINT
  );

  INSERT INTO account_balance (balance) VALUES (500000);

  SELECT balance FROM account_balance; -- Output: 500000
  ```

### 4. INT (INTEGER)
- **Definition**: `INT` is the standard integer type in MySQL. It stores values from `-2,147,483,648` to `2,147,483,647` (signed) or `0` to `4,294,967,295` (unsigned).
- **Syntax**:
  ```sql
  INT[(M)] [UNSIGNED] [ZEROFILL]
  ```

- **Example**:
  ```sql
  CREATE TABLE employees (
      employee_id INT,
      name VARCHAR(50)
  );

  INSERT INTO employees (employee_id, name) VALUES (1, 'John');

  SELECT employee_id, name FROM employees; -- Output: 1, 'John'
  ```

### 5. BIGINT
- **Definition**: `BIGINT` stores very large integer values. It ranges from `-9,223,372,036,854,775,808` to `9,223,372,036,854,775,807` (signed) or `0` to `18,446,744,073,709,551,615` (unsigned).
- **Syntax**:
  ```sql
  BIGINT[(M)] [UNSIGNED] [ZEROFILL]
  ```

- **Example**:
  ```sql
  CREATE TABLE large_numbers (
      big_number BIGINT
  );

  INSERT INTO large_numbers (big_number) VALUES (123456789012345);

  SELECT big_number FROM large_numbers; -- Output: 123456789012345
  ```

### 6. DECIMAL (DEC)
- **Definition**: `DECIMAL` is used for storing exact numeric values, particularly for financial data, where precision is critical. It stores numbers as strings, allowing for accurate arithmetic calculations.
- **Syntax**:
  ```sql
  DECIMAL[(M, D)] [UNSIGNED] [ZEROFILL]
  ```
  Where `M` is the maximum number of digits and `D` is the number of decimal places.

- **Example**:
  ```sql
  CREATE TABLE prices (
      price DECIMAL(10, 2)
  );

  INSERT INTO prices (price) VALUES (12345.67);

  SELECT price FROM prices; -- Output: 12345.67
  ```

### 7. FLOAT
- **Definition**: `FLOAT` stores floating-point numbers with single precision, but it may result in slight rounding errors because it is not as precise as `DECIMAL`.
- **Syntax**:
  ```sql
  FLOAT[(M, D)] [UNSIGNED] [ZEROFILL]
  ```
  Where `M` is the maximum number of digits and `D` is the number of decimal places.

- **Example**:
  ```sql
  CREATE TABLE float_numbers (
      weight FLOAT(5, 2)
  );

  INSERT INTO float_numbers (weight) VALUES (65.43);

  SELECT weight FROM float_numbers; -- Output: 65.43
  ```

### 8. DOUBLE
- **Definition**: `DOUBLE` stores floating-point numbers with double precision, providing greater accuracy compared to `FLOAT`.
- **Syntax**:
  ```sql
  DOUBLE[(M, D)] [UNSIGNED] [ZEROFILL]
  ```

- **Example**:
  ```sql
  CREATE TABLE precise_measurements (
      measurement DOUBLE(10, 5)
  );

  INSERT INTO precise_measurements (measurement) VALUES (12345.67890);

  SELECT measurement FROM precise_measurements; -- Output: 12345.67890
  ```

### 9. BIT
- **Definition**: `BIT` stores bit values (binary values). It can be used to represent boolean flags or bit-level data.
- **Syntax**:
  ```sql
  BIT(M)
  ```
  Where `M` specifies the number of bits (from 1 to 64).

- **Example**:
  ```sql
  CREATE TABLE flags (
      flag BIT(1)
  );

  INSERT INTO flags (flag) VALUES (1);

  SELECT flag FROM flags; -- Output: 1
  ```

### 10. BOOL (BOOLEAN)
- **Definition**: `BOOL` or `BOOLEAN` is a synonym for `TINYINT(1)`, and stores a boolean value (`0` or `1`).
- **Syntax**:
  ```sql
  BOOL
  ```

- **Example**:
  ```sql
  CREATE TABLE boolean_test (
      is_active BOOL
  );

  INSERT INTO boolean_test (is_active) VALUES (1);

  SELECT is_active FROM boolean_test; -- Output: 1
  ```

### 11. SERIAL
- **Definition**: `SERIAL` is an alias for `BIGINT UNSIGNED NOT NULL AUTO_INCREMENT UNIQUE`. It's a convenient way to declare an auto-incrementing column for unique identifiers.
- **Syntax**:
  ```sql
  SERIAL
  ```

- **Example**:
  ```sql
  CREATE TABLE auto_increment_table (
      id SERIAL,
      name VARCHAR(50)
  );

  INSERT INTO auto_increment_table (name) VALUES ('Alice'), ('Bob');

  SELECT id, name FROM auto_increment_table;
  -- Output: 1, 'Alice'
  -- Output: 2, 'Bob'
  ```

### 12. UNSIGNED
- **Definition**: `UNSIGNED` is used as a modifier to any integer or decimal type to disallow negative values, thereby doubling the upper limit of the range.
- **Syntax**:
  ```sql
  [DataType] UNSIGNED
  ```

- **Example**:
  ```sql
  CREATE TABLE unsigned_numbers (
      positive_number INT UNSIGNED
  );

  INSERT INTO unsigned_numbers (positive_number) VALUES (100);

  SELECT positive_number FROM unsigned_numbers; -- Output: 100
  ```

### 13. ZEROFILL
- **Definition**: `ZEROFILL` pads the display of the numeric value with leading zeros to the specified width.
- **Syntax**:
  ```sql
  [DataType] ZEROFILL
  ```

-

 **Example**:
  ```sql
  CREATE TABLE zero_fill_example (
      order_id INT ZEROFILL
  );

  INSERT INTO zero_fill_example (order_id) VALUES (123);

  SELECT order_id FROM zero_fill_example; -- Output: 0000000123
  ```

---

## Numeric Functions in MySQL
Here are some common functions used to manipulate numeric data in MySQL:

1. **ABS()**: Returns the absolute value of a number.
   ```sql
   SELECT ABS(-10); -- Output: 10
   ```

2. **CEIL()**: Returns the smallest integer greater than or equal to a number.
   ```sql
   SELECT CEIL(4.3); -- Output: 5
   ```

3. **FLOOR()**: Returns the largest integer less than or equal to a number.
   ```sql
   SELECT FLOOR(4.7); -- Output: 4
   ```

4. **ROUND()**: Rounds a number to the nearest integer or specified number of decimal places.
   ```sql
   SELECT ROUND(123.456, 2); -- Output: 123.46
   ```

5. **MOD()**: Returns the remainder of one number divided by another.
   ```sql
   SELECT MOD(10, 3); -- Output: 1
   ```

---

## Best Practices
- Use `TINYINT`, `SMALLINT`, `MEDIUMINT`, and `BIGINT` depending on the expected range of values to optimize storage.
- Choose `DECIMAL` for financial or exact numeric data where precision is important.
- Avoid `FLOAT` and `DOUBLE` for currency and precise calculations due to potential rounding errors.
- Always declare whether an integer type should be `UNSIGNED` if you expect only positive values.
- Use `ZEROFILL` when you need formatted numbers with leading zeros.

---

## Conclusion
MySQL offers a wide range of numeric data types to cater to various storage and precision needs. By choosing the correct type for your data, you can improve the performance and efficiency of your database. This guide covers all 13 numeric types, including practical examples to help you make informed decisions when designing your database.

Happy coding! 😊

---