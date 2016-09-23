# gs

[![Build Status](https://travis-ci.org/spreecode/node-gs.svg?branch=master)](https://travis-ci.org/spreecode/node-gs)

NodeJS wrapper for `gs`

# Usage

```javascript
    var gs = require('gs');

    gs(inputFile)
      .batch()
      .nopause()
      .output(outputFile)
      .exec(function(err, data) {
        console.log(data.toString());
      });
```

# API

* `include` - set path to `gs_init.ps` file (portable Ghostscript)
* `batch`
* `nopause`
* `device` - device - defaults to `txtwrite`
* `output` - file - defaults to `-` which represents stdout
* `input` - file
* `exec` - callback

## Events

* `data (text)`
* `page (currentPage)`
* `pages (firstPage, lastPage)`

```javascript
    gs(inputFile)
      .output(outputFile)
      .on('page', function(page) { console.debug('processing page:', page); })
      .exec(function(err, data) {
        console.log(data.toString());
      });
```

# License

MIT - http://ncb000gt.mit-license.org/
