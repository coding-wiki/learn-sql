# PostgreSQL Setup

## Installing PostgreSQL on Mac
Run these commands to install:
```bash
# install postgresql
$ brew install postgresql

# initialise database
$ initdb /usr/local/var/postgres

# start the postgres server
$ brew services start postgresql

# create your database
$ createdb mydb
```
