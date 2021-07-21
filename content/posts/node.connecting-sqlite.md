---
title: "Node :: Connecting To SQLite Database Using Node.js"
date: 2021-07-22T00:31:40+09:00
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
canonicalURL: "https://www.sqlitetutorial.net/sqlite-nodejs/connect/"
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



**Summary**: in this tutorial, you will learn how to connect to an SQLite database from Node.js applications.



## Installing sqlite3 module

To interact with the SQLite database, you need to download and install [`sqlite3`](https://github.com/mapbox/node-sqlite3) module. You can use `npm` to do so using the following command:

```shell
> npm install sqlite3
```

After installing the `sqlite3` module, you are ready to connect to a SQLite database from a Node.js application.

@types도 같이 깔자.

```shell
> npm install --save-dev @types/sqlite3
```



To connect to an SQLite database, you need to:

1. First, import the `sqlite3` module
2. Second, call the `Database()` function of the `sqlite3` module and pass the database information such as database file, opening mode, and a callback function.



## Connecting to the in-memory database

To open a database connection to an in-memory database, you use the following steps.

First, import the `sqlite3` module:

```js
const sqlite3 = require('sqlite3').verbose();
```

Notice that the execution mode is set to verbose to produce long stack traces.

Second, create a `Database` object:

```js
let db = new sqlite3.Database(':memory:');
```

The `sqlite3.Database()` returns a `Database` object and opens the database connection automatically.

The `sqlite3.Database()` accepts a callback function that will be called when the database opened successfully or when an error occurred.

The callback function has the `error` object as the first parameter. If an `error` occurred, the `error` object is not `null`, otherwise, it is `null`.

If you don’t provide the callback function and an error occurred during opening the database, an `error` event will be emitted. In case the database is opened successfully, the `open` event is emitted regardless of whether a callback is provided or not.

So you now can open an SQLite database and provide the detailed information if an error occurred as follows:

```js
let db = new sqlite3.Database(':memory:', (err) => {
  if (err) {
    return console.error(err.message);
  }
  console.log('Connected to the in-memory SQlite database.');
});
```

It is a good practice to close a database connection when you are done with it. To close a database connection, you call the `close()` method of the `Database` object as follows:

```js
db.close();
```

The `close()` method will wait for all pending queries completed before actually closing the database.

Similar to the `Database()`, the `close()` method also accepts a callback that indicates whether an error occurred during closing the database connection.

```js
db.close((err) => {
  if (err) {
    return console.error(err.message);
  }
  console.log('Close the database connection.');
});
```

The following illustrates the complete code for opening and closing an in-memory SQLite database:

```js
const sqlite3 = require('sqlite3').verbose();

// open database in memory
let db = new sqlite3.Database(':memory:', (err) => {
  if (err) {
    return console.error(err.message);
  }
  console.log('Connected to the in-memory SQlite database.');
});

// close the database connection
db.close((err) => {
  if (err) {
    return console.error(err.message);
  }
  console.log('Close the database connection.');
});
```

Let’s run the program to see how it works.

```shell
> node connect.js
Connected to the in-memory SQlite database.
Close the database connection.
```

As you can see, it works perfectly as expected.



## Connecting to a disk file database

To connect to a disk file database, instead of passing the `':memory:'` string, you pass the path to the database file.

For example, to connect to the `chinook` database file stored in the `db` folder, you use the following statement:

```js
let db = new sqlite3.Database('./db/chinook.db', (err) => {
  if (err) {
    console.error(err.message);
  }
  console.log('Connected to the chinook database.');
});
```

There are three opening modes:

1. `sqlite3.OPEN_READONLY`: open the database for read-only.
2. `sqlite3.OPEN_READWRITE` : open the database for reading and writting.
3. `sqlite3.OPEN_CREATE`: open the database, if the database does not exist, create a new database.

The `sqlite3.Database()` accepts one or more mode as the second argument. By default, it uses the `OPEN_READWRITE | OPEN_CREATE` mode. It means that if the database does not exist, the new database will be created and is ready for read and write.

To open the `chinook` sample database for read and write, you can do it as follows:

```js
let db = new sqlite3.Database('./db/chinook.db', sqlite3.OPEN_READWRITE, (err) => {
  if (err) {
    console.error(err.message);
  }
  console.log('Connected to the chinook database.');
});
```

The following example shows the complete code for opening the `chinook` database, querying data from the `playlists` table, and closing the database connection.

```js
const sqlite3 = require('sqlite3').verbose();

// open the database
let db = new sqlite3.Database('./db/chinook.db', sqlite3.OPEN_READWRITE, (err) => {
  if (err) {
    console.error(err.message);
  }
  console.log('Connected to the chinook database.');
});

db.serialize(() => {
  db.each(`SELECT PlaylistId as id,
                  Name as name
           FROM playlists`, (err, row) => {
    if (err) {
      console.error(err.message);
    }
    console.log(row.id + "\t" + row.name);
  });
});

db.close((err) => {
  if (err) {
    console.error(err.message);
  }
  console.log('Close the database connection.');
});
```

Note that you will learn [how to query data](https://www.sqlitetutorial.net/sqlite-nodejs/query/) in the next tutorial.

In this tutorial, you have learned how to connect to an SQLite database either in-memory or disk file based database.



## See Also

- https://www.sqlitetutorial.net/sqlite-nodejs/
