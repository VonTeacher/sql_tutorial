# SQL Syntax
Introduction to SQL syntax and help understand the details of SQL statements

## Declarative Language
A Sql statement begins with;
- a **verb** that describes an action, then
- a **subject**, and
- a **predicate**

```sql
SELECT first_name             # mandatory
FROM employees                # mandatory
WHERE YEAR(hire_date) = 2020; # optional
```

## SQL Commands
Commands are composed of tokens that can be literals, keywords, identifiers, or expressions. Tokens are separated by space, tabs, or newlines.

## Literals
Explicit values, which are also known as constants, of three kinds: **string**, **numeric**, and **binary**.

### String
```sql
'Student'    # SQL is case-sensitive
'2022-03-26'
'42'         # Note: 42 would be numeric
```
### Numeric
```sql
500
-3
1.25
```
### Binary
Sql represents binary values using the notation `x'0000'`, where each digit is hexadecimal.
```sql
x'01'
x'0f0ff'
```

## Keywords
```sql
SELECT, FROM, INSERT, UPDATE, DELETE, DROP, etc...
```

## Identifiers
Refer to specific objects in the database such as tables, columns, indexes, etc.

*SQL is case-insensitive with respect to keywords and identifiers.*
```sql
Select * From employees; # all are equivalent
SELECT * FROM EMPLOYEES;
select * from employees;
SELECT * FROM employees;
```

## Comments
```sql
SELECT employee_id, salary
FROM employees
WHERE salary > 100_000; --employees making bank

/* Pay your workers more, you bourgeoisie pig! */
UPDATE employees
SET salary = salary * 1.15
WHERE salary < 80_000;
```
