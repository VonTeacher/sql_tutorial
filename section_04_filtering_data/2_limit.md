# LIMIT
Limits the number of rows returned from a query.

## Introduction
To limit the number of rows returned by a `SELECT` statement, you use `LIMIT` and `OFFSET` clauses.

```sql
SELECT column_list
FROM table1
ORDER BY columg_list
LIMIT row_count OFFSET offset_value;
```
- `LIMIT row_count` determines the number of rows returned by the query.
- `OFFSET offset_value` skips the offset_value of rows before beginning to return the rows.
  - The `OFFSET` clause is optional.
- When you use the `LIMIT` clause, it is important to use an `ORDER BY` clause to ensure the order of rows in the result set.

## `LIMIT` Examples
The following examples uses the `LIMIT` clause to return the first 5 rows:
```sql
SELECT employee_id, first_name, last_name
FROM employees
ORDER BY first_name
LIMIT 5;
```

The following examples uses both `LIMIT` and `OFFSET` to return five rows starting from the 4th row:
```sql
SELECT employee_id, first_name, last_name
FROM employees
ORDER BY first_name
LIMIT 5 OFFSET 3;
```

## Using `LIMIT` to get the top N rows with the highest or lowest value
```sql
SELECT employee_id, first_name, last_name, salary
FROM employees
ORDER BY salary DESC
LIMIT 5;
```
 employee_id | first_name | last_name |  salary
-------------|------------|-----------|----------
100 | Steven     | King      | 24000.00
102 | Lex        | De Haan   | 17000.00
101 | Neena      | Kochhar   | 17000.00
145 | John       | Russell   | 14000.00
146 | Karen      | Partners  | 13500.00

To get the five employees with the lowest salary, you sort the employees by salary in ascending order instead:
```sql
SELECT employee_id, first_name, last_name, salary
FROM employees
ORDER BY salary
LIMIT 5;
```
 employee_id | first_name |  last_name  | salary
-------------|------------|-------------|---------
119 | Karen      | Colmenares  | 2500.00
118 | Guy        | Himuro      | 2600.00
126 | Irene      | Mikkilineni | 2700.00
117 | Sigal      | Tobias      | 2800.00
116 | Shelli     | Baida       | 2900.00

## Getting rows with the Nth highest value
```sql
SELECT employee_id, first_name, last_name, salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 1;
```
 employee_id | first_name | last_name |  salary
-------------|------------|-----------|----------
101 | Neena      | Kochhar   | 17000.00
- NOTE: This query works with the assumption that every employee has a different salary. It will fail if there are two employees who have the same highest salary.

To fix this issue, you can get the second highest salary first using the following statement.
```sql
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 1;
#=> 17000
```
And pass the result to another query:
```sql
SELECT employee_id, first_name, last_name, salary
FROM employees
WHERE salary = 17000;
```
If you know subquery, you can combine both queries into a single query as follows:
```sql
SELECT employee_id, first_name, last_name, salary
FROM employees
WHERE salary = (
  SELECT DISTINCT salary
  FROM employees
  ORDER BY salary DESC
  LIMIT 1 OFFSET 1
);
```
 employee_id | first_name | last_name |  salary
-------------|------------|-----------|----------
101 | Neena      | Kochhar   | 17000.00
102 | Lex        | De Haan   | 17000.00
