# pouchdb-electron

PouchDB works great with Electron (formerly known as Atom Shell). Here's how to get started.

## Sample app

* ["Hello atom" with PouchDB app](https://github.com/nolanlawson/hello-atom-with-pouchdb)

## Installation

To use PouchDB in your Electron app, just download [pouchdb.js](http://pouchdb.com/guides/setup-pouchdb.html) and include it in your `index.html`:

```html
<script src="path/to/pouchdb.js"></script>
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

You can also use PouchDB in a Node.js style with the LevelDB adapter, but it's a bit trickier to install compared to the IndexedDB/WebSQL adapters. It should be worth it, though, since LevelDB tends to be the fastest PouchDB adapter.

Essentially you'll need to rebuild LevelDB for Electron. There is a demo of how to do so  in [Level/electron-demo](https://github.com/Level/electron-demo). Basically you will need to run this script as a `postinstall` step:

```bash
cd node_modules/pouchdb/node_modules/leveldown
HOME=~/.electron-gyp node-gyp rebuild \
  --target=0.29.1 --arch=x64 \
  --dist-url=https://atom.io/download/atom-shell
```

Then you can use PouchDB over LevelDB like so:

```js
var db = new PouchDB('mydb', {adapter: 'leveldb'});
```
