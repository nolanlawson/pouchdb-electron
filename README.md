# pouchdb-electron

PouchDB works great with Electron (formerly known as Atom Shell). Here's how to get started.

## Demo app

* [Hello Electron with PouchDB](https://github.com/nolanlawson/hello-electron-with-pouchdb)

## Installation

To use PouchDB in your Electron app, just download [pouchdb.js](http://pouchdb.com/guides/setup-pouchdb.html) and include it in your `index.html`:

```html
<script src="path/to/pouchdb.js"></script>
```

(Or `npm install` or `bower install`.)

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

Basically you will need to run this script as a `postinstall` step:

```bash
cd node_modules/leveldown
HOME=~/.electron-gyp node-gyp rebuild \
  --target=0.29.1 --arch=x64 \
  --dist-url=https://atom.io/download/atom-shell
```

If this doesn't work on your system, you can always use the IndexedDB/WebSQL adapters instead. The performance benefit from using LevelDB is (probably) minor.
