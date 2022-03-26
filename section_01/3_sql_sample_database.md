# SQL Sample Database

## Schema
### Countries
|    Column    |         Type          | Collation | Nullable | Default
|--------------|-----------------------|-----------|----------|---------
 country_id   | character(2)          |           | not null |
 country_name | character varying(40) |           |          |
 region_id    | integer               |           | not null |
```sql
Indexes:
    "countries_pkey" PRIMARY KEY, btree (country_id)
Foreign-key constraints:
    "countries_region_id_fkey" FOREIGN KEY (region_id) REFERENCES regions(region_id) ON UPDATE CASCADE ON DELETE CASCADE
Referenced by:
    TABLE "locations" CONSTRAINT "locations_country_id_fkey" FOREIGN KEY (country_id) REFERENCES countries(country_id) ON UPDATE CASCADE ON DELETE CASCADE
```
---
### Departments
|     Column      |         Type          | Collation | Nullable |                      Default
-----------------|-----------------------|-----------|----------|----------------------------------------------------
 department_id   | integer               |           | not null | nextval('departments_department_id_seq'::regclass)
 department_name | character varying(30) |           | not null |
 location_id     | integer               |           |          |
```sql
Indexes:
    "departments_pkey" PRIMARY KEY, btree (department_id)
Foreign-key constraints:
    "departments_location_id_fkey" FOREIGN KEY (location_id) REFERENCES locations(location_id) ON UPDATE CASCADE ON DELETE CASCADE
Referenced by:
    TABLE "employees" CONSTRAINT "employees_department_id_fkey" FOREIGN KEY (department_id) REFERENCES departments(department_id) ON UPDATE CASCADE ON DELETE CASCADE
```
---
### Dependents
|    Column    |         Type          | Collation | Nullable |                     Default
--------------|-----------------------|-----------|----------|--------------------------------------------------
 dependent_id | integer               |           | not null | nextval('dependents_dependent_id_seq'::regclass)
 first_name   | character varying(50) |           | not null |
 last_name    | character varying(50) |           | not null |
 relationship | character varying(25) |           | not null |
 employee_id  | integer               |           | not null |
```sql
Indexes:
    "dependents_pkey" PRIMARY KEY, btree (dependent_id)
Foreign-key constraints:
    "dependents_employee_id_fkey" FOREIGN KEY (employee_id) REFERENCES employees(employee_id) ON UPDATE CASCADE ON DELETE CASCADE
```
---
### Employees
|    Column     |          Type          | Collation | Nullable |                    Default
---------------|------------------------|-----------|----------|------------------------------------------------
 employee_id   | integer                |           | not null | nextval('employees_employee_id_seq'::regclass)
 first_name    | character varying(20)  |           |          |
 last_name     | character varying(25)  |           | not null |
 email         | character varying(100) |           | not null |
 phone_number  | character varying(20)  |           |          |
 hire_date     | date                   |           | not null |
 job_id        | integer                |           | not null |
 salary        | numeric(8,2)           |           | not null |
 manager_id    | integer                |           |          |
 department_id | integer                |           |          |
```sql
Indexes:
    "employees_pkey" PRIMARY KEY, btree (employee_id)
Foreign-key constraints:
    "employees_department_id_fkey" FOREIGN KEY (department_id) REFERENCES departments(department_id) ON UPDATE CASCADE ON DELETE CASCADE
    "employees_job_id_fkey" FOREIGN KEY (job_id) REFERENCES jobs(job_id) ON UPDATE CASCADE ON DELETE CASCADE
    "employees_manager_id_fkey" FOREIGN KEY (manager_id) REFERENCES employees(employee_id) ON UPDATE CASCADE ON DELETE CASCADE
Referenced by:
    TABLE "dependents" CONSTRAINT "dependents_employee_id_fkey" FOREIGN KEY (employee_id) REFERENCES employees(employee_id) ON UPDATE CASCADE ON DELETE CASCADE
    TABLE "employees" CONSTRAINT "employees_manager_id_fkey" FOREIGN KEY (manager_id) REFERENCES employees(employee_id) ON UPDATE CASCADE ON DELETE CASCADE
```
---
### Jobs
|   Column   |         Type          | Collation | Nullable |               Default
------------|-----------------------|-----------|----------|--------------------------------------
 job_id     | integer               |           | not null | nextval('jobs_job_id_seq'::regclass)
 job_title  | character varying(35) |           | not null |
 min_salary | numeric(8,2)          |           |          |
 max_salary | numeric(8,2)          |           |          |
```sql
Indexes:
    "jobs_pkey" PRIMARY KEY, btree (job_id)
Referenced by:
    TABLE "employees" CONSTRAINT "employees_job_id_fkey" FOREIGN KEY (job_id) REFERENCES jobs(job_id) ON UPDATE CASCADE ON DELETE CASCADE
```
---
### Locations
|     Column     |         Type          | Collation | Nullable |                    Default
----------------|-----------------------|-----------|----------|------------------------------------------------
 location_id    | integer               |           | not null | nextval('locations_location_id_seq'::regclass)
 street_address | character varying(40) |           |          |
 postal_code    | character varying(12) |           |          |
 city           | character varying(30) |           | not null |
 state_province | character varying(25) |           |          |
 country_id     | character(2)          |           | not null |
```sql
Indexes:
    "locations_pkey" PRIMARY KEY, btree (location_id)
Foreign-key constraints:
    "locations_country_id_fkey" FOREIGN KEY (country_id) REFERENCES countries(country_id) ON UPDATE CASCADE ON DELETE CASCADE
Referenced by:
    TABLE "departments" CONSTRAINT "departments_location_id_fkey" FOREIGN KEY (location_id) REFERENCES locations(location_id) ON UPDATE CASCADE ON DELETE CASCADE
```
---
### Regions
|   Column    |         Type          | Collation | Nullable |                  Default
-------------|-----------------------|-----------|----------|--------------------------------------------
 region_id   | integer               |           | not null | nextval('regions_region_id_seq'::regclass)
 region_name | character varying(25) |           |          |
```sql
Indexes:
    "regions_pkey" PRIMARY KEY, btree (region_id)
Referenced by:
    TABLE "countries" CONSTRAINT "countries_region_id_fkey" FOREIGN KEY (region_id) REFERENCES regions(region_id) ON UPDATE CASCADE ON DELETE CASCADE
```
