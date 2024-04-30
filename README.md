# PostgreSQL Cheat Sheet

Enter to posgress:

```psql -U postgres``` 

List dbs:
```\l```

Creating new db:
``` CREATE DATABASE db_name;```

Drop a db:
 ```DROP DATABASE db_name;```

Connect to a db:
 ```\c db_name```

Connect again to postgress / exit from current db:
``` \c postgres```

-----------------------------------------------------

To see all the tables in the current db:
 ```\d```

To see datails of the table:
```\d table_name```

Create table without constrains:
```CREATE TABLE table_name(id INT, name VARCHAR(50), email VARCHAR(50), date_of_birth DATE);```


Delete a table:
```DROP TABLE table_name;```

Delete a record:
```DELETE FROM employee WHERE name='muneer';```

Create table with constraints:
```CREATE TABLE table_name(id BIGSERIAL NOT NULL PRIMARY KEY, name VARCHAR(50) NOT NULL,email VARCHAR(50) NOT NULL UNIQUE, date_of_birth DATE);```

INSERT:
```INSERT INTO table_name (name, email, date_of_birth VALUES ('John', 'John@gmail.com', '1999-01-01');```

To see the table contents:
```SELECT * FROM table_name;```
or
```SELECT field_name FROM table_name;```

ORDER BY:
 ```select * from employee order by name ASC;```
 ```select * from employee order by name DESC;```

WHERE, AND:
```SELECT field_name FROM table_name WHERE name='muneer' AND date_of_birth='2000-10-01';```

WHERE + '<,>,='
```company=# SELECT * FROM employee WHERE date_of_birth<'2000-01-09';```

DISTINCT:
```SELECT DISTINCT field_name FROM table_name; (avoid repeat values)```

ALTER:
```ALTER TABLE table_name ADD COLUMN gender VARCHAR(10); (add column to the table)```

```alter table students drop column_name;``` ( delete a column )

```ALTER TABLE students ADD CONSTRAINT unique_email UNIQUE (email);```

UPDATE:
```UPDATE table_name SET gender = 'Female'  WHERE name = 'Rose'; ```  (update the value of the gender of the row of Rose)
 
CREATED AT:
```CREATE TABLE table_name (id SERIAL PRIMARY KEY,name VARCHAR(100),email VARCHAR(100),gender VARCHAR(10),created_at DATE DEFAULT CURRENT_DATE);```


Limit:
```SELETCT * FROM table_name LIMIT 5;```
slect from a index
```SELECT * FROM table_name OFFSET 5 LIMIT 5;```

FETCH:
```company=# SELECT * FROM employee FETCH FIRST 5 ROWS ONLY;```

IN:
```SELECT * FROM employee WHERE place IN('chennai','mumbai');```
BETWEEN:
```SELECT * FROM employee WHERE date_of_birth BETWEEN DATE '1999-01-01' AND '2005-01-02';```

LIKE:
 ```SELECT * FROM employee WHERE name LIKE 'd%';``` (show the rows with name starting d)
 ```SELECT * FROM employee WHERE name LIKE '%d';``` (show the rows with name ending d)
iLIKE:
 ```company=# SELECT * FROM employee WHERE name iLIKE '%d';``` (case in-sensitive)

GROUP BY:
 ```SELECT place FROM employee GROUP BY place; ```
``` SELECT place,COUNT(*) FROM employee GROUP BY place;```

HAVING:
```SELECT place,COUNT(*) FROM employee GROUP BY place HAVING COUNT(*)>1;```
```SELECT place,COUNT(*) FROM employee GROUP BY place HAVING COUNT(*)=1;```

AGGREGATE FUNCTIONS:

max:
```SELECT max(salary) FROM employee;```

min:
```SELECT min(salary) FROM employee;```

round:
```SELECT round(avg(salary)) FROM employee;```

Alias(AS):
```select id,name,email,salary,(salary/10) as sample from employee;```

COALESCE
``` select id,name,mark,total,coalesce(email,'not found') from student```
(it show not found for empty emails)

CONFLICT:
1. DO NOTHING
   It dont update the record and not show the errro
2. DO UPDATE
   It update the record 

UPSERT QUERY:
insert if there is no record exists
update if there is a record exists.

FOREIGN KEY:
A foreign key links to the primary of a another table.

```CREATE TABLE addresses (id SERIAL PRIMARY KEY,emp_id INTEGER REFERENCES employees(id),city VARCHAR(100),district VARCHAR(100),pin VARCHAR(10));```

INNER JOIN:
```select * from employees inner join addresses on employees.id=addresses.emp_id;```
  (address is another table which contains emp_id as a foreign key refering the employees       tables's primary key id)

LEFT JOIN:
 show all data of left table and matching data of right

RIGHT JOIN:
 show all data of right table and matching data of left

FULL OUTER JOIN:
 show the complete data of both tables

CASE:
 select name,mark, 
 case 
 when mark>=180 then 'A+' 
 when mark between 150 and 180 then 'A' 
 when mark between 100 and 150 then 'B+' 
 end from students;

SUBQUERY:
```select * from employee wheren id= (select id from employee where name='muneer');```

```TRANSTACTION
 BEGIN;
 UPDATE employees
 SET salary = salary + 500;
 COMMIT;
