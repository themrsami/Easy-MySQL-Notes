# README: Date and Time Data Types in MySQL

This guide provides a detailed look at the 5 date and time data types available in MySQL, complete with syntax, examples, and best practices. By the end of this guide, you will understand how to store and manipulate temporal data in MySQL effectively.

## Table of Contents
1. [Introduction](#introduction)
2. [Date and Time Data Types in MySQL](#date-and-time-data-types-in-mysql)
   - [DATE](#date)
   - [DATETIME](#datetime)
   - [TIMESTAMP](#timestamp)
   - [TIME](#time)
   - [YEAR](#year)
3. [Date and Time Functions in MySQL](#date-and-time-functions-in-mysql)
4. [Best Practices](#best-practices)
5. [Conclusion](#conclusion)

---

## Introduction

Date and time data types in MySQL allow you to store various kinds of temporal information, such as dates, times, and timestamps. These types are essential for applications that handle scheduling, logging, or any other time-related data. MySQL provides several options for representing dates and times, depending on the level of detail and precision you require.

---

## Date and Time Data Types in MySQL

### 1. DATE
- **Definition**: `DATE` stores a date in the format `'YYYY-MM-DD'` without a time part.
- **Range**: From `'1000-01-01'` to `'9999-12-31'`
- **Storage**: 3 bytes
- **Syntax**:
  ```sql
  DATE
  ```

- **Example**:
  ```sql
  CREATE TABLE employees (
      hire_date DATE
  );

  INSERT INTO employees (hire_date) VALUES ('2023-10-19');

  SELECT hire_date FROM employees; -- Output: '2023-10-19'
  ```

### 2. DATETIME
- **Definition**: `DATETIME` stores a date and time in the format `'YYYY-MM-DD HH:MM:SS'`.
- **Range**: From `'1000-01-01 00:00:00'` to `'9999-12-31 23:59:59'`
- **Storage**: 8 bytes
- **Syntax**:
  ```sql
  DATETIME[(fsp)]
  ```
  Where `fsp` is the fractional seconds precision (0 to 6).

- **Example**:
  ```sql
  CREATE TABLE appointments (
      appointment_time DATETIME
  );

  INSERT INTO appointments (appointment_time) VALUES ('2023-10-19 14:30:00');

  SELECT appointment_time FROM appointments; -- Output: '2023-10-19 14:30:00'
  ```

### 3. TIMESTAMP
- **Definition**: `TIMESTAMP` stores both the date and time but tracks the time in UTC and automatically adjusts for the current time zone.
- **Range**: From `'1970-01-01 00:00:01 UTC'` to `'2038-01-19 03:14:07 UTC'`
- **Storage**: 4 bytes
- **Syntax**:
  ```sql
  TIMESTAMP[(fsp)]
  ```

- **Example**:
  ```sql
  CREATE TABLE logs (
      event_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  );

  INSERT INTO logs VALUES ();

  SELECT event_time FROM logs; -- Output: current timestamp, e.g., '2023-10-19 14:32:00'
  ```

### 4. TIME
- **Definition**: `TIME` stores only the time portion in the format `'HH:MM:SS'`.
- **Range**: From `'-838:59:59'` to `'838:59:59'`
- **Storage**: 3 bytes
- **Syntax**:
  ```sql
  TIME[(fsp)]
  ```

- **Example**:
  ```sql
  CREATE TABLE shifts (
      shift_start TIME
  );

  INSERT INTO shifts (shift_start) VALUES ('08:30:00');

  SELECT shift_start FROM shifts; -- Output: '08:30:00'
  ```

### 5. YEAR
- **Definition**: `YEAR` stores a year in a 4-digit format (or 2-digit format in deprecated versions).
- **Range**: From `1901` to `2155` (4-digit) and `70` to `99` mapped to `1970-1999` (2-digit).
- **Storage**: 1 byte
- **Syntax**:
  ```sql
  YEAR[(4)]
  ```

- **Example**:
  ```sql
  CREATE TABLE products (
      manufacture_year YEAR
  );

  INSERT INTO products (manufacture_year) VALUES (2023);

  SELECT manufacture_year FROM products; -- Output: 2023
  ```

---

## Date and Time Functions in MySQL

MySQL provides several functions to manipulate and query date and time data:

1. **NOW()**: Returns the current date and time.
   ```sql
   SELECT NOW(); -- Output: '2023-10-19 14:40:00'
   ```

2. **CURDATE()**: Returns the current date.
   ```sql
   SELECT CURDATE(); -- Output: '2023-10-19'
   ```

3. **CURTIME()**: Returns the current time.
   ```sql
   SELECT CURTIME(); -- Output: '14:40:00'
   ```

4. **DATE_ADD()**: Adds a specified interval to a date.
   ```sql
   SELECT DATE_ADD('2023-10-19', INTERVAL 5 DAY); -- Output: '2023-10-24'
   ```

5. **DATEDIFF()**: Returns the difference between two dates.
   ```sql
   SELECT DATEDIFF('2023-10-24', '2023-10-19'); -- Output: 5
   ```

6. **EXTRACT()**: Extracts a part of a date, such as year, month, day, etc.
   ```sql
   SELECT EXTRACT(YEAR FROM '2023-10-19'); -- Output: 2023
   ```

7. **STR_TO_DATE()**: Converts a string into a date using a specified format.
   ```sql
   SELECT STR_TO_DATE('19-10-2023', '%d-%m-%Y'); -- Output: '2023-10-19'
   ```

8. **DATE_FORMAT()**: Formats a date according to a specified pattern.
   ```sql
   SELECT DATE_FORMAT('2023-10-19', '%d/%m/%Y'); -- Output: '19/10/2023'
   ```

---

## Best Practices

- Use `DATE` for storing only date-related information (e.g., birthdays, due dates).
- Use `DATETIME` if you need to store both date and time without automatic timezone adjustments.
- Use `TIMESTAMP` for tracking events that need to be timezone-aware (e.g., log entries, user actions).
- Use `TIME` for representing time values without any date information (e.g., work shifts, store hours).
- Use `YEAR` for data where only the year is relevant (e.g., year of manufacture, year of graduation).
- Always use functions like `NOW()` or `CURDATE()` to capture the current date/time rather than manually entering it.

---

## Conclusion

This guide covers the 5 essential date and time data types in MySQL, with examples to help you understand their use cases. By choosing the appropriate data type and leveraging MySQL's built-in date/time functions, you can efficiently store and manipulate temporal data in your database.

Happy coding! 😊

---