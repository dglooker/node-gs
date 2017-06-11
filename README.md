node-gs
=====

NodeJS wrapper for `gs` (GhostScript).

Installation
=====

```sh
npm install https://github.com/MiroHibler/node-gs/tarball/master
```

or

```javascript
    "dependencies": {
        "gs": "https://github.com/MiroHibler/node-gs/tarball/master"
    }
```

Usage
=====

Sample usage:

```javascript
    var gs = require( 'gs' );

    gs()
        .batch()
        .nopause()
        .option( '-r' + 50 * 2 )
        .option( '-dDownScaleFactor=2' )
        .device( 'png16m' )
        .input( '/tmp/' + fileName )
		.output( '/tmp/' + fileName + '-%d.png' )
        // optional:
        .executablePath( 'ghostscript/bin/./gs' )
        .exec( function ( error, stdout, stderr ) {
            if ( error ) {
                // ¯\_(ツ)_/¯
            } else {
                // ( ͡° ͜ʖ ͡°)
            }
        });
```

Usage with piping input and output:

```javascript
    var gs = require( 'gs' ),
        fs = require( 'fs' ),
        input = fs.readFileSync( '/tmp/' + fileName );

    if ( input ) {
        gs()
            .option( '-r' + 50 * 2 )
            .option( '-dDownScaleFactor=2' )
            .device( 'png16m' )
            .exec( input, function ( error, stdout, stderr ) {
                if ( error ) {
                    // ¯\_(ツ)_/¯
                } else {
                    // ( ͡° ͜ʖ ͡°)
                }
            });
    }
```

# API

* `batch` - set batch option
* `command` - tell gs to interpret PostScript code
* `currentDirectory` / `p` - tell gs to use current directory for libraries first
* `diskfonts` - set diskfonts option
* `define` - set definition with value
* `device` - device - defaults to `txtwrite`
* `executablePath` - path to the Ghostscript executable files (example: `ghostscript/bin/./gs`)
* `include` - set path to `gs_init.ps` file (portable Ghostscript)
array of include paths
* `input` - file or data for stdin (when invoked with `gs( '-' )`)
* `nobind` - set nobind option
* `nocache` - set nocache option
* `nodisplay` - set nodisplay option
* `nopause` - set nopause option
* `option` - add any option that is not provided through the methods
* `output` - file - defaults to `-` which represents stdout
* `page` - number - tell gs to process single page
* `pagecount` - return number of pages
* `pages` - numbers - tell gs to process page range
* `papersize` - set the paper size
* `quiet` / `q` - tell gs to be quiet
* `reset` - reset gs to initial state
* `resolution` / `res` / `r` - set device resolution
* `safer` - set gs to run in safe mode
* `exec` - callback

## Events

```javascript
    gs( inputFile )
        .output( outputFile )
        .on( 'pages', function ( from, to ) {
            console.debug( '[sg] Processing pages ' + from + '-' * to );
        })
        .on( 'page', function ( page ) {
            console.debug( '[sg] Processing page:', page );
        })
        .on( 'data', function ( data ) {
            console.log( '[sg] Data:', data.toString() );
        })
        .exec( function ( err, data ) {
            console.log( '[sg] Data:', data.toString() );
        });
```

# License

MIT - http://miro.mit-license.org/
