# PSQL Cheatsheet
A list of useful `psql` CLI commands.

## Getting Started
Refer to [PostgreSQL installation and usage instructions to find out how to use psql](./)

## Help Utility
In Terminal:
```sh
psql
```

In `psql`:
```
\?
```

## Top Commands:
```
\q                  -- quit psql
\d                  -- list databases
\d                  -- list of tables
\c [DATABASE-NAME]  -- Connect to a database
```

## Useful Commands

General
```
  \q                      -- quit psql
  \g [FILE] or ;          -- execute query (and send results to file or |pipe)
  \gexec                  -- execute query, then execute each value in its result
  \gset [PREFIX]          -- execute query and store results in psql variables
  \crosstabview [COLUMNS] -- execute query and display results in crosstab
  \watch [SEC]            -- execute query every SEC seconds
```

Help
```
  \? [commands]          -- show help on backslash commands
  \h [NAME]              -- help on syntax of SQL commands, * for all commands
```

Input/Output
```
  \copy ...              -- perform SQL COPY with data stream to the client host
  \echo [STRING]         -- write string to standard output
  \i FILE                -- execute commands from file
  \ir FILE               -- as \i, but relative to location of current script
  \o [FILE]              -- send all query results to file or |pipe
  \qecho [STRING]        -- write string to query output stream (see \o)
```

Informational
```
  (options: S = show system objects, + = additional detail)
  \d                     -- list tables, views, and sequences
  \d  NAME               -- describe table, view, sequence, or index
  \dd[S]  [PATTERN]      -- show object descriptions not displayed elsewhere
  \ddp    [PATTERN]      -- list default privileges
  \dD     [PATTERN]      -- list domains
  \det    [PATTERN]      -- list foreign tables
  \du                    -- list users
  \du     [USERNAME]     -- list specific username
```
  