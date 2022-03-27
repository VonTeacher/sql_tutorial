# SQL Distinct
Learn how to use `DISTINCT` to remove duplicates from a result set.

## Introduction
```sql
SELECT DISTINCT column1, column2
FROM table;
```
- If you use one column after `DISTINCT`, it uses values in that column to evaluate duplicates.
- If you use two or more columns, it will use the combination of values in those columns to evaluate the duplicate.
- NOTE: If you want to select two columns and remove duplicates in one column, you should use `GROUP BY` instead.

### `DISTINCT` on one column
```sql
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC;
```

### `DISTINCT` on multiple columns
```sql
SELECT DISTINCT job_id, salary
FROM employees
ORDER BY job_id, salary DESC;
```

## SQL `DISTINCT` and `NULL`
`NULL` means unknown or missing data. Unlike values like numbers, `NULL` does not equal anything, even itself.
```sql
NULL = NULL --returns unknown
```

Return the distinct phone numbers of employees (only returns one `NULL`):
```sql
SELECT DISTINCT phone_number
FROM employees
ORDER BY phone_number;
```
