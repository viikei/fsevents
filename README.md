# fsevents [![NPM](https://nodei.co/npm/fsevents.png)](https://nodei.co/npm/fsevents/)

Native access to MacOS FSEvents in [Node.js](http://nodejs.org/)

The FSEvents API in MacOS allows applications to register for notifications of
changes to a given directory tree. It is a very fast and lightweight alternative
to kqueue.

This is a low-level library. For a cross-compatible file watching module that
uses fsevents, check out [Chokidar](https://www.npmjs.com/package/chokidar).

* [Module Site & GitHub](https://github.com/fsevents/fsevents)
* [NPM Page](https://npmjs.org/package/fsevents)

## Installation

	npm install fsevents

## Usage

```js
const fsevents = require('fsevents');
const stop = fsevents.watch(__dirname, (path, flags, id)=>{
  const info = fsevents.getInfo(path, flags, id);
}); // To start observation
stop(); // To end observation
```

### Callback

The callback passed as the second parameter to `.watch` get's called whenever the operating system detects a
a change in the file system. It takes three arguments:

 * `path` - which is a string naming the path of the item in the filesystem that changed
 * `flags` - a numeric value describing what the change was
 * `id` - a unique-id identifying this specific event

### `getInfo(path, flags, id) => {info-object}`

The `getInfo` function takes the `path`, `flags` and `id` arguments and converts those parameters into a structure
that is easier to digest to determine what the change was.

The `info-object` has the following shape:

```js
{
  "event": "<deleted|moved|created|modified|root-changed|unknown>",
  "path": "<path-that-this-is-about>",
  "type": "<file|directory|symlink>",
  "changes": {
    "inode": true, // Has the iNode Meta-Information changed
    "finder": false, // Has the Finder Meta-Data changed
    "access": false, // Have the access permissions changed
    "xattrs": false // Have the xAttributes changed
  },
  "flags": <raw-flags>
}
```

## MIT License

Copyright (C) 2010-2018 by Philipp Dunkel, Ben Noordhuis, Elan Shankar

See LICENSE file.