# MySQL Tutorial

## Introduction

This is a tutorial form MySQL, but I won't cover all of the features or details in this tutorial. Instead, I will only focus on what comes out of my thoughts and I will update this occasionally. For more information please check [MySQL Official Website](http://dev.mysql.com/ "MySQL Official Website").

## Creating users
1. Creating a user named `kevin` with password `123456`

```
CREATE USER 'kevin'@'localhost' IDENTIFIED BY '123456';
```
<blockquote>
<b>Note:</b> 'kevin'@'localhost' means if you can only login at localhost with the account `kevin`
</blockquote>

2. Grant all privileges to `kevin@localhost` on database sakila

```
GRANT ALL ON sakila.* TO 'kevin'@'localhost';
```

3. Update privileges, it basically tells MySQL to load privileges into memory

```
FLUSH PRIVILEGES;
```

4. Now, you may log into MySQL with `kevin`

```
mysql -u kevin -p123456
```
<pre>
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| sakila             |
+--------------------+
</pre>

## Creating tables

The following commands are used to create a table name `demo.customer` which has the same structure as `sakila.customer`.

<blockquote>
 	<b>Note:</b> sakila is a demo database which comes along with MySQL.
</blockquote>

```
CREATE DATABASE demo;
USE demo;
CREATE TABLE customer LIKE sakila.customer;
```

Then, we can use `DESC` or `demo.customer` to display the table structure:

```
DESC customer;
```

<blockquote>
	<b>Note:</b> <i>SHOW CREATE TABLE table_name</i> can also show table structures in a SQL-style way.
</blockquote>

<pre>
+-------------+----------------------+------+-----+-------------------+-----------------------------+
| Field       | Type                 | Null | Key | Default           | Extra                       |
+-------------+----------------------+------+-----+-------------------+-----------------------------+
| customer_id | smallint(5) unsigned | NO   | PRI | NULL              | auto_increment              |
| store_id    | tinyint(3) unsigned  | NO   | MUL | NULL              |                             |
| first_name  | varchar(45)          | NO   |     | NULL              |                             |
| last_name   | varchar(45)          | NO   | MUL | NULL              |                             |
| email       | varchar(50)          | YES  |     | NULL              |                             |
| address_id  | smallint(5) unsigned | NO   | MUL | NULL              |                             |
| active      | tinyint(1)           | NO   |     | 1                 |                             |
| create_date | datetime             | NO   |     | NULL              |                             |
| last_update | timestamp            | NO   |     | CURRENT_TIMESTAMP | on update CURRENT_TIMESTAMP |
+-------------+----------------------+------+-----+-------------------+-----------------------------+
</pre>

The follow command is trying to copy data from sakila.customer into demo.customer:
```
INSERT INTO customer SELECT * FROM sakila.customer; 
```

Here we can fetch the first 2 records from demo.customer:
```
SELECT * FROM customer LIMIT 2;
```

<pre>
+-------------+----------+------------+-----------+-------------------------------------+------------+--------+---------------------+---------------------+
| customer_id | store_id | first_name | last_name | email                               | address_id | active | create_date         | last_update         |
+-------------+----------+------------+-----------+-------------------------------------+------------+--------+---------------------+---------------------+
|           1 |        1 | MARY       | SMITH     | MARY.SMITH@sakilacustomer.org       |          5 |      1 | 2006-02-14 22:04:36 | 2006-02-15 04:57:20 |
|           2 |        1 | PATRICIA   | JOHNSON   | PATRICIA.JOHNSON@sakilacustomer.org |          6 |      1 | 2006-02-14 22:04:36 | 2006-02-15 04:57:20 |
+-------------+----------+------------+-----------+-------------------------------------+------------+--------+---------------------+---------------------+
</pre>

Alternatively, we can simply use `CREATE TABLE table_name SELECT ...` to accomplish the same task above:
```
CREATE TABLE customer SELECT * FROM sakila.customer;
```

The following example shows how to use `IF` in a SELECT statement, first we need to create a table named `person`, and then insert some data.

```
CREATE TABLE  IF NOT EXISTS person(
	id INT PRIMARY KEY AUTO_INCREMENT,
	name VARCHAR(20) NOT NULL,
	gender CHAR(1) DEFAULT 'N',
	age INT UNSIGNED
);

INSERT INTO person(name, gender, age) VALUES('kevin', 'M', 26);
INSERT INTO person(name, gender, age) VALUES('lucy', 'F', 22);
INSERT INTO person(name, gender) VALUES('jhon', 'M');

+----+-------+--------+------+
| id | name  | gender | age  |
+----+-------+--------+------+
|  1 | kevin | M      |   26 |
|  2 | lucy  | F      |   22 |
|  3 | jhon  | M      | NULL |
+----+-------+--------+------+
```

Here we use `IF` to give age a value UNKNOWN if it's null:

```
SELECT id, name, gender, IF(age IS NULL, 'UNKNOWN', age) AS age FROM person;
or 
SELECT id, name, gender, IFNULL(age,'UNKNOWN') AS age FROM person;
alternatively.

+----+-------+--------+---------+
| id | name  | gender | age     |
+----+-------+--------+---------+
|  1 | kevin | M      | 26      |
|  2 | lucy  | F      | 22      |
|  3 | jhon  | M      | UNKNOWN |
+----+-------+--------+---------+
```
