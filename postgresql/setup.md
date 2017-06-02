# PostgreSQL Setup

## Installing PostgreSQL on Mac
Run these commands to install:
```bash
(
  # install postgresql
  brew install postgresql

  # initialise database
  initdb /usr/local/var/postgres

  # start the postgres server
  brew services start postgresql

  # Get user input for database name
  echo 'Please input your desired database name, such as mydb'
  read PSQL_DB_NAME
  
  # Get logged in username
  PSQL_MY_USERNAME=$(whoami)

  # create your database where mydb is your desired database name and create database with your username to allow using just 'psql'
  createdb $PSQL_DB_NAME
  createdb $PSQL_MY_USERNAME
);
```

Then to login to the database, use `psql mydb`.

To setup autocomplete for PostgreSQL, you can install pgcli with brew:
```bash
brew install pgcli
```
and login to the database with `pgcli mydb`.


## Installing PostgreSQL on Linux (Debian-based)
Run these commands to install Postgres
```bash
# Update package list
sudo apt-get update

# Install postgresql and postgresql-contrib (additional modules such as UUID)
sudo apt-get -y install postgresql postgresql-contrib

# Set a shell variable to currently logged in user
PSQL_MY_USERNAME=$(whoami)

# Create a new postgres user for the currently logged in user
sudo -u postgres createuser $PSQL_MY_USERNAME

# Create a new postgres user for the currently logged in user
sudo -u postgres createdb $PSQL_MY_USERNAME
```

Run `psql` to access the Postgre CLI, then proceed to run these SQL commands:
```sql
CREATE DATABASE test;

CREATE USER testuser;

GRANT ALL PRIVILEGES ON DATABASE test TO testuser;
```

To avoid using a user account:
```bash
#ignore /etc/postgresql/$(ls /usr/local/Cellar/postgresql)

#bash automation
echo 'local   all             all                                     trust' >> $(psql -t -d postgres -c $'SHOW hba_file;')
```


## Resources:
- [Autocomplete postgresql client](https://github.com/dbcli/pgcli)
- [Installing PostgreSQL on Linux](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-16-04)
- [Windows :O](https://www.bigsql.org/package-manager.jsp/)
- [dwyl/learn-postgresql](https://github.com/dwyl/learn-postgresql)
