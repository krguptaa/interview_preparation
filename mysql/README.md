# MySQL Interview Questions & Answers — 10+ Years Experience

> A comprehensive MySQL interview preparation guide covering **Basic, Intermediate, Advanced, Query-Based, Performance, Indexing, Transactions, Concurrency, Database Design, and Production Troubleshooting**.

---

## 📚 Table of Contents

* [1. Basic MySQL Questions](#1-basic-mysql-questions)
* [2. Intermediate MySQL Questions](#2-intermediate-mysql-questions)
* [3. Advanced MySQL Questions](#3-advanced-mysql-questions)
* [4. SQL Query-Based Questions](#4-sql-query-based-questions)
* [5. Window Function Questions](#5-window-function-questions)
* [6. JOIN-Based Questions](#6-join-based-questions)
* [7. Indexing Questions](#7-indexing-questions)
* [8. EXPLAIN & Query Optimization](#8-explain--query-optimization)
* [9. Transactions & Concurrency](#9-transactions--concurrency)
* [10. Stored Procedures, Functions & Triggers](#10-stored-procedures-functions--triggers)
* [11. Database Design Questions](#11-database-design-questions)
* [12. Performance & Production Scenarios](#12-performance--production-scenarios)
* [13. Advanced SQL Challenges](#13-advanced-sql-challenges)
* [14. Senior-Level Scenario Questions](#14-senior-level-scenario-questions)
* [15. Quick Revision Checklist](#15-quick-revision-checklist)

---

# 1. Basic MySQL Questions

## Q1. What is MySQL?

### Answer

MySQL is a relational database management system (RDBMS) that uses SQL to store, retrieve, and manipulate structured data.

MySQL supports:

* Relational tables
* SQL queries
* Transactions
* Indexes
* Constraints
* Views
* Stored procedures
* Triggers
* Replication
* JSON data
* Multiple storage engines

For transactional applications, **InnoDB** is the commonly used storage engine.

---

## Q2. What is the difference between SQL and MySQL?

### Answer

| SQL                                          | MySQL                      |
| -------------------------------------------- | -------------------------- |
| Query language                               | Database management system |
| Defines how to interact with relational data | Stores and manages data    |
| Standard language                            | Specific database product  |
| Used by multiple RDBMSs                      | Implements SQL             |

### Example

```sql
SELECT *
FROM employees
WHERE salary > 100000;
```

`SELECT` and `WHERE` are SQL syntax, while MySQL is the database system executing the query.

---

## Q3. What is a Primary Key?

### Answer

A primary key uniquely identifies each record in a table.

```sql
CREATE TABLE employees (
    id BIGINT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(12,2)
);
```

### Important points

* Cannot contain `NULL`
* Must be unique
* One primary key constraint per table
* InnoDB uses the primary key as the clustered index

---

## Q4. What is a Foreign Key?

### Answer

A foreign key establishes a relationship between two tables and helps maintain referential integrity.

```sql
CREATE TABLE departments (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE employees (
    id BIGINT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(id)
);
```

---

## Q5. What is a UNIQUE constraint?

### Answer

A `UNIQUE` constraint prevents duplicate non-`NULL` values for the indexed key.

```sql
CREATE TABLE users (
    id BIGINT PRIMARY KEY,
    email VARCHAR(255) UNIQUE
);
```

---

## Q6. What is NULL?

### Answer

`NULL` represents an unknown, missing, or unavailable value.

It is different from:

```text
0
''
FALSE
```

### Correct

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

### Incorrect

```sql
SELECT *
FROM employees
WHERE manager_id = NULL;
```

---

## Q7. What is the difference between DELETE, TRUNCATE and DROP?

| Command    | Deletes Data | Deletes Table | Typical Use          |
| ---------- | -----------: | ------------: | -------------------- |
| `DELETE`   |          Yes |            No | Delete selected rows |
| `TRUNCATE` |          Yes |            No | Remove all rows      |
| `DROP`     |          Yes |           Yes | Remove table         |

### DELETE

```sql
DELETE FROM employees
WHERE id = 10;
```

### TRUNCATE

```sql
TRUNCATE TABLE employees;
```

### DROP

```sql
DROP TABLE employees;
```

---

## Q8. What is the difference between WHERE and HAVING?

### WHERE

Filters rows before aggregation.

```sql
SELECT *
FROM employees
WHERE salary > 100000;
```

### HAVING

Filters groups after aggregation.

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 5;
```

---

## Q9. What is the difference between CHAR and VARCHAR?

### CHAR

Fixed-length string.

```sql
CHAR(10)
```

### VARCHAR

Variable-length string.

```sql
VARCHAR(100)
```

For most application fields where string length varies, `VARCHAR` is generally preferred.

---

## Q10. What is a View?

### Answer

A view is a stored query that behaves like a virtual table.

```sql
CREATE VIEW active_employees AS
SELECT id, name, salary
FROM employees
WHERE status = 'ACTIVE';
```

Use:

```sql
SELECT *
FROM active_employees;
```

---

# 2. Intermediate MySQL Questions

## Q11. What is an Index?

### Answer

An index is a data structure that helps MySQL locate rows more efficiently.

```sql
CREATE INDEX idx_employee_department
ON employees(department_id);
```

### Advantages

* Faster reads
* Faster filtering
* Faster joins
* Can help sorting
* Can enable covering-index access

### Disadvantages

* Requires storage
* Slows inserts
* Slows updates
* Slows deletes
* Requires maintenance

---

## Q12. What is a Composite Index?

### Answer

An index containing multiple columns.

```sql
CREATE INDEX idx_employee_department_status
ON employees(department_id, status);
```

It can help:

```sql
SELECT *
FROM employees
WHERE department_id = 10
  AND status = 'ACTIVE';
```

---

## Q13. What is the Leftmost Prefix Rule?

Given:

```sql
CREATE INDEX idx_orders
ON orders(customer_id, status, order_date);
```

This index can generally support:

```sql
WHERE customer_id = 10;
```

and:

```sql
WHERE customer_id = 10
AND status = 'PAID';
```

But:

```sql
WHERE status = 'PAID';
```

does not efficiently use the index's leading portion because `customer_id` is not constrained.

---

## Q14. What is a Covering Index?

### Answer

A covering index contains all columns required by a query.

```sql
CREATE INDEX idx_customer_status
ON orders(customer_id, status);
```

Query:

```sql
SELECT customer_id, status
FROM orders
WHERE customer_id = 100;
```

MySQL may be able to satisfy the query directly from the index.

---

## Q15. What is Cardinality?

### Answer

Cardinality represents the number of distinct values in a column or index.

Example:

```text
status:

ACTIVE
ACTIVE
ACTIVE
ACTIVE
INACTIVE
```

This has relatively low cardinality.

Whereas:

```text
email:

a@example.com
b@example.com
c@example.com
...
```

usually has high cardinality.

---

## Q16. What is Selectivity?

### Answer

Selectivity describes how effectively a predicate reduces the number of candidate rows.

For example:

```sql
WHERE email = 'john@example.com'
```

is generally highly selective if email is unique.

Whereas:

```sql
WHERE status = 'ACTIVE'
```

may be poorly selective if 95% of rows are active.

---

## Q17. Why doesn't MySQL always use an index?

### Answer

Possible reasons include:

1. Table is small.
2. Index has poor selectivity.
3. Query returns a large percentage of rows.
4. Statistics are inaccurate.
5. Another index is cheaper.
6. Function is applied to the indexed column.
7. Implicit type conversion occurs.
8. Composite index order is inappropriate.
9. Full table scan is estimated to be cheaper.

---

# 3. Advanced MySQL Questions

## Q18. What is EXPLAIN?

### Answer

`EXPLAIN` displays the execution plan that MySQL expects to use for a query.

```sql
EXPLAIN
SELECT *
FROM employees
WHERE department_id = 10;
```

Important columns:

```text
id
select_type
table
type
possible_keys
key
key_len
rows
filtered
Extra
```

---

## Q19. What is EXPLAIN ANALYZE?

### Answer

`EXPLAIN ANALYZE` executes the query and provides actual execution information.

```sql
EXPLAIN ANALYZE
SELECT *
FROM employees
WHERE department_id = 10;
```

### Difference

```text
EXPLAIN
   ↓
Estimated execution plan

EXPLAIN ANALYZE
   ↓
Actual execution + runtime statistics
```

---

## Q20. Explain EXPLAIN `type`.

Common access types include:

```text
system
const
eq_ref
ref
range
index
ALL
```

Generally:

```text
const / eq_ref
      ↓
ref
      ↓
range
      ↓
index
      ↓
ALL
```

However, this is not an absolute "good-to-bad" ranking for every query. The correct plan depends on the query and data.

---

## Q21. What does `ALL` mean in EXPLAIN?

### Answer

`ALL` generally means a full table scan.

Example:

```text
type = ALL
```

But:

> `ALL` does not automatically mean the query is bad.

For a table with 100 rows, a full scan may be cheaper than an index lookup.

---

## Q22. What is `Using filesort`?

### Answer

`Using filesort` means MySQL needs an additional sorting operation.

Example:

```sql
SELECT *
FROM orders
ORDER BY order_date DESC;
```

If an appropriate index is unavailable, MySQL may need to perform additional sorting.

---

## Q23. What is `Using temporary`?

### Answer

It indicates MySQL is using a temporary structure while processing part of the query.

Common causes include:

* `GROUP BY`
* `DISTINCT`
* `ORDER BY`
* Complex joins

It should be investigated when the query processes large datasets.

---

## Q24. What is a Sargable Query?

A query is generally sargable when the predicate allows efficient index access.

### Better

```sql
SELECT *
FROM orders
WHERE order_date >= '2026-01-01'
AND order_date < '2027-01-01';
```

### Potentially problematic

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = 2026;
```

Applying a function to an indexed column can prevent efficient index access.

---

# 4. SQL Query-Based Questions

## Q25. Find the highest salary.

```sql
SELECT MAX(salary) AS highest_salary
FROM employees;
```

---

## Q26. Find the second-highest salary.

### Method 1

```sql
SELECT MAX(salary) AS second_highest_salary
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

### Method 2 — DENSE_RANK

```sql
SELECT salary
FROM (
    SELECT
        salary,
        DENSE_RANK() OVER (
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) x
WHERE rnk = 2;
```

---

## Q27. Find the Nth highest salary.

```sql
SELECT salary
FROM (
    SELECT
        salary,
        DENSE_RANK() OVER (
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) x
WHERE rnk = 5;
```

Change `5` to the required rank.

---

## Q28. Find duplicate salaries.

```sql
SELECT
    salary,
    COUNT(*) AS employee_count
FROM employees
GROUP BY salary
HAVING COUNT(*) > 1;
```

---

## Q29. Find employees with duplicate salaries.

```sql
SELECT e.*
FROM employees e
JOIN (
    SELECT salary
    FROM employees
    GROUP BY salary
    HAVING COUNT(*) > 1
) d
ON d.salary = e.salary;
```

---

## Q30. Find employees earning more than the company average.

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

## Q31. Find employees earning more than their department average.

```sql
SELECT *
FROM (
    SELECT
        e.*,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS department_avg
    FROM employees e
) x
WHERE salary > department_avg;
```

---

## Q32. Find the highest-paid employee in each department.

```sql
SELECT *
FROM (
    SELECT
        e.*,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees e
) x
WHERE rnk = 1;
```

---

## Q33. Find the top 3 employees in each department.

```sql
SELECT *
FROM (
    SELECT
        e.*,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC, id
        ) AS rn
    FROM employees e
) x
WHERE rn <= 3;
```

### If you want the top 3 distinct salary levels:

```sql
SELECT *
FROM (
    SELECT
        e.*,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees e
) x
WHERE rnk <= 3;
```

---

## Q34. Find employees earning more than their manager.

```sql
SELECT
    e.name AS employee_name,
    e.salary AS employee_salary,
    m.name AS manager_name,
    m.salary AS manager_salary
FROM employees e
JOIN employees m
    ON e.manager_id = m.id
WHERE e.salary > m.salary;
```

This is a **self-join**.

---

## Q35. Find employees without a manager.

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

---

## Q36. Find departments having more than 5 employees.

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 5;
```

---

## Q37. Find departments with no employees.

```sql
SELECT d.*
FROM departments d
LEFT JOIN employees e
    ON e.department_id = d.id
WHERE e.id IS NULL;
```

---

## Q38. Find the latest employee in each department.

```sql
SELECT *
FROM (
    SELECT
        e.*,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY joining_date DESC, id DESC
        ) AS rn
    FROM employees e
) x
WHERE rn = 1;
```

---

## Q39. Find the second latest employee in each department.

```sql
SELECT *
FROM (
    SELECT
        e.*,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY joining_date DESC, id DESC
        ) AS rn
    FROM employees e
) x
WHERE rn = 2;
```

---

## Q40. Find employees having the same salary.

```sql
SELECT e.*
FROM employees e
WHERE EXISTS (
    SELECT 1
    FROM employees e2
    WHERE e2.salary = e.salary
      AND e2.id <> e.id
);
```

---

# 5. Window Function Questions

## Q41. What is ROW_NUMBER()?

`ROW_NUMBER()` assigns a unique sequential number to each row.

```sql
SELECT
    name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_num
FROM employees;
```

---

## Q42. What is RANK()?

`RANK()` assigns the same rank to tied values but leaves gaps.

```text
Salary    Rank

100000     1
90000      2
90000      2
80000      4
```

---

## Q43. What is DENSE_RANK()?

`DENSE_RANK()` assigns the same rank to tied values without gaps.

```text
Salary    Dense Rank

100000     1
90000      2
90000      2
80000      3
```

---

## Q44. Difference between ROW_NUMBER, RANK and DENSE_RANK?

| Function       | Duplicate Values | Gap After Tie |
| -------------- | ---------------- | ------------- |
| `ROW_NUMBER()` | Different number | N/A           |
| `RANK()`       | Same rank        | Yes           |
| `DENSE_RANK()` | Same rank        | No            |

### Remember

```text
ROW_NUMBER  → Unique number
RANK        → Same rank + gaps
DENSE_RANK  → Same rank + no gaps
```

---

## Q45. What is LAG()?

`LAG()` retrieves a value from a previous row.

```sql
SELECT
    employee_id,
    salary,
    LAG(salary) OVER (
        PARTITION BY employee_id
        ORDER BY effective_date
    ) AS previous_salary
FROM employee_salary_history;
```

Useful for:

* Previous salary
* Previous transaction
* Previous month's revenue
* Comparing current and previous records

---

## Q46. What is LEAD()?

`LEAD()` retrieves a value from a following row.

```sql
SELECT
    employee_id,
    salary,
    LEAD(salary) OVER (
        PARTITION BY employee_id
        ORDER BY effective_date
    ) AS next_salary
FROM employee_salary_history;
```

---

## Q47. Calculate a running total.

```sql
SELECT
    order_date,
    amount,
    SUM(amount) OVER (
        ORDER BY order_date
    ) AS running_total
FROM orders;
```

---

## Q48. Calculate a running total per customer.

```sql
SELECT
    customer_id,
    order_date,
    amount,
    SUM(amount) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
    ) AS running_total
FROM orders;
```

---

# 6. JOIN-Based Questions

## Q49. What is INNER JOIN?

Returns rows matching in both tables.

```sql
SELECT
    e.name,
    d.name AS department
FROM employees e
INNER JOIN departments d
    ON d.id = e.department_id;
```

---

## Q50. What is LEFT JOIN?

Returns all rows from the left table and matching rows from the right table.

```sql
SELECT
    d.name,
    e.name
FROM departments d
LEFT JOIN employees e
    ON e.department_id = d.id;
```

---

## Q51. What is a SELF JOIN?

A table joined to itself.

Example:

```sql
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
    ON m.id = e.manager_id;
```

---

## Q52. Find customers who have never placed an order.

### LEFT JOIN

```sql
SELECT c.*
FROM customers c
LEFT JOIN orders o
    ON o.customer_id = c.id
WHERE o.id IS NULL;
```

### NOT EXISTS

```sql
SELECT c.*
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.id
);
```

---

# 7. Indexing Questions

## Q53. What is a clustered index?

In InnoDB, the primary key determines the clustered index organization of the table data.

The table rows are organized around the primary key.

Therefore, primary-key design can have significant storage and performance implications.

---

## Q54. What is a secondary index?

A secondary index is an index other than the clustered primary key.

```sql
CREATE INDEX idx_employee_salary
ON employees(salary);
```

In InnoDB, secondary indexes contain the indexed columns plus the primary key value used to locate the corresponding clustered record.

---

## Q55. Why shouldn't we create an index on every column?

Because indexes:

* Consume disk space
* Increase write cost
* Increase update/delete cost
* Increase maintenance
* Can increase optimizer complexity

Indexes should support actual query patterns.

---

## Q56. What is a composite index column order?

Given:

```sql
CREATE INDEX idx_orders
ON orders(customer_id, status, order_date);
```

Column order matters.

A common access pattern such as:

```sql
WHERE customer_id = ?
AND status = ?
ORDER BY order_date DESC
```

may benefit significantly from this index.

But the best index depends on the actual workload and execution plan.

---

# 8. EXPLAIN & Query Optimization

## Q57. How do you optimize a slow query?

### Answer

I normally follow this process:

```text
1. Reproduce the issue
2. Capture the query and parameters
3. Run EXPLAIN
4. Run EXPLAIN ANALYZE
5. Review access type
6. Review selected indexes
7. Compare estimated vs actual rows
8. Check joins
9. Check sorting
10. Check temporary operations
11. Check cardinality/statistics
12. Review indexes
13. Rewrite query if required
14. Benchmark the change
15. Monitor production
```

---

## Q58. Why is SELECT * not recommended?

Instead of:

```sql
SELECT *
FROM employees;
```

prefer:

```sql
SELECT
    id,
    name,
    department_id,
    salary
FROM employees;
```

Benefits:

* Less data transfer
* Less memory usage
* Better readability
* Can enable covering-index opportunities
* Less sensitive to schema changes

---

## Q59. Why can OFFSET pagination become slow?

Example:

```sql
SELECT *
FROM orders
ORDER BY id
LIMIT 50 OFFSET 1000000;
```

The database may need to process and skip a large number of rows.

### Keyset pagination

```sql
SELECT *
FROM orders
WHERE id > 1000000
ORDER BY id
LIMIT 50;
```

For large datasets, keyset pagination is often more efficient when the ordering requirements permit it.

---

## Q60. How do you optimize a query on a 100-million-row table?

Consider:

```text
1. Proper indexing
2. Composite indexes
3. Covering indexes
4. Sargable predicates
5. Efficient pagination
6. Avoid SELECT *
7. Query rewriting
8. Partitioning when appropriate
9. Archiving/retention
10. Read replicas for suitable workloads
11. Caching
12. Monitoring
13. Capacity planning
```

---

# 9. Transactions & Concurrency

## Q61. What is a Transaction?

A transaction is a logical unit of work that should be committed completely or rolled back.

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE id = 2;

COMMIT;
```

---

## Q62. What are ACID properties?

### Atomicity

All operations succeed or none are committed.

### Consistency

Data remains valid according to database constraints and transaction rules.

### Isolation

Concurrent transactions are isolated according to the isolation level.

### Durability

Committed data survives failures according to the database's durability guarantees.

---

## Q63. What are MySQL isolation levels?

MySQL/InnoDB supports:

```text
READ UNCOMMITTED
READ COMMITTED
REPEATABLE READ
SERIALIZABLE
```

InnoDB commonly defaults to:

```text
REPEATABLE READ
```

---

## Q64. What is a Deadlock?

Example:

```text
Transaction A
    ↓
Locks Row 1
    ↓
Waits for Row 2

Transaction B
    ↓
Locks Row 2
    ↓
Waits for Row 1
```

Neither transaction can continue.

MySQL detects the deadlock and rolls back one transaction.

### Prevention

* Consistent lock order
* Short transactions
* Proper indexes
* Avoid unnecessary locks
* Retry safely after deadlock

---

## Q65. What is Optimistic Locking?

Use a version column.

```sql
UPDATE employees
SET
    salary = 95000,
    version = version + 1
WHERE id = 10
AND version = 5;
```

If:

```text
affected_rows = 0
```

another transaction may have modified the record.

---

# 10. Stored Procedures, Functions & Triggers

## Q66. What is a Stored Procedure?

```sql
DELIMITER //

CREATE PROCEDURE GetEmployeesByDepartment(
    IN p_department_id INT
)
BEGIN
    SELECT *
    FROM employees
    WHERE department_id = p_department_id;
END //

DELIMITER ;
```

Execute:

```sql
CALL GetEmployeesByDepartment(1);
```

---

## Q67. What is a Stored Function?

A function returns a value.

Example:

```sql
CREATE FUNCTION calculate_bonus(
    p_salary DECIMAL(12,2)
)
RETURNS DECIMAL(12,2)
DETERMINISTIC
RETURN p_salary * 0.10;
```

---

## Q68. What is a Trigger?

A trigger executes automatically in response to table events.

Example:

```sql
CREATE TRIGGER employee_audit
AFTER UPDATE ON employees
FOR EACH ROW
INSERT INTO employee_audit_log
(
    employee_id,
    changed_at
)
VALUES
(
    NEW.id,
    CURRENT_TIMESTAMP
);
```

### Senior consideration

Triggers can introduce hidden side effects, so they should be used carefully.

---

# 11. Database Design Questions

## Q69. What is Normalization?

Normalization organizes data to reduce unnecessary duplication and update anomalies.

Common levels:

```text
1NF
2NF
3NF
BCNF
```

---

## Q70. What is Denormalization?

Denormalization intentionally duplicates or precomputes data to improve specific read workloads.

Examples:

* Reporting tables
* Summary tables
* Precomputed totals
* Read-heavy workloads

Trade-off:

```text
Faster Reads
     ↓
More Storage
     +
More Data Consistency Complexity
```

---

## Q71. Surrogate Key vs Natural Key

### Surrogate Key

```sql
id BIGINT AUTO_INCREMENT PRIMARY KEY
```

### Natural Key

A business value such as:

```text
email
product_code
employee_number
```

A common design is:

```text
Surrogate Primary Key
+
Unique Constraint on Business Key
```

---

# 12. Performance & Production Scenarios

## Q72. A query takes 2 seconds today and 30 seconds tomorrow. What do you check?

### Answer

Check:

```text
1. EXPLAIN ANALYZE
2. Execution plan changes
3. Table growth
4. Statistics
5. Index changes
6. Data distribution
7. Query parameters
8. Locks
9. Long-running transactions
10. CPU
11. Memory
12. Disk I/O
13. Concurrent workload
14. Recent application deployment
```

---

## Q73. MySQL is using an index but the query is still slow. Why?

Possible reasons:

* Index returns too many rows
* Low selectivity
* Many table lookups
* Poor composite-index design
* Expensive joins
* Sorting
* Aggregation
* Temporary operations
* Lock waits
* I/O bottleneck

Use:

```sql
EXPLAIN ANALYZE
```

to compare estimated and actual execution behavior.

---

## Q74. CPU suddenly reaches 100%. What do you check?

```sql
SHOW FULL PROCESSLIST;
```

Then investigate:

* Long-running queries
* Expensive joins
* Missing indexes
* Full scans
* Large sorts
* Large aggregations
* Query concurrency
* Recent deployments
* Data growth

---

## Q75. Database has too many connections. What do you check?

```sql
SHOW STATUS LIKE 'Threads_connected';

SHOW STATUS LIKE 'Threads_running';

SHOW VARIABLES LIKE 'max_connections';
```

Also investigate:

* Application connection pooling
* Connection leaks
* Long-running requests
* Idle connections
* Traffic spikes

Increasing `max_connections` blindly can increase memory pressure.

---

# 13. Advanced SQL Challenges

## Q76. Find the top 3 salaries in each department.

```sql
SELECT *
FROM (
    SELECT
        e.*,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees e
) x
WHERE rnk <= 3;
```

---

## Q77. Find employees whose salary is greater than their manager.

```sql
SELECT
    e.name AS employee,
    e.salary AS employee_salary,
    m.name AS manager,
    m.salary AS manager_salary
FROM employees e
JOIN employees m
    ON m.id = e.manager_id
WHERE e.salary > m.salary;
```

---

## Q78. Find the latest order for each customer.

```sql
SELECT *
FROM (
    SELECT
        o.*,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date DESC, id DESC
        ) AS rn
    FROM orders o
) x
WHERE rn = 1;
```

---

## Q79. Find the second latest order for each customer.

```sql
SELECT *
FROM (
    SELECT
        o.*,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date DESC, id DESC
        ) AS rn
    FROM orders o
) x
WHERE rn = 2;
```

---

## Q80. Find customers who placed an order in 2025 but not in 2026.

```sql
SELECT DISTINCT o.customer_id
FROM orders o
WHERE o.order_date >= '2025-01-01'
  AND o.order_date < '2026-01-01'
  AND NOT EXISTS (
      SELECT 1
      FROM orders o2
      WHERE o2.customer_id = o.customer_id
        AND o2.order_date >= '2026-01-01'
        AND o2.order_date < '2027-01-01'
  );
```

---

## Q81. Find duplicate transactions.

```sql
SELECT
    customer_id,
    amount,
    transaction_date,
    COUNT(*) AS duplicate_count
FROM transactions
GROUP BY
    customer_id,
    amount,
    transaction_date
HAVING COUNT(*) > 1;
```

---

## Q82. Calculate a running total.

```sql
SELECT
    order_date,
    amount,
    SUM(amount) OVER (
        ORDER BY order_date
    ) AS running_total
FROM orders;
```

---

## Q83. Calculate month-over-month sales.

```sql
WITH monthly_sales AS (
    SELECT
        YEAR(order_date) AS sales_year,
        MONTH(order_date) AS sales_month,
        SUM(amount) AS total_sales
    FROM orders
    GROUP BY
        YEAR(order_date),
        MONTH(order_date)
)
SELECT
    sales_year,
    sales_month,
    total_sales,
    LAG(total_sales) OVER (
        ORDER BY sales_year, sales_month
    ) AS previous_month_sales
FROM monthly_sales;
```

---

## Q84. Find employees whose salary increased.

```sql
WITH salary_history AS (
    SELECT
        employee_id,
        salary,
        effective_date,
        LAG(salary) OVER (
            PARTITION BY employee_id
            ORDER BY effective_date
        ) AS previous_salary
    FROM employee_salary_history
)
SELECT *
FROM salary_history
WHERE salary > previous_salary;
```

---

## Q85. Find users who have not logged in during the last 90 days.

```sql
SELECT u.*
FROM users u
WHERE NOT EXISTS (
    SELECT 1
    FROM user_logins l
    WHERE l.user_id = u.id
      AND l.login_date >= NOW() - INTERVAL 90 DAY
);
```

---

# 14. Senior-Level Scenario Questions

## Q86. A query is slow only in production. What could be the reason?

### Answer

I would compare:

```text
Development
    vs
Production
```

for:

* Number of rows
* Data distribution
* Indexes
* Statistics
* Execution plan
* Hardware
* Memory
* CPU
* Disk I/O
* Concurrent queries
* Locks
* Configuration
* Query parameters

A query that works on 100K rows may behave very differently on 100M rows.

---

## Q87. How would you optimize a 30-second query?

### Strong Senior Answer

> I would first capture the exact query and parameters and establish a baseline. Then I would run `EXPLAIN` and `EXPLAIN ANALYZE`, inspect the access paths, join order, estimated versus actual rows, indexes, sorting, temporary operations, and locking. Based on the bottleneck, I might rewrite the query, change an index, refresh statistics, or modify the data-access pattern. I would benchmark the change and validate its effect on other workloads before deploying it.

---

## Q88. What would you do if MySQL chooses the wrong index?

### Answer

I would not immediately force an index.

First check:

```text
1. EXPLAIN ANALYZE
2. Index statistics
3. Cardinality
4. Data distribution
5. Query selectivity
6. Composite-index order
7. Table size
8. Recent data changes
```

Then consider:

```sql
ANALYZE TABLE employees;
```

If the optimizer still makes an inappropriate choice, investigate query/index redesign and only use optimizer hints when there is a justified, measured reason.

---

## Q89. How would you handle millions of DELETE operations?

Avoid one enormous transaction where practical.

Use controlled batches:

```sql
DELETE FROM orders
WHERE created_at < '2020-01-01'
LIMIT 10000;
```

Repeat until complete.

Also consider:

* Proper indexes
* Transaction size
* Lock duration
* Undo/redo pressure
* Replication impact
* Archiving
* Partitioning where appropriate

---

## Q90. How do you prevent deadlocks?

### Answer

I would:

1. Keep transactions short.
2. Access resources in a consistent order.
3. Avoid unnecessary locking.
4. Ensure queries use appropriate indexes.
5. Avoid external calls inside transactions.
6. Inspect deadlock diagnostics.
7. Implement safe retry logic.

---

# 15. Quick Revision Checklist

## Basic

* [ ] What is MySQL?
* [ ] SQL vs MySQL
* [ ] Primary Key
* [ ] Foreign Key
* [ ] UNIQUE
* [ ] NULL
* [ ] DELETE vs TRUNCATE vs DROP
* [ ] WHERE vs HAVING
* [ ] CHAR vs VARCHAR
* [ ] Views

## Intermediate

* [ ] Index
* [ ] Composite Index
* [ ] Covering Index
* [ ] Cardinality
* [ ] Selectivity
* [ ] Leftmost Prefix
* [ ] Clustered Index
* [ ] Secondary Index
* [ ] EXISTS vs IN
* [ ] UNION vs UNION ALL

## Advanced

* [ ] EXPLAIN
* [ ] EXPLAIN ANALYZE
* [ ] Query execution plan
* [ ] Optimizer
* [ ] Statistics
* [ ] Sargability
* [ ] Window Functions
* [ ] CTE
* [ ] Transactions
* [ ] ACID
* [ ] MVCC
* [ ] Isolation Levels
* [ ] Locks
* [ ] Deadlocks

## Query-Based

* [ ] Second-highest salary
* [ ] Nth-highest salary
* [ ] Duplicate records
* [ ] Top N per group
* [ ] Highest salary per department
* [ ] Employee vs manager salary
* [ ] Latest record per group
* [ ] Running total
* [ ] LAG / LEAD
* [ ] Month-over-month calculation
* [ ] Customers without orders
* [ ] Gaps and islands
* [ ] Consecutive dates

## Performance

* [ ] Full table scan
* [ ] Index selection
* [ ] Composite indexes
* [ ] Covering indexes
* [ ] `Using filesort`
* [ ] `Using temporary`
* [ ] Large-table optimization
* [ ] Pagination
* [ ] Query profiling
* [ ] Slow query troubleshooting
* [ ] Connection management
* [ ] Lock troubleshooting

---

# 🎯 Final Interview Strategy for 10+ Years Experience

For a senior MySQL interview, don't stop at:

> **"What is an index?"**

Be prepared for:

```text
What is an index?
        ↓
How does it improve performance?
        ↓
Which index would you create?
        ↓
Why this column order?
        ↓
What if MySQL doesn't use it?
        ↓
What does EXPLAIN show?
        ↓
What does EXPLAIN ANALYZE show?
        ↓
What if estimated rows are very different from actual rows?
        ↓
What happens when the table has 100 million rows?
        ↓
What are the trade-offs?
```

The strongest senior-level answers demonstrate **SQL knowledge + execution-plan analysis + indexing strategy + transaction/concurrency knowledge + production troubleshooting + engineering trade-offs**.
