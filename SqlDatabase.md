# SQL DataBase

## Resources
SQL Designer: http://ondras.zarovi.cz/sql/demo/
Backup a database using Microsoft mysql server management studio: https://www.learnhowtoprogram.com/c/c-database-basics/to-do-list-with-databases-part-2-backing-up-and-restoring-a-database

## Using Command Line
```console
//Access the SQLCMD
sqlcmd -S "(localdb)\mssqllocaldb"

//See current DataBase1
1> SELECT DB_NAME();
2> GO

//Let's list out all of the databases in our SQL server:
1> SELECT name FROM Sys.Databases;
2> GO

// Connect to database
1> USE test_database;
2> GO

//Inspect your table
1> SELECT column_name, data_type FROM information_schema.columns WHERE table_name = 'contacts';
2> GO
```

Shortterm Cheat Sheet
```console
1> CREATE DATABASE todo;
2> GO
1> USE todo;
2> GO
1> CREATE TABLE tasks
2> (
3>   id INT IDENTITY (1,1),
4>   description VARCHAR(255)
5> );
6> GO
```
