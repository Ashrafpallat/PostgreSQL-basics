# PostgreSQL Cheat Sheet

## Connect to PostgreSQL
```psql -U postgres``` 

### List Databases
```\l```

### Create a New Database
``` CREATE DATABASE db_name;```

### Drop a Database
 ```DROP DATABASE db_name;```

### Connect to a Database
 ```\c db_name```

### Connect Again to PostgreSQL / Exit from Current Database
``` \c postgres```

## Tables

### See All Tables in the Current Database
 ```\d```

### See Details of a Table
```\d table_name```

### Create Table Without Constraints
```CREATE TABLE table_name(id INT, name VARCHAR(50), email VARCHAR(50), date_of_birth DATE);```

### Delete a Table
```DROP TABLE table_name;```

### Delete a Record
```DELETE FROM employee WHERE name='muneer';```

### Create Table With Constraints
```CREATE TABLE table_name(id BIGSERIAL NOT NULL PRIMARY KEY, name VARCHAR(50) NOT NULL,email VARCHAR(50) NOT NULL UNIQUE, date_of_birth DATE);```

## Data Manipulation

### Insert
```INSERT INTO table_name (name, email, date_of_birth VALUES ('John', 'John@gmail.com', '1999-01-01');```

### See Table Contents
```SELECT * FROM table_name;```

### Order By
```select * from employee order by name ASC;```
```select * from employee order by name DESC;```

### Where, AND
```SELECT field_name FROM table_name WHERE name='muneer' AND date_of_birth='2000-10-01';```

### Where + '<,>,='
```company=# SELECT * FROM employee WHERE date_of_birth<'2000-01-09';```

### Distinct
```SELECT DISTINCT field_name FROM table_name;```

### Alter Table
```ALTER TABLE table_name ADD COLUMN gender VARCHAR(10);```
```alter table students drop column_name;```
```ALTER TABLE students ADD CONSTRAINT unique_email UNIQUE (email);```

### Update
```UPDATE table_name SET gender = 'Female'  WHERE name = 'Rose'; ```

## Additional Table Features

### Created At
```CREATE TABLE table_name (id SERIAL PRIMARY KEY,name VARCHAR(100),email VARCHAR(100),gender VARCHAR(10),created_at DATE DEFAULT CURRENT_DATE);```

## Advanced Queries

### Limit
```SELETCT * FROM table_name LIMIT 5;```
```SELECT * FROM table_name OFFSET 5 LIMIT 5;```

### Fetch
```company=# SELECT * FROM employee FETCH FIRST 5 ROWS ONLY;```

### In
```SELECT * FROM employee WHERE place IN('chennai','mumbai');```

### Between
```SELECT * FROM employee WHERE date_of_birth BETWEEN DATE '1999-01-01' AND '2005-01-02';```

### Like
```SELECT * FROM employee WHERE name LIKE 'd%';```
```SELECT * FROM employee WHERE name LIKE '%d';```

### iLike
```company=# SELECT * FROM employee WHERE name iLIKE '%d';```

### Group By
```SELECT place FROM employee GROUP BY place; ```
```SELECT place,COUNT(*) FROM employee GROUP BY place;```

### Having
```SELECT place,COUNT(*) FROM employee GROUP BY place HAVING COUNT(*)>1;```
```SELECT place,COUNT(*) FROM employee GROUP BY place HAVING COUNT(*)=1;```

### Aggregate Functions

#### Max
```SELECT max(salary) FROM employee;```

#### Min
```SELECT min(salary) FROM employee;```

#### Round
```SELECT round(avg(salary)) FROM employee;```

### Alias (AS)
```select id,name,email,salary,(salary/10) as sample from employee;```

### Coalesce
``` select id,name,mark,total,coalesce(email,'not found') from student```

### Conflict
1. DO NOTHING: It doesn't update the record and doesn't show an error.
2. DO UPDATE: It updates the record.

### Upsert Query
Insert if there is no record exists, update if there is a record exists.

## Foreign Key

A foreign key links to the primary of another table.

```CREATE TABLE addresses (id SERIAL PRIMARY KEY,emp_id INTEGER REFERENCES employees(id),city VARCHAR(100),district VARCHAR(100),pin VARCHAR(10));```

## Joins

### Inner Join
```select * from employees inner join addresses on employees.id=addresses.emp_id;```

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
