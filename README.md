gs
==

[![Build Status](https://travis-ci.org/spreecode/node-gs.svg?branch=master)](https://travis-ci.org/spreecode/node-gs)

NodeJS wrapper for `gs`


Usage
=====

```javascript
    var gs = require('gs');

    gs(inputFile)
      .include(`${__dirname}/my-portable-ghostscript/share/ghostscript/9.19/Resource/Init/`)
      .batch()
      .nopause()
      .output(outputFile)
      .exec(function(err, data) {
        console.log(data.toString());
      });
```

API
===

* `batch`
* `nopause`
* `device` - device - defaults to `txtwrite`
* `output` - file - defaults to `-` which represents stdout
* `input` - file
* `exec` - callback


License
=======

MIT - http://ncb000gt.mit-license.org/
