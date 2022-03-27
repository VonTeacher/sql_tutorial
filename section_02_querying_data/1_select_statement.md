# SQL SELECT
Use SQL SELECT statement to query data from a single table.

## Introduction
Selects data from one or more tables.
```sql
SELECT select_list --specify a list of comma-separated values
FROM table_name;   --specify the table name
```
- When evaluating the `SELECT` statement, the system evaluates `FROM` first and then `SELECT`.

To query data from all columns of a table:
```sql
SELECT * FROM table;
```

## SQL SELECT Statement Examples
### `SELECT *`
- `SELECT *` is helpful for ad-hoc queries only, and not suitable for applicatoin development, as it returns data from all columns of a table. The database needs more time to read data from the disk and transfer it to an application.

### Specific Columns
```sql
SELECT employee_id,
       first_name,
       last_name,
       hire_date
FROM employees;
```

### Simple Calculation
```sql
SELECT first_name,
       last_name,
       salary,
       salary * 1.15 AS new_salary --alias
FROM employees;
```
- `AS` renames a column to something more helpful than the actual calculation
