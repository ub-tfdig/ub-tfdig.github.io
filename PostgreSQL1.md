---
title: "Creating a Database with PostgreSQL"
date: January 31 2023
fontsize: 12pt
---

# Creating a Database with PostgreSQL

## Preparations

- Download the EDB PostgreSQL installer on your laptop from [this site](/https://www.enterprisedb.com/downloads/postgres-postgresql-downloads), by choosing your operating system and the newest version of PostgreSQL, and complete the installation process. During installation, you will be asked to create a PostgreSQL user password. Make sure you remember this password. 
- In the PostgreSQL folder on your PC, find the script file called "SQL Shell (psql)" or "runpsql.bat", and make a shortcut to it on your desktop.

## A Brief Introduction to PostgreSQL
PostgreSQL is a database management system based on the programming language SQL (Structured Query Language). PostgreSQL is "the world's most advanced open source relational database" [see postgresql.org](/http://postgresql.org). 
<br>
"Open source" means that the source code of the software is openly and freely available for anyone to download, modify and improve. The benefits of using Free and Open Source Software (FOSS) are many. Because the software is continuously developed by a community, it continues to improve based on the needs of the users. It is also more flexible, transparent, and, of course, free.
<br>
"Relational" means that PostgreSQL databases allow us to establish and track relationships between data points. This allows us to store complex data in a simple and accessible structure.
<br>
PostgreSQL provides the engine we are going to use to manage the databases. In this case, the database you create will be stored locally on your laptop, which will therefore serve as your database server. You will not need internet access to connect to your database.
<br>
In order to "communicate" with the database system, we will use the SQL shell "psql", a terminal-based, command-line tool that we can use to connect to PostgreSQL. There are several other ways of interacting with and managing PostgreSQL databases, but we will mainly use psql.

## PART I - 19.04.23 Step by step instructions
### *Connect to PostgreSQL via psql*
Open the "SQL Shell (psql)"
<br>
Press ENTER to accept the default server
<br>
Press ENTER to accept the default database
<br>
Press ENTER to accept the default port
<br>
Press ENTER to accept default username
<br>
Enter your password (you will not be able to see on the screen that your password is being entered) and ENTER

You should now have a line on your screen that reads "postgres=#"

### *Create a new database*
Type (after postgres=#):

 CREATE DATABASE name_of_database;

 and press ENTER.

 You have now created a new database. You may use any database name you like, without spaces. If you, for example, want to create a database called Quran_Translations, you type:
 
 CREATE DATABASE Quran_Translations;

 "CREATE DATABASE" is the command, "Quran_Translations" is the name you chose for the database, and the semi-colon is what signalizes that you want to run the command. If you type the command and press enter without the semi-colon, the command will not run, and the database will not be created. 

### *Connect to the new database*
 Exit and re-enter psql. This time, press ENTER once for default server and then, after "DATABASE [postgres]" type the name of your new database, for example "Quran_Translations". Then press ENTER twice and insert your password as before. You should end up with a new line that has the name of your new database followed by =#. For example: Quran_Translations=#.

### *Create a new table in the database*
We can create many different types of tables, depending on the data we have. For this first exercise, we will create a simple table with three columns. The first column will automatically assign an id number to each row of data we insert. This is called an auto-incremental integer column. The other two columns will have variables we choose. For my database of Qur'an translations, I may want a table for Italian translations, with the columns "translator name" and "date of publication". Type:

CREATE TABLE Italian_Translations (
id BIGSERIAL NOT NULL PRIMARY KEY, translator_name VARCHAR(50) NOT NULL, publication_date VARCHAR(50) NOT NULL);

For each column we want to create, thus, we enter what we want to name it, what kind of data it is and any restrictions we want the column to have. VARCHAR(50) means that we want the datatype "variable character" with maximum 50 characters, and "not null" means that each row of data we enter must have a value in this column, it cannot be left empty. 

### *Insert data into the table*
To insert data into the table, type:

INSERT INTO table_name (variable1, variable2) VALUES ('value1', 'value2');

For example:

INSERT INTO Italian_Translations (translator_name, publication_date) VALUES ('Bonelli', '1929');

### *View, change and delete data*
To view the data you have inserted in the table, type:

SELECT * FROM table_name;

For example:

SELECT * FROM Italian_Translations;'

To view the table data in an expanded display, type:
\x
and press ENTER
Then re-enter the SELECT * FROM table_name; command. To duplicate command line, press arrow up on your keyboard.

To see all your tables, type:
\dt
and press ENTER

To change/update data in a table, type:

UPDATE table_name SET variable = 'value' WHERE id = nr;

For example:

UPDATE Italian_Translations SET translator_name 'Luigi Bonelli' WHERE id = 1;

To delete data:

DELETE FROM table_name WHERE id = nr;

For example:

DELETE FROM Italian_Translations WHERE id = 1;



