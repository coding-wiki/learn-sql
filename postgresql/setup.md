# PostgreSQL Setup

## Installation
Contents
- [Mac instructions](#mac-instructions)
- [Linux instructions](#linux-instructions)

### Mac Instructions
Run these commands to install:
```bash
  # install postgresql
  brew install postgresql

  # uncomment and run below if you experience problems:
  #initdb /usr/local/var/postgres

  # start the postgres server
  brew services start postgresql
  
  # Set logged in username to environment variable
  PSQL_MY_USERNAME=$(whoami)

  # create database with your username (from environment variable)
  createdb $PSQL_MY_USERNAME
```

Then to test that you can login to the database, use `psql`.
Running `psql` is equivalent to `psql <your computer username>`

**Congratulations! You've got PostgreSQL setup on Mac (hopefully).**




### Linux Instructions
Run these commands to install Postgres on **Debian/Ubuntu**
```bash
# Update package list
sudo apt-get update

# Install postgresql and postgresql-contrib (additional modules such as UUID)
sudo apt-get -y install postgresql postgresql-contrib

# Set a shell variable to currently logged in user
PSQL_MY_USERNAME=$(whoami)

# Create a new postgres user for the currently logged in user
sudo -u postgres createuser $PSQL_MY_USERNAME --superuser

# Create a new postgres database for the currently logged in user
sudo -u postgres createdb $PSQL_MY_USERNAME

# 
# 
# sudo -u postgres psql -c "ALTER USER $PSQL_MY_USERNAME WITH SUPERUSER"
```

Then to test that you can login to the database, use `psql`.
Running `psql` is equivalent to `psql <your computer username>`

**Congratulations! You've got PostgreSQL setup on Linux (hopefully).**

**If you're using Arch Linux, try this:**

```sh
# Install postgresql and postgresql-contrib (additional modules such as UUID)
sudo pacman -S postgresql postgresql-contrib
# Set a shell variable to currently logged in user
PSQL_MY_USERNAME=$(whoami)
# Initialise database:
sudo -u postgres initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data'
# Create a new postgres (super)user for the currently logged in user
sudo -u postgres createuser $PSQL_MY_USERNAME --superuser
# Create a new postgres database for the currently logged in user
sudo -u postgres createdb $PSQL_MY_USERNAME
# Logout as _postgres_ user:
[postgres]$ exit
```


### If you have issues with outdated versions (on *Debian*), use these steps:
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




## Creating databases
To create a database, run:
```sh
createdb <database name>
```

And to connect to it, run:
```sh
psql <database name>
```

## User Permissions

Security note: Superuser/root roles shouldn't exist in **production**, since permissions should be granted per-database.

An alternative to making your user a superuser, is to always use `sudo -u postgres <command like psql or createdb here>`


If you'd like to use per-user privileges for a database:

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

## Bonus - Installing an autocomplete client
*Pgcli* is an alternative command line interface (client) for Postgres with auto-completion and syntax highlighting.

### Autocomplete on Mac
You can install `pgcli` with brew:
```bash
brew install pgcli
```
and login to databases with `pgcli` instead of `psql`.

### Autocomplete on Linux
You can install `pgcli` with the Python package manager, `pip`:
```bash
# Either this: Debian install
sudo apt-get install python-pip 
sudo apt-get install libpq-dev python-dev

# Or this:Redhat systems
sudo yum install python-pip
sudo yum install postgresql-devel python-devel

# Then run this:
sudo pip install pgcli
```
and login to databases with `pgcli` instead of `psql`.


## Resources:
- [Autocomplete postgresql client](https://github.com/dbcli/pgcli)
- [Installing PostgreSQL on Linux](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-16-04)
- [Windows :O](https://www.bigsql.org/package-manager.jsp/)
- [dwyl/learn-postgresql](https://github.com/dwyl/learn-postgresql)
