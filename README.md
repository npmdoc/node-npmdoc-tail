# api documentation for  [tail (v1.2.1)](http://www.lucagrulla.com/node-tail)  [![npm package](https://img.shields.io/npm/v/npmdoc-tail.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-tail) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-tail.svg)](https://travis-ci.org/npmdoc/node-npmdoc-tail)
#### tail a file in node

[![NPM](https://nodei.co/npm/tail.png?downloads=true)](https://www.npmjs.com/package/tail)

[![apidoc](https://npmdoc.github.io/node-npmdoc-tail/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-tail_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-tail/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-tail/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-tail/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Luca Grulla",
        "url": "http://www.lucagrulla.com"
    },
    "bugs": {
        "url": "https://github.com/lucagrulla/node-tail/issues"
    },
    "contributors": [
        {
            "name": "Luca Grulla"
        },
        {
            "name": "Tom Hall"
        }
    ],
    "dependencies": {},
    "description": "tail a file in node",
    "devDependencies": {
        "chai": "^3.2.0",
        "coffee-script": "1.10.0",
        "mocha": "^3.0.2"
    },
    "directories": {},
    "dist": {
        "shasum": "c998a0cd9f8bf6dce780a6bc7339e66371e0db3f",
        "tarball": "https://registry.npmjs.org/tail/-/tail-1.2.1.tgz"
    },
    "engines": {
        "node": ">= 0.4.0"
    },
    "gitHead": "a3ccc0de8796e71088666b75dd46fa97e8b43cd1",
    "homepage": "http://www.lucagrulla.com/node-tail",
    "license": "MIT",
    "main": "lib/tail",
    "maintainers": [
        {
            "name": "lucagrulla",
            "email": "luca.grulla@gmail.com"
        }
    ],
    "name": "tail",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/lucagrulla/node-tail.git"
    },
    "scripts": {},
    "version": "1.2.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module tail](#apidoc.module.tail)
1.  [function <span class="apidocSignatureSpan">tail.</span>Tail (filename, options)](#apidoc.element.tail.Tail)
1.  object <span class="apidocSignatureSpan">tail.</span>Tail.prototype

#### [module tail.Tail](#apidoc.module.tail.Tail)
1.  boolean <span class="apidocSignatureSpan">tail.Tail.</span>usingDomains
1.  [function <span class="apidocSignatureSpan">tail.</span>Tail (filename, options)](#apidoc.element.tail.Tail.Tail)
1.  [function <span class="apidocSignatureSpan">tail.Tail.</span>EventEmitter ()](#apidoc.element.tail.Tail.EventEmitter)
1.  [function <span class="apidocSignatureSpan">tail.Tail.</span>init ()](#apidoc.element.tail.Tail.init)
1.  [function <span class="apidocSignatureSpan">tail.Tail.</span>listenerCount (emitter, type)](#apidoc.element.tail.Tail.listenerCount)
1.  number <span class="apidocSignatureSpan">tail.Tail.</span>defaultMaxListeners
1.  object <span class="apidocSignatureSpan">tail.Tail.</span>__super__

#### [module tail.Tail.prototype](#apidoc.module.tail.Tail.prototype)
1.  [function <span class="apidocSignatureSpan">tail.Tail.prototype.</span>constructor (filename, options)](#apidoc.element.tail.Tail.prototype.constructor)
1.  [function <span class="apidocSignatureSpan">tail.Tail.prototype.</span>readBlock ()](#apidoc.element.tail.Tail.prototype.readBlock)
1.  [function <span class="apidocSignatureSpan">tail.Tail.prototype.</span>unwatch ()](#apidoc.element.tail.Tail.prototype.unwatch)
1.  [function <span class="apidocSignatureSpan">tail.Tail.prototype.</span>watch (pos)](#apidoc.element.tail.Tail.prototype.watch)
1.  [function <span class="apidocSignatureSpan">tail.Tail.prototype.</span>watchEvent (e)](#apidoc.element.tail.Tail.prototype.watchEvent)
1.  [function <span class="apidocSignatureSpan">tail.Tail.prototype.</span>watchFileEvent (curr, prev)](#apidoc.element.tail.Tail.prototype.watchFileEvent)



# <a name="apidoc.module.tail"></a>[module tail](#apidoc.module.tail)

#### <a name="apidoc.element.tail.Tail"></a>[function <span class="apidocSignatureSpan">tail.</span>Tail (filename, options)](#apidoc.element.tail.Tail)
- description and source-code
```javascript
function Tail(filename, options) {
  var pos, ref, ref1, ref2, ref3, ref4;
  this.filename = filename;
  if (options == null) {
    options = {};
  }
  this.readBlock = bind(this.readBlock, this);
  this.separator = (ref = options.separator) != null ? ref : /[\r]{0,1}\n/, this.fsWatchOptions = (ref1 = options.fsWatchOptions
) != null ? ref1 : {}, this.fromBeginning = (ref2 = options.fromBeginning) != null ? ref2 : false, this.follow = (ref3 = options
.follow) != null ? ref3 : true, this.logger = options.logger, this.useWatchFile = (ref4 = options.useWatchFile) != null ? ref4 :
false;
  if (this.logger) {
    this.logger.info("Tail starting...");
    this.logger.info("filename: " + this.filename);
  }
  this.buffer = '';
  this.internalDispatcher = new events.EventEmitter();
  this.queue = [];
  this.isWatching = false;
  this.internalDispatcher.on('next', (function(_this) {
    return function() {
      return _this.readBlock();
    };
  })(this));
  if (this.fromBeginning) {
    pos = 0;
  }
  this.watch(pos);
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.tail.Tail"></a>[module tail.Tail](#apidoc.module.tail.Tail)

#### <a name="apidoc.element.tail.Tail.Tail"></a>[function <span class="apidocSignatureSpan">tail.</span>Tail (filename, options)](#apidoc.element.tail.Tail.Tail)
- description and source-code
```javascript
function Tail(filename, options) {
  var pos, ref, ref1, ref2, ref3, ref4;
  this.filename = filename;
  if (options == null) {
    options = {};
  }
  this.readBlock = bind(this.readBlock, this);
  this.separator = (ref = options.separator) != null ? ref : /[\r]{0,1}\n/, this.fsWatchOptions = (ref1 = options.fsWatchOptions
) != null ? ref1 : {}, this.fromBeginning = (ref2 = options.fromBeginning) != null ? ref2 : false, this.follow = (ref3 = options
.follow) != null ? ref3 : true, this.logger = options.logger, this.useWatchFile = (ref4 = options.useWatchFile) != null ? ref4 :
false;
  if (this.logger) {
    this.logger.info("Tail starting...");
    this.logger.info("filename: " + this.filename);
  }
  this.buffer = '';
  this.internalDispatcher = new events.EventEmitter();
  this.queue = [];
  this.isWatching = false;
  this.internalDispatcher.on('next', (function(_this) {
    return function() {
      return _this.readBlock();
    };
  })(this));
  if (this.fromBeginning) {
    pos = 0;
  }
  this.watch(pos);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.tail.Tail.EventEmitter"></a>[function <span class="apidocSignatureSpan">tail.Tail.</span>EventEmitter ()](#apidoc.element.tail.Tail.EventEmitter)
- description and source-code
```javascript
function EventEmitter() {
  EventEmitter.init.call(this);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.tail.Tail.init"></a>[function <span class="apidocSignatureSpan">tail.Tail.</span>init ()](#apidoc.element.tail.Tail.init)
- description and source-code
```javascript
init = function () {
  this.domain = null;
  if (EventEmitter.usingDomains) {
    // if there is an active domain, then attach to it.
    domain = domain || require('domain');
    if (domain.active && !(this instanceof domain.Domain)) {
      this.domain = domain.active;
    }
  }

  if (!this._events || this._events === Object.getPrototypeOf(this)._events) {
    this._events = new EventHandlers();
    this._eventsCount = 0;
  }

  this._maxListeners = this._maxListeners || undefined;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.tail.Tail.listenerCount"></a>[function <span class="apidocSignatureSpan">tail.Tail.</span>listenerCount (emitter, type)](#apidoc.element.tail.Tail.listenerCount)
- description and source-code
```javascript
listenerCount = function (emitter, type) {
  if (typeof emitter.listenerCount === 'function') {
    return emitter.listenerCount(type);
  } else {
    return listenerCount.call(emitter, type);
  }
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.tail.Tail.prototype"></a>[module tail.Tail.prototype](#apidoc.module.tail.Tail.prototype)

#### <a name="apidoc.element.tail.Tail.prototype.constructor"></a>[function <span class="apidocSignatureSpan">tail.Tail.prototype.</span>constructor (filename, options)](#apidoc.element.tail.Tail.prototype.constructor)
- description and source-code
```javascript
function Tail(filename, options) {
  var pos, ref, ref1, ref2, ref3, ref4;
  this.filename = filename;
  if (options == null) {
    options = {};
  }
  this.readBlock = bind(this.readBlock, this);
  this.separator = (ref = options.separator) != null ? ref : /[\r]{0,1}\n/, this.fsWatchOptions = (ref1 = options.fsWatchOptions
) != null ? ref1 : {}, this.fromBeginning = (ref2 = options.fromBeginning) != null ? ref2 : false, this.follow = (ref3 = options
.follow) != null ? ref3 : true, this.logger = options.logger, this.useWatchFile = (ref4 = options.useWatchFile) != null ? ref4 :
false;
  if (this.logger) {
    this.logger.info("Tail starting...");
    this.logger.info("filename: " + this.filename);
  }
  this.buffer = '';
  this.internalDispatcher = new events.EventEmitter();
  this.queue = [];
  this.isWatching = false;
  this.internalDispatcher.on('next', (function(_this) {
    return function() {
      return _this.readBlock();
    };
  })(this));
  if (this.fromBeginning) {
    pos = 0;
  }
  this.watch(pos);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.tail.Tail.prototype.readBlock"></a>[function <span class="apidocSignatureSpan">tail.Tail.prototype.</span>readBlock ()](#apidoc.element.tail.Tail.prototype.readBlock)
- description and source-code
```javascript
readBlock = function () {
  var block, stream;
  if (this.queue.length >= 1) {
    block = this.queue.shift();
    if (block.end > block.start) {
      stream = fs.createReadStream(this.filename, {
        start: block.start,
        end: block.end - 1,
        encoding: "utf-8"
      });
      stream.on('error', (function(_this) {
        return function(error) {
          if (_this.logger) {
            _this.logger.error("Tail error: " + error);
          }
          return _this.emit('error', error);
        };
      })(this));
      stream.on('end', (function(_this) {
        return function() {
          if (_this.queue.length >= 1) {
            return _this.internalDispatcher.emit("next");
          }
        };
      })(this));
      return stream.on('data', (function(_this) {
        return function(data) {
          var chunk, i, len, parts, results;
          _this.buffer += data;
          parts = _this.buffer.split(_this.separator);
          _this.buffer = parts.pop();
          results = [];
          for (i = 0, len = parts.length; i < len; i++) {
            chunk = parts[i];
            results.push(_this.emit("line", chunk));
          }
          return results;
        };
      })(this));
    }
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.tail.Tail.prototype.unwatch"></a>[function <span class="apidocSignatureSpan">tail.Tail.prototype.</span>unwatch ()](#apidoc.element.tail.Tail.prototype.unwatch)
- description and source-code
```javascript
unwatch = function () {
  if (this.watcher) {
    this.watcher.close();
  } else {
    fs.unwatchFile(this.filename);
  }
  this.isWatching = false;
  return this.queue = [];
}
```
- example usage
```shell
...
  console.log('ERROR: ', error);
});
'''

If you want to stop tail:

'''javascript
tail.unwatch()
'''

To start watching again:
'''javascript
tail.watch()
'''
...
```

#### <a name="apidoc.element.tail.Tail.prototype.watch"></a>[function <span class="apidocSignatureSpan">tail.Tail.prototype.</span>watch (pos)](#apidoc.element.tail.Tail.prototype.watch)
- description and source-code
```javascript
watch = function (pos) {
  var stats;
  if (this.isWatching) {
    return;
  }
  this.isWatching = true;
  stats = fs.statSync(this.filename);
  this.pos = pos != null ? pos : stats.size;
  if (this.logger) {
    this.logger.info("filesystem.watch present? " + (fs.watch !== void 0));
    this.logger.info("useWatchFile: " + this.useWatchFile);
  }
  if (!this.useWatchFile && fs.watch) {
    if (this.logger) {
      this.logger.info("watch strategy: watch");
    }
    return this.watcher = fs.watch(this.filename, this.fsWatchOptions, (function(_this) {
      return function(e) {
        return _this.watchEvent(e);
      };
    })(this));
  } else {
    if (this.logger) {
      this.logger.info("watch strategy: watchFile");
    }
    return fs.watchFile(this.filename, this.fsWatchOptions, (function(_this) {
      return function(curr, prev) {
        return _this.watchFileEvent(curr, prev);
      };
    })(this));
  }
}
```
- example usage
```shell
...

'''javascript
tail.unwatch()
'''

To start watching again:
'''javascript
tail.watch()
'''

# Configuration
The only mandatory parameter is the path to the file to tail.

'''javascript
var fileToTail = "/path/to/fileToTail.txt";
...
```

#### <a name="apidoc.element.tail.Tail.prototype.watchEvent"></a>[function <span class="apidocSignatureSpan">tail.Tail.prototype.</span>watchEvent (e)](#apidoc.element.tail.Tail.prototype.watchEvent)
- description and source-code
```javascript
watchEvent = function (e) {
  var stats;
  if (e === 'change') {
    stats = fs.statSync(this.filename);
    if (stats.size < this.pos) {
      this.pos = stats.size;
    }
    if (stats.size > this.pos) {
      this.queue.push({
        start: this.pos,
        end: stats.size
      });
      this.pos = stats.size;
      if (this.queue.length === 1) {
        return this.internalDispatcher.emit("next");
      }
    }
  } else if (e === 'rename') {
    this.unwatch();
    if (this.follow) {
      return setTimeout(((function(_this) {
        return function() {
          return _this.watch();
        };
      })(this)), 1000);
    } else {
      if (this.logger) {
        this.logger.error("'rename' event for " + this.filename + ". File not available.");
      }
      return this.emit("error", "'rename' event for " + this.filename + ". File not available.");
    }
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.tail.Tail.prototype.watchFileEvent"></a>[function <span class="apidocSignatureSpan">tail.Tail.prototype.</span>watchFileEvent (curr, prev)](#apidoc.element.tail.Tail.prototype.watchFileEvent)
- description and source-code
```javascript
watchFileEvent = function (curr, prev) {
  if (curr.size > prev.size) {
    this.queue.push({
      start: prev.size,
      end: curr.size
    });
    if (this.queue.length === 1) {
      return this.internalDispatcher.emit("next");
    }
  }
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
