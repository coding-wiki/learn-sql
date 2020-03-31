# Installing PostgreSQL on Windows (WSL)

## Prerequisites

- **OS version:** Windows 10 Insider Preview build 18932 or later
- Enable [WSL 2 feature](https://docs.microsoft.com/en-us/windows/wsl/wsl2-install)
- Linux distro installed (e.g. Debian)
  - You can check it with `wsl -l -v`

## Getting Started

### Installing PostgreSQL

1. Open your WSL terminal
2. Update your Ubuntu sources:

```sh
sudo apt update
```

3. install PostgreSQL (and the -contrib package which has some helpful utilities) with:

```sh
sudo apt install postgresql postgresql-contrib
```

To manage or check the database service, use: `sudo service postgresql #(status|start|stop)#`

Examples:

```sh
sudo service postgresql status # for checking the status of your database
sudo service postgresql start # to start running your database
sudo service postgresql stop # to stop running your database
```

### Setting Up `postgres` User

The default admin user, `postgres`, requires a password before you can connect to a database.

To set a password, use:

```sh
sudo passwd postgres
```

(you will get prompted to enter the password, type the characters, which won't appear on screen, and press `enter` once finished)

### Running `psql` Shell

`psql` is a terminal-based front-end for PostgreSQL. It lets you type in queries interactively, sending them to PostgreSQL, and returning the query results to you. Alternatively, input can be from a file.

```sh
# Start your postgres service with:
sudo service postgresql start

# Open the psql shell for the active postgresql service:
sudo -u postgres psql
```

To exit `postgres=#` enter: `\q` or use the shortcut key: `Ctrl` + `D`

## Creating Your First Database

```bash
# Set a shell variable to currently logged in user
PSQL_MY_USERNAME=$(whoami)

# Create a new postgres user for the currently logged in user
sudo -u postgres createuser $PSQL_MY_USERNAME --superuser

# Create a new postgres database for the currently logged in user
sudo -u postgres createdb $PSQL_MY_USERNAME

# Assign SUPERUSER privileges to the database for your new user:

sudo -u postgres psql $PSQL_MY_USERNAME -c "ALTER USER $PSQL_MY_USERNAME WITH SUPERUSER"
```

### Creating a New Database For an App

You shouldn't use a root user outside of the Terminal, and this user should be blocked off from the internet.

Let's create a separate user for each app, like this:

```bash
MY_APP_NAME=hello_world

sudo -u postgres createuser $MY_APP_NAME
sudo -u postgres createdb $MY_APP_NAME

sudo -u postgres psql $MY_APP_NAME -c "ALTER USER $MY_APP_NAME WITH SUPERUSER;"
```

And let's check that our new user doesn't have privileges to create or delete other databases:

```bash
# Enter psql shell
psql $MY_APP_NAME
```

Inside our `psql` shell, run: `\du` to check the users. You should see something like this:

![image](https://user-images.githubusercontent.com/6757532/78057539-ca941f80-737e-11ea-8488-68cf8d85636c.png)


## Troubleshooting

If you get the error `PANIC: could not flush dirty data: Function not implemented`, you can try this:

```sh
sudo nano /etc/postgresql/10/main/postgresql.conf
```

and append this line to the end of the file:

```
data_sync_retry = true.
```

(`Ctrl` + `O` and press `Y` to save, and `Ctrl` + `D` to exit `nano`)

## Resources

If you need help debugging problems, try: https://medium.com/@karansingh1559/how-to-set-up-postgresql-on-ubuntu-for-wsl-fcbb777d165b

- [Get started using MongoDB or PostgreSQL with Node.js on Windows](https://docs.microsoft.com/en-us/windows/nodejs/databases#prerequisites)
  - [LICENSE of the Microsoft docs – Creative Commons Attribution](https://github.com/MicrosoftDocs/windows-uwp/blob/docs/LICENSE)
