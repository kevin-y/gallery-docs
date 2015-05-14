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
	<b>Note:</b> SHOW CREATE TABLE table_name can also show table structures in a SQL-style way.
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

