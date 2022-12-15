+++
title = "Goose in go"
date = "2022-09-20"
author = "Inu John"
cover = "img/goose.jpg"
tags = ["golang", "database", "migration", "go"]
description = "Using goose in golang for database migration. 🦆"
+++

## What is Goose?

Goose is a tool in golang used for database migrations.

## Installation

Goose can either be installed as a CLI tool, or it can be used as a package. You can find it [here](https://pressly.github.io/goose/installation/)

## How do I migrate?

In your root folder, create a new folder named `migrations.` This new folder you just created is where your migrations will be stored.

Next, cd into the `migrations` folder and run this command to create a new table `goose create {table name} sql` this will generate a file that looks like something similar to this `20023473848499499_{table name}.sql`

If we opened the file we just created, we'll see some code snippet, make sure you don't delete them, it'll help in the migration process.

```sql
-- +goose Up
-- +goose StatementBegin
-- +goose StatementEnd

-- +goose Down
-- +goose StatementBegin
-- +goose StatementEnd
```

This is what an empty migration file looks like. Now, let's break it down.

```sql
-- +goose Up
-- +goose StatementBegin

-- +goose StatementEnd
```

The `goose up` is used to migrate your tables {files} to your database. A `goose up` migrate is something like this;

```sql
-- +goose Up
-- +goose StatementBegin
  CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR(255) NOT NULL,
  last_name VARCHAR(255) NOT NULL,
);
-- +goose StatementEnd
```

The `goose down` is used to drop your {files} in your database. A `goose down` migrate is something like this;

```sql
-- +goose Down
-- +goose StatementBegin
  DROP TABLE users;
-- +goose StatementEnd
```

```sql
-- +goose Up
-- +goose StatementBegin
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR(255) NOT NULL,
  last_name VARCHAR(255) NOT NULL,
  email VARCHAR(255) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL,
  access_level INTEGER DEFAULT 1 NOT NULL,
  created_at timestamp NOT NULL,
  updated_at timestamp NOT NULL,
  deleted_at timestamp
);
-- +goose StatementEnd

-- +goose Down
-- +goose StatementBegin
  DROP TABLE users;
-- +goose StatementEnd
```

To run the `goose up` command on your terminal, this is the command you should use.

    goose postgres "user={user name} dbname={db name} sslmode=disable password={password}" up

To run the `goose down` command on your terminal, this is the command you should use.

    goose postgres "user={user name} dbname={db name} sslmode=disable password={password}" down

You can also check the status using:

    goose postgres "user={user name} dbname={db name} sslmode=disable password={password}" status
