# SQL ORDER BY
How to use SQL `ORDER BY` clause to sort the result set based on specified criteria in ascending or descending orders.

## Introduction
`ORDER BY` is an optional clause of `SELECT` and allows to sort the rows returned by `SELECT` by one or more sort expressions in asc/desc order.
```sql
SELECT list
FROM table_name
ORDER BY sort_expression [ASC | DESC];
```
1. Place `ORDER BY` after `FROM`.
2. Specify a sort expression.
3. Use `ASC|DESC` to sort the result set in asc/desc order.
* Note: `ORDER BY` uses `ASC` by default.

`ORDER BY` allows sorting by multiple expressions:
```sql
SELECT list
FROM table_name
ORDER BY
    sort_expression_1 ASC --first sort
    sort_expression_2 DESC; --second sort
```

## `ORDER BY` Clause Examples
### Sort Values in One Column
```sql
SELECT employee_id,
    first_name,
    last_name,
    hire_date,
    salary
FROM employees
ORDER BY first_name;
```
### Multiple Columns
```sql
SELECT employee_id,
    first_name,
    last_name,
    hire_date,
    salary
FROM employees
ORDER BY
    first_name,
    last_name DESC;
```

### Numeric Column
```sql
SELECT employee_id,
    first_name,
    last_name,
    hire_date,
    salary
FROM employees
ORDER BY
    salary DESC;
```
### Date Example
```sql
SELECT employee_id,
    first_name,
    last_name,
    hire_date,
    salary
FROM employees
ORDER BY
    hire_date;
```
