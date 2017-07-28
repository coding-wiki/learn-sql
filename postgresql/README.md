# Learn PostgreSQL
PostgreSQL is an object-relational database management system (ORDBMS) that supports a large part of the SQL standard and offers many modern features

## Getting Started

[Setup](./setup.md)

## Accessing your SQL database
You need to login to your database with a command line or graphical interface to run SQL commands.

We will be using `psql` which is a command line interface that comes with PostgreSQL. It has a number of CLI specific commands which are accessed with `\<letter>` such as `\l`

[PSQL Cheatsheet](./psql-cheatsheet.md)

### Command syntax - `Terminal`
```sh
psql <optional-database-name>
# use "sudo -u postgres psql" on Linux if above doesn't work
```
> hold `CTRL + D` to leave

### Example to login to database with your system username:
```sh
psql
```


## Creating a database
A database with your system username was created in the setup instructions. Each database contains a set of tables, which optionally relate to each other. Each app should have its own database.

To create a database, use these commands in a database interface:
```sql
CREATE DATABASE test; -- where test is <new-database-name>
```

Setting up a user with privileges for existing database: 
```sql
CREATE USER myuser; -- where myuser is <new-database-username>
GRANT ALL PRIVILEGES ON DATABASE test TO myuser; -- where test is <database-name> and myuser is <database-username>
```

## Access a database

### Command syntax - `Terminal`
```sh
psql <database-name>
```

### Command syntax - `SQL client` such as `psql`
```sql
\c <database-name>
```

## SQL Commands
An SQL command has to start with a command such as `SELECT` or `INSERT INTO` and end with a semi-colon: `;`

## Getting Data
Command syntax of `SELECT`:
```sql
SELECT <row_1>, <row_2> FROM <table_name>
-- Where row_1 is required, row_2, etc are optional and comma separated
-- row_1 is the name of the SQL row, or you can use * to select all rows
-- table_name is the name of the SQL table

```

Optional parameters appended to previous syntax statement:
```sql
WHERE      -- specifies which rows to retrieve.
GROUP      -- BY groups rows sharing a property so that an aggregate function can be applied to each group.
HAVING     -- selects among the groups defined by the GROUP BY clause.
ORDER BY   -- specifies an order in which to return the rows.
AS         -- provides an alias which can be used to temporarily rename tables or columns.
```

### If/switch statements in SQL

You can use a switch syntax in SQL.

Syntax inside a `SELECT ... FROM <table>`:
```sql
CASE WHEN (<condition>) THEN
  <value>
ELSE
  <value>
END AS <column_name>
```

Example
```sql
SELECT name,

	CASE WHEN (percentage > 50) THEN
		'large'
	ELSE
		'small'
	END AS size

	FROM table_name;
```
