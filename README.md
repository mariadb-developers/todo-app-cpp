# TODO - C++ Console Application

The [tasks.cpp](tasks.cpp) file can be used (via C++ compiler) to build an executable that can perform create-read-update-delete (CRUD) operations on a target [MariaDB database](https://github.com/mariadb-developers/mariadb-getting-started) using [MariaDB's C++ connector](https://github.com/mariadb-corporation/mariadb-connector-cpp).

# Table of Contents
1. [Requirements](#requirements)
2. [Getting started with MariaDB](#mariadb)
3. [Get the code](#code)
4. [Create the database and table](#schema)
5. [Build and run the app](#app)
6. [Support and contribution](#support-contribution)
7. [License](#license)

## Requirements <a name="requirements"></a>

This sample was created using the following techologies and they must be installed before proceeding.

* [MariaDB Connector/C++](https://mariadb.com/docs/appdev/connector-cpp/)
* [MariaDB command-line client](https://mariadb.com/products/skysql/docs/clients/mariadb-clients/mariadb-client/) (optional), used to connect to MariaDB database instances.

## 1.) Getting Started with MariaDB <a name="mariadb"></a>

[MariaDB](https://mariadb.com) is a community-developed, commercially supported relational database management system, and the database you'll be using for this application.

If you don't have a MariaDB database up and running you can find more information on how to download, install and start using a MariaDB database in the [MariaDB Quickstart Guide](https://github.com/mariadb-developers/mariadb-getting-started).

## 2.) Get the code <a name="code"></a>

First, use [git](git-scm.org) (through CLI or a client) to retrieve the code using `git clone`:

```
$ git clone https://github.com/mariadb-developers/todo-app-cpp.git
```

## 3.) Create the database and table <a name="schema"></a>

[Connect to your MariaDB database](https://mariadb.com/products/skysql/docs/clients/) (from [Step #2](#mariadb)) and execute the following SQL scripts using the following options:

a.) Use the [MariaDB command-line client](https://mariadb.com/products/skysql/docs/clients/mariadb-clients/mariadb-client/) to execute the SQL contained within [schema.sql](schema.sql).

_Example command:_
```bash
$ mariadb --host HOST_ADDRESS --port PORT_NO --user USER --password PASSWORD < schema.sql
```
schema
**OR**

b.) Copy, paste and execute the raw SQL commands contained in [schema.sql](schema.sql) using a [client of your choice](https://mariadb.com/products/skysql/docs/clients/).

```sql
CREATE DATABASE todo;

CREATE TABLE todo.tasks (
  id INT(11) unsigned NOT NULL AUTO_INCREMENT,
  description VARCHAR(500) NOT NULL,
  completed BOOLEAN NOT NULL DEFAULT 0,
  PRIMARY KEY (id)
);
```

## 4.) Configure the code <a name="configure-code"></a>

[Within the tasks.cpp file](tasks.cpp#L81-L82), navigate to the `main` method and add your database connection values.

Example implementation:

```cpp
sql::SQLString url("jdbc:mariadb://localhost:3306/todo");
sql::Properties properties({{"user", "app_user"}, {"password", "Password123!"}});
```

## 5.) Run the app <a name="app"></a>

Once you've pulled down and configured the code, you're ready to build and run the application! 

1. Build [tasks.cpp](tasks.cpp) to produce an executable called `tasks`.

```bash
$ g++ -o tasks tasks.cpp -std=c++11 -lmariadbcpp
```

2. Perform CRUD operations using the `tasks` executable.

    a. **Insert** a new task record.

    ```
    $ ./tasks addTask 'New Task Description'
    ```

    b. **Update** a task's completion status.

    ```
    $ ./tasks updateTaskStatus 1 1
    ```

    c. **Select** and print all tasks.

    ```
    $ ./tasks showTasks
    ```

    d. **Delete** a task record.

    ```
    $ ./tasks deleteTask 1
    ```

## Support and Contribution <a name="support-contribution"></a>

Please feel free to submit PR's, issues or requests to this project project directly.

If you have any other questions, comments, or looking for more information on MariaDB please check out:

* [MariaDB Developer Hub](https://mariadb.com/developers)
* [MariaDB Community Slack](https://r.mariadb.com/join-community-slack)

Or reach out to us diretly via:

* [developers@mariadb.com](mailto:developers@mariadb.com)
* [MariaDB Twitter](https://twitter.com/mariadb)

## License <a name="license"></a>
[![License](https://img.shields.io/badge/License-MIT-blue.svg?style=plastic)](https://opensource.org/licenses/MIT)
