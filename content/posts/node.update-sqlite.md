---
title: "Node :: Updating Data in SQLite Database from a Node.js Application"
date: 2021-07-25T16:25:41+09:00
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
canonicalURL: "https://www.sqlitetutorial.net/sqlite-nodejs/update/"
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



**Summary**: this tutorial shows you how to update data in the SQLite database from a Node.js application.

To update data in the SQLite database from a Node.js application, you use these steps:

1. [Open a database connection](https://www.sqlitetutorial.net/sqlite-nodejs/connect/).
2. Execute an `UPDATE` statement.
3. Close the database connection.

For the demonstration, we will use the `langs` table in the `sample.db` database that we created in the [previous tutorial](https://www.sqlitetutorial.net/sqlite-nodejs/insert/).

## Updating data example

To update data in a table, you use the `UPDATE` statement as follows:

```sql
UPDATE table_name
SET column_name = value_1
WHERE id = id_value;
```

To execute the `UPDATE` statement in the Node.js application, you call the `run()` method of the `Database` object:

```js
db.run(sql, params, function(err){
  // 
});
```

The `run()` method executes an `UPDATE` statement with specified parameters and calls a callback afterwards.

The `err` argument of the callback stores the error detail in case the execution has any problem e.g., syntax error, locking, etc.

If the `UPDATE` statement is executed successfully, the `this` object of the callback function will contain the `changes` property that stores the number of rows updated.

The following `update.js` program illustrates how to update a row in the `langs` table from `C` to `Ansi C`:

```js
const sqlite3 = require('sqlite3').verbose();

// open a database connection
let db = new sqlite3.Database('./db/sample.db');

//
let data = ['Ansi C', 'C'];
let sql = `UPDATE langs
            SET name = ?
            WHERE name = ?`;

db.run(sql, data, function(err) {
  if (err) {
    return console.error(err.message);
  }
  console.log(`Row(s) updated: ${this.changes}`);

});

// close the database connection
db.close();
```

Let’s test the `update.js` program.

```shell
>node update.js
Row(s) updated: 1
```

The output showed that one row has been updated which is correct.

In this tutorial, you have learned how to update data in the SQLite database from a Node.js application.



## See Also

- https://www.sqlitetutorial.net/sqlite-nodejs/
