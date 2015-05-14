# MySQL Tutorial

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