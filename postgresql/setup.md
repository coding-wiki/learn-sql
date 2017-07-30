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

# Superuser/root roles shouldn't exist in production, since permissions should be granted per-database
# See below code block for alternative
sudo -u psql -c "ALTER USER $PSQL_MY_USERNAME WITH SUPERUSER"
```

An alternative to making your user a superuser, is to always use `sudo -u postgres <command like psql or createdb here>`

To use `psql`, you need to use `psql` from a user account with the necessary priveleges or `sudo -u postgres psql`.

To setup a database with privileges for a new user (if you want to use per-user privileges):
```sql
CREATE DATABASE <database name here>;

CREATE USER <desired username to connect to database>;

GRANT ALL PRIVILEGES ON DATABASE <database name here> TO <desired username entered previously>;
```

Alternative to avoid using `sudo -u postgres`:
```bash
#ignore /etc/postgresql/$(ls /usr/local/Cellar/postgresql)

#bash automation
echo 'local   all             all                                     trust' >> $(psql -t -d postgres -c $'SHOW hba_file;')
```

### If you have issues with outdated versions, use these steps:
1. If postgres is installed already, uninstall it with `sudo apt-get remove postgres postgres-contrib`
2. Depending on your system, run the appropriate command:

  - **FOR Ubuntu 17.04 ONLY:**
    ```sh
    deb http://apt.postgresql.org/pub/repos/apt/ zesty-pgdg main
    ```
  
  - **FOR Ubuntu 16.04 ONLY:**
    ```sh
    deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main
    ```
  
  - **FOR Ubuntu 14.04 ONLY:**
    ```sh
    deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main
    ```
  
3. **Then run:**
  ```sh
  wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | \
  sudo apt-key add -
  sudo apt-get update
  ```


## Resources:
- [Autocomplete postgresql client](https://github.com/dbcli/pgcli)
- [Installing PostgreSQL on Linux](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-16-04)
- [Windows :O](https://www.bigsql.org/package-manager.jsp/)
- [dwyl/learn-postgresql](https://github.com/dwyl/learn-postgresql)
