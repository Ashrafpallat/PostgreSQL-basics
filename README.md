# PostgreSQL Cheat Sheet

## Connect to PostgreSQL
```sql
psql -U postgres
``` 

### List Databases
```sql
\l
```

### Create a New Database
```sql
CREATE DATABASE db_name;
```

### Drop a Database
 ```sql
 DROP DATABASE db_name;
```

### Connect to a Database
 ```sql
\c db_name
 ```

### Connect Again to PostgreSQL / Exit from Current Database
```sql
\c postgres
```

## Tables

### See All Tables in the Current Database
 ```sql
 \d
```

### See Details of a Table
```sql
\d table_name
```

### Create Table Without Constraints
```sql
CREATE TABLE table_name(id INT, name VARCHAR(50), email VARCHAR(50), date_of_birth DATE);
```

### Delete a Table
```sql
DROP TABLE table_name;
```

### Delete a Record
```sql
DELETE FROM employee WHERE name='muneer';
```

### Create Table With Constraints
```sql
CREATE TABLE table_name(id BIGSERIAL NOT NULL PRIMARY KEY, name VARCHAR(50) NOT NULL,email VARCHAR(50) NOT NULL UNIQUE, date_of_birth DATE);
```

## Data Manipulation

### Insert
```sql
INSERT INTO table_name (name, email, date_of_birth VALUES ('John', 'John@gmail.com', '1999-01-01');
```

### See Table Contents
```sql
SELECT * FROM table_name;
```

### Order By
```sql
select * from employee order by name ASC;
```
```sql
select * from employee order by name DESC;
```

### Where, AND
```sql
SELECT field_name FROM table_name WHERE name='muneer' AND date_of_birth='2000-10-01';
```

### Where + '<,>,='
```sql
 SELECT * FROM employee WHERE date_of_birth<'2000-01-09';
```

### Distinct
```sql
SELECT DISTINCT field_name FROM table_name;
```

### Alter Table
```sql
ALTER TABLE table_name ADD COLUMN gender VARCHAR(10);
```
```sql
alter table students drop column_name;
```
```sql
ALTER TABLE students ADD CONSTRAINT unique_email UNIQUE (email);
```

### Update
```sql
UPDATE table_name SET gender = 'Female'  WHERE name = 'Rose';
```

## Additional Table Features

### Created At
```sql
CREATE TABLE table_name (id SERIAL PRIMARY KEY,name VARCHAR(100),email VARCHAR(100),gender VARCHAR(10),created_at DATE DEFAULT CURRENT_DATE);
```

## Advanced Queries

### Limit
```sql
SELETCT * FROM table_name LIMIT 5;
```
```sql
SELECT * FROM table_name OFFSET 5 LIMIT 5;
```

### Fetch
```sql
 SELECT * FROM employee FETCH FIRST 5 ROWS ONLY;
```

### In
```sql
SELECT * FROM employee WHERE place IN('chennai','mumbai');
```

### Between
```sql
SELECT * FROM employee WHERE date_of_birth BETWEEN DATE '1999-01-01' AND '2005-01-02';
```

### Like
```sql
SELECT * FROM employee WHERE name LIKE 'd%';
```
```sql
SELECT * FROM employee WHERE name LIKE '%d';
```

### iLike
```sql
 SELECT * FROM employee WHERE name iLIKE '%d';
```

### Group By
```sql
SELECT place FROM employee GROUP BY place;
```
```sql
SELECT place,COUNT(*) FROM employee GROUP BY place;
```

### Having
```sql
SELECT place,COUNT(*) FROM employee GROUP BY place HAVING COUNT(*)>1;
```
```sql
SELECT place,COUNT(*) FROM employee GROUP BY place HAVING COUNT(*)=1;
```

### Aggregate Functions

#### Max
```sql
SELECT max(salary) FROM employee;
```

#### Min
```sql
SELECT min(salary) FROM employee;
```

#### Round
```sql
SELECT round(avg(salary)) FROM employee;
```

### Alias (AS)
```sql
select id,name,email,salary,(salary/10) as sample from employee;
```

### Coalesce
```sql
select id,name,mark,total,coalesce(email,'not found') from student
```

### Conflict
1. DO NOTHING: It doesn't update the record and doesn't show an error.
2. DO UPDATE: It updates the record.

### Upsert Query
Insert if there is no record exists, update if there is a record exists.

## Foreign Key

A foreign key links to the primary of another table.

```sql
CREATE TABLE addresses (id SERIAL PRIMARY KEY,emp_id INTEGER REFERENCES employees(id),city VARCHAR(100),district VARCHAR(100),pin VARCHAR(10));
```

## Joins

### Inner Join
```sql
select * from employees inner join addresses on employees.id=addresses.emp_id;
```

### Left Join
Show all data of left table and matching data of right

### Right Join
Show all data of right table and matching data of left

### Full Outer Join
Show the complete data of both tables

## Case Statement

```sql
select name,mark, 
case 
when mark>=180 then 'A+' 
when mark between 150 and 180 then 'A' 
when mark between 100 and 150 then 'B+' 
end from students;
```
### SUBQUERY:

A subquery, also known as a nested query or inner query, is a query nested within another SQL query. Subqueries are enclosed within parentheses and are used to return data that will be used in the main query's condition or selection criteria.

```sql
select * from employee wheren id= (select id from employee where name='muneer');
```

### TRANSTACTION

 ```sql
BEGIN;
 UPDATE employees
 SET salary = salary + 500;
 COMMIT;
```
