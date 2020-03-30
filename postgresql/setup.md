# PostgreSQL Setup

## Installation
Contents
- [Mac instructions](#mac-instructions)
- [Linux instructions](#linux-instructions)

### Mac Instructions
Run these commands to install:

> in bash: (normal Terminal window)

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

To leave `psql`, hold *`ctrl` + `d`*. This quits the process and returns you to `bash` (normal Terminal).

**Congratulations! You've got PostgreSQL setup on Mac (hopefully).**


> If you have trouble with the `CLI` instructions, the Postgres Mac GUI app can be used as a last resort :)
> https://postgresapp.com/

### Linux Instructions
Run these commands to install Postgres on **Debian/Ubuntu**

> in `bash` (normal Terminal window)

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

To leave `psql`, hold *`ctrl` + `d`*. This quits the process and returns you to `bash` (normal Terminal).

**Congratulations! You've got PostgreSQL setup on Linux (hopefully).**

**If you're using Arch Linux, try this:**

```sh
# Make sure your system is fully up to date
sudo pacman -Syu
# Install postgresql
sudo pacman -S postgresql
# Change your user to postgres
sudo -u postgres -i
# Initialise the database (if you get a permissions error follow the steps below)
initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data'
# Return to your user
exit
# Start the postgresql service and enable it automatically on startup
sudo systemctl start postgresql.service
sudo systemctl enable postgresql.service
# Create a new database superuser with the same name as your linux user
sudo -u postgres -i
createuser -s --interactive
# As the database user is the same as your linux user, you no longer need to
# change to the postgres user to access the postgresql commands
exit
# Create a database with the same name as your user
createdb $whoami
```


### If you have permission issues with **initdb** (on *Arch*), reset the folder permissions:

```sh
# Make sure you are logged in as yourself and not postgres
exit # If it says postgres@ rather than yourusername@ to the left of the cursor
# Check if the data folder exists in /var/lib/postgres/
sudo ls /var/lib/postgres
# If it does, delete it; otherwise skip this step
sudo rm -R /var/lib/postgres/data
# Allow write access to the folder
sudo chmod 775 /var/lib/postgres
# Set the folders owner to the postgres user
sudo chown postgres /var/lib/postgres
```

Now return to the stage above where you change your user to postgres

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
