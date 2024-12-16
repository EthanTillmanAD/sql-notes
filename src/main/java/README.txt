
relational databases store data with certain relationships with each other

the relational database management system or (RDBMS) is the system we used to manage the
relational data


Types of data integrity

entity integrity - requires each row name to be unique, to get this we can utilize a primary key

Referential integrity - this is referencing to the relationships between multiple tables and utilizing a foreign key

Domain integrity - this ensures all data inserted is accepted, and within the set requirements

User-defined integrity - this helps allow for business rules when the other integrity types can't cover it


within sql we have commands on creating altering deleting and more

sql is not case-sensitive!!!!
--------------------------------------------------------------------------------------

create - creates a database / table
ex:

//for databases
mysql> create database `database name`;

//for tables
mysql> CREATE TABLE promotions(
    -> id int,
    -> name varchar(50),
    -> category varchar(15)
    -> );
--------------------------------------------------------------------------------------


drop - deletes a database or table
ex:

mysql> drop database `database name`;

we can also pair drop with IF EXISTS where we will only drop the table if
the table name is within that database
--------------------------------------------------------------------------------------


describe - shows columns inside tables
ex:

mysql> describe promotions;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | NO   | PRI | NULL    |       |
| name     | varchar(50) | YES  |     | NULL    |       |
| category | varchar(15) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
--------------------------------------------------------------------------------------


insert - inserts data into the table
ex:

mysql> insert into promotions (id, category) VALUES(1, 'Merchandise');
--------------------------------------------------------------------------------------

select - gets information from table
ex:

mysql> select * from promotions;


+------+------+-------------+
| id   | name | category    |
+------+------+-------------+
|    1 | NULL | Merchandise |
+------+------+-------------+
when using select we can also use the LIMIT keyword to set how many items we want

ex:

mysql>  select * from movies LIMIT 5;
--------------------------------------------------------------------------------------

alter - modifies structure of database or table
ex:

mysql> alter table promotions ADD PRIMARY KEY(id);

--------------------------------------------------------------------------------------

truncate - removes all table records
ex:



--------------------------------------------------------------------------------------



rename - renames database or table
ex:



--------------------------------------------------------------------------------------

show - shows databases or tables
ex:
mysql> show database `database name`;


--------------------------------------------------------------------------------------



primary key restraint, makes values required
we can either set the table to have a primary key when we create it or alter it and add
it in

ex:
mysql> alter table promotions ADD PRIMARY KEY(id);


OR

mysql> create table inventory(
    -> productID INT UNSIGNED NOT NULL AUTO_INCREMENT,
    -> productCode CHAR(3) NOT NULL DEFAULT '',
    -> name VARCHAR(30) NOT NULL DEFAULT '',
    -> quantity INT UNSIGNED NOT NULL DEFAULT 0,
    -> price DECIMAL(7,2)NOT NULL DEFAULT 99999.99,
    -> PRIMARY KEY (productID)
    -> );


the foreign key is used as a bridge between tables within a database and ensure the data entered is valid

ex:
mysql> create table test(
    -> fakeId INT PRIMARY KEY,
    -> ProductID INT,
    -> FOREIGN KEY (ProductID) REFERENCES inventory (ProductID);



--------------------------------------------------------------------------------------


to delete a stored item inside our table we can use a statement to delete it

ex:
mysql> select * from inventory
    -> where productID=1006;
+-----------+-------------+------------+----------+-------+
| productID | productCode | name       | quantity | price |
+-----------+-------------+------------+----------+-------+
|      1006 | CON         | Controller |      200 | 59.99 |
+-----------+-------------+------------+----------+-------+
1 row in set (0.00 sec)

mysql> delete from inventory where productID=1006
    -> ;
Query OK, 1 row affected (0.01 sec)

mysql> select * from inventory
    -> ;
+-----------+-------------+-----------+----------+-------+
| productID | productCode | name      | quantity | price |
+-----------+-------------+-----------+----------+-------+
|      1001 | PEN         | Pen Red   |     5000 |  1.23 |
|      1002 | PEN         | Pen Blue  |     8000 |  1.25 |
|      1003 | PEN         | Pen Black |     2000 |  1.25 |
|      1004 | PEC         | Pencil 2B |    10000 |  0.48 |
|      1005 | PEC         | Pencil 2H |     8000 |  0.49 |
+-----------+-------------+-----------+----------+-------+
--------------------------------------------------------------------------------------
we can add a column
mysql> alter table inventory ADD Ratings Int;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc inventory;
+-------------+--------------+------+-----+----------+----------------+
| Field       | Type         | Null | Key | Default  | Extra          |
+-------------+--------------+------+-----+----------+----------------+
| productID   | int unsigned | NO   | PRI | NULL     | auto_increment |
| productCode | char(3)      | NO   |     |          |                |
| name        | varchar(30)  | NO   |     |          |                |
| quantity    | int unsigned | NO   |     | 0        |                |
| price       | decimal(7,2) | NO   |     | 99999.99 |                |
| Ratings     | int          | YES  |     | NULL     |                |
+-------------+--------------+------+-----+----------+----------------+
6 rows in set (0.00 sec)

mysql> select * from inventory
    -> ;
+-----------+-------------+-----------+----------+-------+---------+
| productID | productCode | name      | quantity | price | Ratings |
+-----------+-------------+-----------+----------+-------+---------+
|      1001 | PEN         | Pen Red   |     5000 |  1.23 |    NULL |
|      1002 | PEN         | Pen Blue  |     8000 |  1.25 |    NULL |
|      1003 | PEN         | Pen Black |     2000 |  1.25 |    NULL |
|      1004 | PEC         | Pencil 2B |    10000 |  0.48 |    NULL |
|      1005 | PEC         | Pencil 2H |     8000 |  0.49 |    NULL |
+-----------+-------------+-----------+----------+-------+---------+
mysql> UPDATE inventory
    -> SET Ratings=8
    -> WHERE name='Pen Red';
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from inventory
    -> ;
+-----------+-------------+-----------+----------+-------+---------+
| productID | productCode | name      | quantity | price | Ratings |
+-----------+-------------+-----------+----------+-------+---------+
|      1001 | PEN         | Pen Red   |     5000 |  1.23 |       8 |
|      1002 | PEN         | Pen Blue  |     8000 |  1.25 |    NULL |
|      1003 | PEN         | Pen Black |     2000 |  1.25 |    NULL |
|      1004 | PEC         | Pencil 2B |    10000 |  0.48 |    NULL |
|      1005 | PEC         | Pencil 2H |     8000 |  0.49 |    NULL |
+-----------+-------------+-----------+----------+-------+---------+


mysql> update inventory SET Ratings=5, quantity=8001 where productID=1002;
Query OK, 1 row affected (0.02 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from inventory;
+-----------+-------------+-----------+----------+-------+---------+
| productID | productCode | name      | quantity | price | Ratings |
+-----------+-------------+-----------+----------+-------+---------+
|      1001 | PEN         | Pen Red   |     5000 |  1.23 |       8 |
|      1002 | PEN         | Pen Blue  |     8001 |  1.25 |       5 |
|      1003 | PEN         | Pen Black |     2000 |  1.25 |    NULL |
|      1004 | PEC         | Pencil 2B |    10000 |  0.48 |    NULL |
|      1005 | PEC         | Pencil 2H |     8000 |  0.49 |    NULL |
+-----------+-------------+-----------+----------+-------+---------+

Where is a search method to search through data
ex:

mysql> select * from inventory
    -> WHERE price<1;
+-----------+-------------+-----------+----------+-------+---------+
| productID | productCode | name      | quantity | price | Ratings |
+-----------+-------------+-----------+----------+-------+---------+
|      1004 | PEC         | Pencil 2B |    10000 |  0.48 |    NULL |
|      1005 | PEC         | Pencil 2H |     8000 |  0.49 |    NULL |
+-----------+-------------+-----------+----------+-------+---------+



mysql> select name, quantity from inventory WHERE name='Pen Black';
+-----------+----------+
| name      | quantity |
+-----------+----------+
| Pen Black |     2000 |
+-----------+----------+

we can use order by to change sort by something

mysql> select * from inventory WHERE name LIKE 'Pen %' ORDER BY price DESC;
+-----------+-------------+-----------+----------+-------+---------+
| productID | productCode | name      | quantity | price | Ratings |
+-----------+-------------+-----------+----------+-------+---------+
|      1002 | PEN         | Pen Blue  |     8001 |  1.25 |       5 |
|      1003 | PEN         | Pen Black |     2000 |  1.25 |    NULL |
|      1001 | PEN         | Pen Red   |     5000 |  1.23 |       8 |
+-----------+-------------+-----------+----------+-------+---------+
this we are order by descending order, ascending is default
can also use RAND() to do it by randomly


mysql> select MAX(price) from inventory;
+------------+
| MAX(price) |
+------------+
|       1.25 |
+------------+
mysql> select AVG(price) from inventory;
+------------+
| AVG(price) |
+------------+
|   0.940000 |
+------------+



mysql> select productCode, count(*)
    -> from inventory
    -> GROUP BY productCode;
+-------------+----------+
| productCode | count(*) |
+-------------+----------+
| PEN         |        3 |
| PEC         |        2 |
+-------------+----------+


UNSIGNED makes it to where you can only have positive numbers
decimal(5,2) = 123.45




mysql> select productCode AS `Product Code`,
    -> COUNT(*) AS `Count`,
    -> CAST(AVG(price) AS DECIMAL(7,2)) AS `Average`,
    -> from inventory
    -> GROUP BY productCode
    -> HAVING Count >=3;



    foreign key


    mysql> insert into promo(id, inventory_productID, name, category) VALUES( 1, 1001, 'points', 'cashback');
    Query OK, 1 row affected (0.01 sec)

    mysql> select name, category from promo where inventory_productID = 1001;
    +--------+----------+
    | name   | category |
    +--------+----------+
    | points | cashback |
    +--------+----------+


we can also join tables together
depending on where we want to join them we have special keywords such as JOIN INNER RIGHT INNER LEFT
 ex:

mysql> SELECT `column name` from `table name` INNER LEFT `other table name` ON `first table column name` = `second column name`
    -> WHERE condition;

In sql we have datatype such as int, char, decimal and more



