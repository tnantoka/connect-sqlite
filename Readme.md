# Connect SQLite3

connect-sqlite3 is a SQLite3 session store modeled after the TJ's connect-redis store.


## Installation
```sh
	  $ npm install connect-sqlite3
```

## Options

  - `table='sessions'` Database table name
  - `db='sessionsDB'` Database file name (defaults to table name)
  - `dir='.'` Directory to save '<db>.db' file
  - `concurrentDB='false'` Enables [WAL](https://www.sqlite.org/wal.html) mode (defaults to false)

## Usage
```js
    var connect = require('connect'),
        SQLiteStore = require('connect-sqlite3')(connect);

    connect.createServer(
      connect.cookieParser(),
      connect.session({ store: new SQLiteStore, secret: 'your secret' })
    );
```
  with express
```js
    3.x:
    var SQLiteStore = require('connect-sqlite3')(express);

    4.x:
    var session = require('express-session');
    var SQLiteStore = require('connect-sqlite3')(session);

    app.configure(function() {
      app.set('views', __dirname + '/views');
      app.set('view engine', 'ejs');
      app.use(express.bodyParser());
      app.use(express.methodOverride());
      app.use(express.cookieParser());
      app.use(session({
        store: new SQLiteStore,
        secret: 'your secret',
        cookie: { maxAge: 7 * 24 * 60 * 60 * 1000 } // 1 week
      }));
      app.use(app.router);
      app.use(express.static(__dirname + '/public'));
    });
```
## Test
```sh
    $ npm test
```
