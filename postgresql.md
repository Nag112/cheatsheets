---
title: PostgreSQL
layout: 2017/sheet

category: Databases
updated: 2024-01-15
intro: |
  PostgreSQL is a powerful, open source object-relational database system.
  It provides the `psql` command line tool for interacting with its database.
---

### Create Database

```shell
createdb <databasename>
```

### Query Database

```shell
psql --no-align --tuples-only --command="SELECT * FROM <table>" # Useful for scripting
psql -Atc "SELECT * FROM <table>" # short version of above
```

### Login to Database

```shell
psql # logs in to default database & default user
sudo -u <rolename:postgres> psql # logs in with a particular user
sudo psql -h <HOST> -p <PORT> -U <DB_USER> <DB_NAME> # log into postgres specifying host, port, user and db
```

#### Commands

* Show roles: `\du`
* Show tables: `\dt`
* Show databases: `\l`
* Show schemas: `\dn`
* Show views: `\dv`
* Show tables: `\dt` or `\dt+`
* Show stored procedure: `\df+ <function_name>`
* Show tables with more information: `\dt+`
* Connect to a database: `\c <database>`
* Show columns of a table: `\d <table>` or `\d+ <table>`
* Quit: `\q`