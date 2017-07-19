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
