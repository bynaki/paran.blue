---
title: "Node :: Inserting Data Into an SQLite Table from a Node.js Application"
date: 2021-07-25T00:15:38+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["node", "sqlite3"]
categories: ["Node"]
author: "bynaki"
showToc: true
TocOpen: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://www.sqlitetutorial.net/sqlite-nodejs/insert/"
disableHLJS: false # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: false
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/bynaki/paran.blue/blob/main/content"
    Text: "Edit" # edit text
    appendFilePath: true # to append file path to Edit link
---



**Summary**: in this tutorial, you will learn how to insert one or more row into an SQLite table from a Node.js application.

To insert data into an SQLite table from a Node.js application, you follow these steps:

1. [Open a database connection](https://www.sqlitetutorial.net/sqlite-nodejs/connect/).
2. Execute an `INSERT` statement.
3. Close the database connection.

For the demonstration, we will create a new database named `sample.db` in the `db` folder.

When you open a database connection in the default mode, the database is created if it does not exist.

```js
let db = new sqlite3.Database('./db/sample.db');
```

In the `sample.db` database, we [create a table](https://www.sqlitetutorial.net/sqlite-create-table/) called `langs` for storing programming languages:

```js
db.run('CREATE TABLE langs(name text)');
```

You can run the program to create the `sample.db` database and `langs` table as follows:

```js
const sqlite3 = require('sqlite3').verbose();

let db = new sqlite3.Database('../db/sample.db');

db.run('CREATE TABLE langs(name text)');

db.close();
```

Now, we are ready to insert data into the `langs` table.

## Insert one row into a table

To execute an `INSERT` statement, you use the `run()` method of the `Database` object:

```js
db.run(sql, params, function(err){
  // 
});
```

The `run()` method executes an `INSERT` statement with specified parameters and calls a callback afterwards.

If an error occurred, you can find the detailed information in the `err` argument of the callback function.

In case the statement is executed successfully, the `this` object of the callback function will contain two properties:

- `lastID` property stores the value of the last inserted row ID.
- `changes` property stores the rows affected by the query.

The following `insert.js` program illustrates how to insert a row into the `langs` table:

```js
  const sqlite3 = require('sqlite3').verbose();

  let db = new sqlite3.Database('./db/sample.db');

  // insert one row into the langs table
  db.run(`INSERT INTO langs(name) VALUES(?)`, ['C'], function(err) {
    if (err) {
      return console.log(err.message);
    }
    // get the last insert id
    console.log(`A row has been inserted with rowid ${this.lastID}`);
  });

  // close the database connection
  db.close();
```

Let’s run the `insert.js` program:

```shell
>node insert.js
A row has been inserted with rowid 1
```

It worked as expected.

## Insert multiple rows into a table at a time

To [insert multiple rows](https://www.sqlitetutorial.net/sqlite-insert/) at a time into a table, you use the following form of the `INSERT` statement:

```sql
INSERT INTO table_name(column_name)
VALUES(value_1), (value_2), (value_3),...
```

To simulate this in the Node.js application, we first need to construct the `INSERT` statement with multiple placeholders:

```sql
INSERT INTO table_name(column_name)
VALUES(?), (?), (?),...
```

Suppose, you want to insert rows into the `langs` table with the data from the following `languages` array:

```js
let languages = ['C++', 'Python', 'Java', 'C#', 'Go'];
```

To construct the `INSERT` statement, we use the `map()` method to map each element in the `languages` array into `(?)` and then join all placeholders together.

```js
let placeholders = languages.map((language) => '(?)').join(',');
let sql = 'INSERT INTO langs(name) VALUES ' + placeholders;
```

The following `insert-many.js` program illustrates how to insert multiple rows into the `langs`table:

```js
const sqlite3 = require('sqlite3').verbose();

// open the database connection
let db = new sqlite3.Database('../db/sample.db');

let languages = ['C++', 'Python', 'Java', 'C#', 'Go'];

// construct the insert statement with multiple placeholders
// based on the number of rows
let placeholders = languages.map((language) => '(?)').join(',');
let sql = 'INSERT INTO langs(name) VALUES ' + placeholders;

// output the INSERT statement
console.log(sql);

db.run(sql, languages, function(err) {
  if (err) {
    return console.error(err.message);
  }
  console.log(`Rows inserted ${this.changes}`);
});

// close the database connection
db.close();
```

Let’s run the `insert-many.js` program to see how it works.

```shell
> node insert-many.js
INSERT INTO langs(name) VALUES (?),(?),(?),(?),(?)
Rows inserted 5
```

It inserted 5 rows into the `langs` table which is what we expected.

In this tutorial, you have learned how to insert one or more rows into an SQLite table from a Node.js application.



## See Also

- https://www.sqlitetutorial.net/sqlite-nodejs/
