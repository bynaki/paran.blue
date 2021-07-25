---
title: "Node :: Deleting Data in SQLite Database from a Node.js Application"
date: 2021-07-25T20:19:44+09:00
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
canonicalURL: "https://www.sqlitetutorial.net/sqlite-nodejs/delete/"
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



**Summary**: in this tutorial, you will learn how to delete data in the SQLite database from a Node.js application.

To delete data in the SQLite database from a Node.js application, you use the following steps:

1. [Open a database connection](https://www.sqlitetutorial.net/sqlite-nodejs/connect/).
2. Execute a `DELETE` statement.
3. Close the database connection.

For the demonstration, we will use the `langs` table in the `sample.db` database that we created in the [previous tutorial](https://www.sqlitetutorial.net/sqlite-nodejs/insert/).

## Deleting data example

To delete data from a table, you use the `DELETE` statement as follows:

```sql
DELETE FROM table_name
WHERE column_name = value;
```

To execute the `DELETE` statement from a Node.js application, you call the `run()` method of the `Database` object as follows:

```js
db.run(sql, params, function(err) {
  // 
});
```

The `run()` method allows you to execute a `DELETE` statement with specified parameters and calls a callback function afterwards.

If there was any error during the execution of `DELETE` statement, the `err` argument of the callback function will provide the detail. In case the `DELETE` statement executed successfully, the `this` object of the callback function will contain the `changes` property that stores the number of rows deleted.

The following `delete.js` program illustrates how to delete a row from the `langs` table:

```js
const sqlite3 = require('sqlite3').verbose();

// open a database connection
let db = new sqlite3.Database('./db/sample.db', (err) => {
  if (err) {
    console.error(err.message);
  }
});

let id = 1;
// delete a row based on id
db.run(`DELETE FROM langs WHERE rowid=?`, id, function(err) {
  if (err) {
    return console.error(err.message);
  }
  console.log(`Row(s) deleted ${this.changes}`);
});

// close the database connection
db.close((err) => {
  if (err) {
    return console.error(err.message);
  }
});
```

Let’s test the `update.js` program.

```shell
>node delete.js
Row(s) deleted: 1
```

The output showed that one row has been deleted successfully.

In this tutorial, you have learned how to delete data in the SQLite database from a Node.js application.



## See Also

- https://www.sqlitetutorial.net/sqlite-nodejs/
