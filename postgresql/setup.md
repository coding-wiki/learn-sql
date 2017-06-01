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

# create your database where mydb is your desired database name
$ createdb mydb
```

Then to login to the database, use `psql mydb`.

To setup autocomplete for PostgreSQL, you can install pgcli with brew:
```bash
brew install pgcli
```
and login to the database with `pgcli mydb`.


## Installing PostgreSQL on Linux (Debian-based)
Run these commands to install Postgre
```bash
# Update package list
sudo apt-get update

# Install postgresql and postgresql-contrib (additional modules such as UUID)
sudo apt-get install postgresql postgresql-contrib

# Set a shell variable to currently logged in user
MY_USERNAME=$(whoami)

# Create a new postgres user for the currently logged in user
sudo -u postgres createuser $MY_USERNAME

# Create a new postgres user for the currently logged in user
sudo -u postgres createdb $MY_USERNAME
```

Run `psql` to access the Postgre CLI, then proceed to run these SQL commands:
```sql
CREATE DATABASE test;

CREATE USER testuser;

GRANT ALL PRIVILEGES ON DATABASE test TO testuser;
```


## Resources:
- [Autocomplete postgresql client](https://github.com/dbcli/pgcli)
- [Installing PostgreSQL on Linux](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-16-04)
- [Windows :O](https://www.bigsql.org/package-manager.jsp/)
- [dwyl/learn-postgresql](https://github.com/dwyl/learn-postgresql)
