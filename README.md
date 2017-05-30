# pouchdb-electron

PouchDB works great with Electron (formerly known as Atom Shell). Here's how to get started.

## Demo app

* [Hello Electron with PouchDB](https://github.com/nolanlawson/hello-electron-with-pouchdb)

## Installation

To use PouchDB in your Electron app, just download [pouchdb.js](http://pouchdb.com/guides/setup-pouchdb.html) and include it in your `index.html`:

```html
<script src="path/to/pouchdb.js"></script>
```

Alternatively - the npm package `pouchdb-browser` can be installed and required in the usual way. Note that the `pouchdb` package will always attempt to use a LevelDB adapter.

```js
import PouchDB from 'pouchdb-browser' 
```

Now `PouchDB` is available as a global variable. So you can create an IndexedDB-based PouchDB:

```js
var db = new PouchDB('mydb');
```

or a WebSQL-based PouchDB:

```js
var db = new PouchDB('mydb', {adapter: 'websql'});
```

Use whichever one you prefer. They both work the same, although in my experience WebSQL is slightly faster than IndexedDB in Chromium, for most use cases. (Electron is based on Chromium.)

## Using LevelDB via LevelDOWN



You can also use PouchDB in a Node.js style with the LevelDB adapter:

```js
var PouchDB = require('pouchdb');
var db = new PouchDB('mydb');
```

However, you will have to rebuild the LevelDB binaries for Electron. The [demo app](https://github.com/nolanlawson/hello-electron-with-pouchdb) shows how to accomplish this.

Basically you will need to run [electron-rebuild](https://github.com/paulcbetts/electron-rebuild) as a `postinstall` step. If you are unable to get this to work properly for all your target environments, then you may need to just stick with the in-browser IndexedDB or WebSQL adapters, and avoid the native LevelDB or SQLite (node-websql) adapters.

**Note**: If you're getting an `IO Error:`/`OpenError` _after packaging_ your app, you'll need to make sure you set the database directory explicitly (using `require('path')` and `__dirname`, for example, like `new PouchDB(path.join(__dirname, 'mydb))`).
