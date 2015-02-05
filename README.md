# pouchdb-atom-shell

PouchDB works great with Atom Shell. Here's how to get started.

## Sample app

* ["Hello atom" with PouchDB app](https://github.com/nolanlawson/hello-atom-with-pouchdb)

## Installation

To use PouchDB in your Atom Shell app, just download [pouchdb.js](http://pouchdb.com/guides/setup-pouchdb.html) and include it in your `index.html`:

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

Use whichever one you prefer. They both work the same, although in my experience WebSQL is slightly faster than IndexedDB in Chromium, for most use cases. (Atom Shell is based on Chromium.)
