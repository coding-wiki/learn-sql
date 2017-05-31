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


## Resources:
- [Autocomplete postgresql client](https://github.com/dbcli/pgcli)
- [Installing PostgreSQL on Linux](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-16-04)
- [Windows :O](https://www.bigsql.org/package-manager.jsp/)
