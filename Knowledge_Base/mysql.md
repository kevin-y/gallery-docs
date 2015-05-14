# MySQL Tutorial

The following commands are used to create a table name `demo.customer` which has the same structure as `sakila.customer`.

> Note: sakila is a demo database which comes along with MySQL 

<pre><code>
CREATE DATABASE demo;
USE demo;
CREATE TABLE customer LIKE sakila.customer;
</code></pre>

We can use `DESC` or `DISCRIBE` to display the table structure:

<pre><code>
DESC customer;
</code></pre>

> Note: SHOW CREATE TABLE table_name can also show table structures in a SQL-style way.

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

