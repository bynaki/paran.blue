---
title: "Node :: Querying Data in SQLite Database from Node.js Applications"
date: 2021-07-23T00:21:52+09:00
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
canonicalURL: "https://www.sqlitetutorial.net/sqlite-nodejs/query/"
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



**Summary**: in this tutorial, you will learn how to query data from the SQLite database from a Node.js application using sqlite3 API.

To query data in SQLite database from a Node.js application, you use these steps:

1. [Open a database connection](https://www.sqlitetutorial.net/sqlite-nodejs/connect/).
2. Execute a `SELECT` statement and process the result set.
3. Close the database connection.

The `sqlite3` module provides you with some methods for querying data such as `all()`, `each()` and `get()`.



## Querying all rows with all() method

The `all()` method allows you to execute an SQL query with specified parameters and call a callback to access the rows in the result set.

The following is the signature of the `all()` method:

```js
db.all(sql,params,(err, rows ) => {
    // process rows here    
});
```

The `err` argument stores the error detail in case there was an error occurred during the execution of the query. Otherwise, the `err` will be `null`. If the query is executed successfully, the `rows` argument contains the result set of the query.

Because the `all()` method retrieves all rows and places them in the memory, therefore, for the large result set, you should use the `each()` method.

The following example illustrates how to query data from the `playlists` table in the sample database using the `all()` method:

```js
const sqlite3 = require('sqlite3').verbose();

// open the database
let db = new sqlite3.Database('./db/chinook.db');

let sql = `SELECT DISTINCT Name name FROM playlists
           ORDER BY name`;

db.all(sql, [], (err, rows) => {
  if (err) {
    throw err;
  }
  rows.forEach((row) => {
    console.log(row.name);
  });
});

// close the database connection
db.close();
```

Let’s run the program.

```shell
>node all.js
90's Music
Audiobooks
Brazilian Music
Classical
Classical 101 - Deep Cuts
Classical 101 - Next Steps
Classical 101 - The Basics
Grunge
Heavy Metal Classic
Movies
Music
Music Videos
On-The-Go 1
TV Shows
```

The output shows all playlists as expected.



## Query the first row in the result set

When you know that the result set contains zero or one row e.g., querying a row based on the primary key or querying with only one aggregate function such as count, sum, max, min, etc., you can use the `get()` method of `Database` object.

```js
db.get(sql, params, (err, row) => {
    // process the row here 
});
```

The `get()` method executes an SQL query and calls the callback function on the first result row. In case the result set is empty, the `row` argument is `undefined`.

The following `get.js` program demonstrates how to query a playlist by its id:

```js
const sqlite3 = require('sqlite3').verbose();

// open the database
let db = new sqlite3.Database('./db/chinook.db');

let sql = `SELECT PlaylistId id,
                  Name name
           FROM playlists
           WHERE PlaylistId  = ?`;
let playlistId = 1;

// first row only
db.get(sql, [playlistId], (err, row) => {
  if (err) {
    return console.error(err.message);
  }
  return row
    ? console.log(row.id, row.name)
    : console.log(`No playlist found with the id ${playlistId}`);

});

// close the database connection
db.close();
```

Let’s run the `get.js` program.

```shell
>node get.js
1 'Music'
```

The output shows the `Music` playlist which is correct.

If you change the `playlistId` to 0 and execute the `get.js` program again:

```shell
>node get.js
No playlist found with the id 0
```

It showed that no playlist found with id 0 as expected.



## Query rows with each() method

The `each()` method executes an SQL query with specified parameters and calls a callback for every row in the result set.

The following illustrates the signature of the `each()` method:

```js
db.each(sql,params, (err, result) => {
   // process each row here
});
```

If the result set is empty, the callback is never called. In case there is an error, the `err` parameter contains the detailed information.

The following `each.js` program illustrates how to use the `each()` method to query customer’s data from the `customers` table.

```js
const sqlite3 = require('sqlite3').verbose();

// open the database
let db = new sqlite3.Database('../db/chinook.db');

let sql = `SELECT FirstName firstName,
                  LastName lastName,
                  Email email
            FROM customers
            WHERE Country = ?
            ORDER BY FirstName`;

db.each(sql, ['USA'], (err, row) => {
  if (err) {
    throw err;
  }
  console.log(`${row.firstName} ${row.lastName} - ${row.email}`);
});

// close the database connection
db.close();
```

Let’s run the `each.js` program:

```shell
>node each.js
Dan Miller - dmiller@comcast.com
Frank Harris - fharris@google.com
Frank Ralston - fralston@gmail.com
Heather Leacock - hleacock@gmail.com
Jack Smith - jacksmith@microsoft.com
John Gordon - johngordon22@yahoo.com
Julia Barnett - jubarnett@gmail.com
Kathy Chase - kachase@hotmail.com
Michelle Brooks - michelleb@aol.com
Patrick Gray - patrick.gray@aol.com
Richard Cunningham - ricunningham@hotmail.com
Tim Goyer - tgoyer@apple.com
Victor Stevens - vstevens@yahoo.com
```

As you see, the callback function was called for each row to print out the customer’s information.

In this tutorial, you have learned how to use various methods of the `Database` object to query data from the SQLite database.



## See Also

- https://www.sqlitetutorial.net/sqlite-nodejs/
