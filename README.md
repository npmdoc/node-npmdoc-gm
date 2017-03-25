# api documentation for  [gm (v1.23.0)](https://github.com/aheckmann/gm)  [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gm.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gm)
#### GraphicsMagick and ImageMagick for node.js

[![NPM](https://nodei.co/npm/gm.png?downloads=true)](https://www.npmjs.com/package/gm)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gm/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gm_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gm/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-gm/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "author": {
        "name": "Aaron Heckmann",
        "email": "aaron.heckmann+github@gmail.com"
    },
    "bugs": {
        "url": "http://github.com/aheckmann/gm/issues"
    },
    "dependencies": {
        "array-parallel": "~0.1.3",
        "array-series": "~0.1.5",
        "cross-spawn": "^4.0.0",
        "debug": "~2.2.0"
    },
    "description": "GraphicsMagick and ImageMagick for node.js",
    "devDependencies": {
        "async": "~0.9.0",
        "gleak": "~0.5.0"
    },
    "directories": {},
    "dist": {
        "shasum": "80a2fe9cbf131515024846444658461269f52661",
        "tarball": "https://registry.npmjs.org/gm/-/gm-1.23.0.tgz"
    },
    "engines": {
        "node": ">= 0.10.0"
    },
    "gitHead": "d650da6a1ca446c23641dba8d7e98c12e3f3b26c",
    "homepage": "https://github.com/aheckmann/gm",
    "keywords": [
        "graphics",
        "magick",
        "image",
        "graphicsmagick",
        "imagemagick",
        "gm",
        "convert",
        "identify",
        "compare"
    ],
    "license": "MIT",
    "licenses": [
        {
            "type": "MIT",
            "url": "http://www.opensource.org/licenses/mit-license.php"
        }
    ],
    "main": "./index",
    "maintainers": [
        {
            "name": "aaron",
            "email": "aaron.heckmann+github@gmail.com"
        },
        {
            "name": "jongleberry",
            "email": "me@jongleberry.com"
        },
        {
            "name": "rwky",
            "email": "admin@rwky.net"
        },
        {
            "name": "fragphace",
            "email": "fragphace@gmail.com"
        }
    ],
    "name": "gm",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/aheckmann/gm.git"
    },
    "scripts": {
        "test": "make test-unit; make test;"
    },
    "version": "1.23.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gm](#apidoc.module.gm)
1.  [function <span class="apidocSignatureSpan">gm.</span>compare (orig, compareTo, options, cb)](#apidoc.element.gm.compare)
1.  [function <span class="apidocSignatureSpan">gm.</span>subClass (options)](#apidoc.element.gm.subClass)
1.  [function <span class="apidocSignatureSpan">gm.</span>super_ ()](#apidoc.element.gm.super_)
1.  object <span class="apidocSignatureSpan">gm.</span>identifyHelpers
1.  object <span class="apidocSignatureSpan">gm.</span>utils
1.  string <span class="apidocSignatureSpan">gm.</span>version

#### [module gm.identifyHelpers](#apidoc.module.gm.identifyHelpers)
1.  [function <span class="apidocSignatureSpan">gm.identifyHelpers.</span>Colors (o, val)](#apidoc.element.gm.identifyHelpers.Colors)
1.  [function <span class="apidocSignatureSpan">gm.identifyHelpers.</span>Depth (o, val)](#apidoc.element.gm.identifyHelpers.Depth)
1.  [function <span class="apidocSignatureSpan">gm.identifyHelpers.</span>Format (o, val)](#apidoc.element.gm.identifyHelpers.Format)
1.  [function <span class="apidocSignatureSpan">gm.identifyHelpers.</span>Geometry (o, val)](#apidoc.element.gm.identifyHelpers.Geometry)
1.  [function <span class="apidocSignatureSpan">gm.identifyHelpers.</span>Orientation (o, val)](#apidoc.element.gm.identifyHelpers.Orientation)

#### [module gm.utils](#apidoc.module.gm.utils)
1.  [function <span class="apidocSignatureSpan">gm.utils.</span>argsToArray (args)](#apidoc.element.gm.utils.argsToArray)
1.  [function <span class="apidocSignatureSpan">gm.utils.</span>escape (arg)](#apidoc.element.gm.utils.escape)
1.  [function <span class="apidocSignatureSpan">gm.utils.</span>isUtil (v)](#apidoc.element.gm.utils.isUtil)
1.  [function <span class="apidocSignatureSpan">gm.utils.</span>unescape (arg)](#apidoc.element.gm.utils.unescape)



# <a name="apidoc.module.gm"></a>[module gm](#apidoc.module.gm)

#### <a name="apidoc.element.gm.compare"></a>[function <span class="apidocSignatureSpan">gm.</span>compare (orig, compareTo, options, cb)](#apidoc.element.gm.compare)
- description and source-code
```javascript
function compare(orig, compareTo, options, cb) {

  var isImageMagick = this._options && this._options.imageMagick;
  var appPath = this._options && this._options.appPath || '';
  var bin = isImageMagick
    ? appPath + 'compare'
    : appPath + 'gm'
  var args = ['-metric', 'mse', orig, compareTo]
  if (!isImageMagick) {
      args.unshift('compare');
  }
  var tolerance = 0.4;
  // outputting the diff image
  if (typeof options === 'object') {

    if (options.highlightColor && options.highlightColor.indexOf('"') < 0) {
      options.highlightColor = '"' + options.highlightColor + '"';
    }

    if (options.file) {
      if (typeof options.file !== 'string') {
        throw new TypeError('The path for the diff output is invalid');
      }
       // graphicsmagick defaults to red
      if (options.highlightColor) {
          args.push('-highlight-color');
          args.push(options.highlightColor);
      }
      if (options.highlightStyle) {
          args.push('-highlight-style')
          args.push(options.highlightStyle)
      }
      // For IM, filename is the last argument. For GM it's '-file <filename>'
      if (!isImageMagick) {
          args.push('-file');
      }
      args.push(options.file);
    }

    if (typeof options.tolerance != 'undefined') {
      if (typeof options.tolerance !== 'number') {
        throw new TypeError('The tolerance value should be a number');
      }
      tolerance = options.tolerance;
    }
  } else {
    // For ImageMagick diff file is required but we don't care about it, so null it out
    if (isImageMagick) {
      args.push('null:');
    }

    if (typeof options == 'function') {
      cb = options; // tolerance value not provided, flip the cb place
    } else {
      tolerance = options
    }
  }

  var proc = spawn(bin, args);
  var stdout = '';
  var stderr = '';
  proc.stdout.on('data',function(data) { stdout+=data });
  proc.stderr.on('data',function(data) { stderr+=data });
  proc.on('close', function (code) {
    // ImageMagick returns err code 2 if err, 0 if similar, 1 if dissimilar
    if (isImageMagick) {
      if (code === 0) {
        return cb(null, 0 <= tolerance, 0, stdout);
      }
      else if (code === 1) {
        err = null;
        stdout = stderr;
      } else {
      return cb(stderr);
      }
    } else {
      if(code !== 0) {
        return cb(stderr);
      }
    }
    // Since ImageMagick similar gives err code 0 and no stdout, there's really no matching
    // Otherwise, output format for IM is '12.00 (0.123)' and for GM it's 'Total: 0.123'
    var regex = isImageMagick ? /\((\d+\.?[\d\-\+e]*)\)/m : /Total: (\d+\.?\d*)/m;
    var match = regex.exec(stdout);
    if (!match) {
      err = new Error('Unable to parse output.\nGot ' + stdout);
      return cb(err);
    }

    var equality = parseFloat(match[1]);
    cb(null, equality <= tolerance, equality, stdout, orig, compareTo);
  });
}
```
- example usage
```shell
...
  - image output
    - **write** - writes the processed image data to the specified filename
    - **stream** - provides a 'ReadableStream' with the processed image data
    - **toBuffer** - returns the image as a 'Buffer' instead of a stream

##compare

Graphicsmagicks 'compare' command is exposed through 'gm.compare()'. This allows us to determine if two images can be considered
 "equal".

Currently 'gm.compare' only accepts file paths.

    gm.compare(path1, path2 [, options], callback)

'''js
gm.compare('/path/to/image1.jpg', '/path/to/another.png', function (err, isEqual, equality, raw, path1, path2) {
...
```

#### <a name="apidoc.element.gm.subClass"></a>[function <span class="apidocSignatureSpan">gm.</span>subClass (options)](#apidoc.element.gm.subClass)
- description and source-code
```javascript
function subClass(options) {
  function gm (source, height, color) {
    if (!(this instanceof parent)) {
      return new gm(source, height, color);
    }

    parent.call(this, source, height, color);
  }

  gm.prototype.__proto__ = parent.prototype;
  gm.prototype._options = {};
  gm.prototype.options(options);

  return gm;
}
```
- example usage
```shell
...

## Use ImageMagick instead of gm

Subclass 'gm' to enable ImageMagick

'''js
var fs = require('fs')
  , gm = require('gm').subClass({imageMagick: true});

// resize and remove EXIF profile data
gm('/path/to/my/img.jpg')
.resize(240, 240)
...
'''
...
```

#### <a name="apidoc.element.gm.super_"></a>[function <span class="apidocSignatureSpan">gm.</span>super_ ()](#apidoc.element.gm.super_)
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



# <a name="apidoc.module.gm.identifyHelpers"></a>[module gm.identifyHelpers](#apidoc.module.gm.identifyHelpers)

#### <a name="apidoc.element.gm.identifyHelpers.Colors"></a>[function <span class="apidocSignatureSpan">gm.identifyHelpers.</span>Colors (o, val)](#apidoc.element.gm.identifyHelpers.Colors)
- description and source-code
```javascript
function Colors(o, val) {
  o.color = parseInt(val, 10);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gm.identifyHelpers.Depth"></a>[function <span class="apidocSignatureSpan">gm.identifyHelpers.</span>Depth (o, val)](#apidoc.element.gm.identifyHelpers.Depth)
- description and source-code
```javascript
function Depth(o, val) {
  o.depth = parseInt(val, 10);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gm.identifyHelpers.Format"></a>[function <span class="apidocSignatureSpan">gm.identifyHelpers.</span>Format (o, val)](#apidoc.element.gm.identifyHelpers.Format)
- description and source-code
```javascript
function Format(o, val) {
  o.format = val.split(" ")[0];
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gm.identifyHelpers.Geometry"></a>[function <span class="apidocSignatureSpan">gm.identifyHelpers.</span>Geometry (o, val)](#apidoc.element.gm.identifyHelpers.Geometry)
- description and source-code
```javascript
function Geometry(o, val) {
  // We only want the size of the first frame.
  // Each frame is separated by a space.
  var split = val.split(" ").shift().split("x");
  var width = parseInt(split[0], 10);
  var height = parseInt(split[1], 10);
  if (o.size && o.size.width && o.size.height) {
    if (width > o.size.width) o.size.width = width;
    if (height > o.size.height) o.size.height = height;
  } else {
    o.size = {
      width:  width,
      height: height
    }
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gm.identifyHelpers.Orientation"></a>[function <span class="apidocSignatureSpan">gm.identifyHelpers.</span>Orientation (o, val)](#apidoc.element.gm.identifyHelpers.Orientation)
- description and source-code
```javascript
function Orientation(o, val) {
  if (val in orientations) {
    o['Profile-EXIF'] || (o['Profile-EXIF'] = {});
    o['Profile-EXIF'].Orientation = val;
    o.Orientation = orientations[val];
  } else {
    o.Orientation = val || 'Unknown';
  }
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.gm.utils"></a>[module gm.utils](#apidoc.module.gm.utils)

#### <a name="apidoc.element.gm.utils.argsToArray"></a>[function <span class="apidocSignatureSpan">gm.utils.</span>argsToArray (args)](#apidoc.element.gm.utils.argsToArray)
- description and source-code
```javascript
argsToArray = function (args) {
  var arr = [];

  for (var i = 0; i <= arguments.length; i++) {
    if ('undefined' != typeof arguments[i])
      arr.push(arguments[i]);
  }

  return arr;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gm.utils.escape"></a>[function <span class="apidocSignatureSpan">gm.utils.</span>escape (arg)](#apidoc.element.gm.utils.escape)
- description and source-code
```javascript
function escape(arg) {
  return '"' + String(arg).trim().replace(/"/g, '\\"') + '"';
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gm.utils.isUtil"></a>[function <span class="apidocSignatureSpan">gm.utils.</span>isUtil (v)](#apidoc.element.gm.utils.isUtil)
- description and source-code
```javascript
isUtil = function (v) {
	var ty = 'object';
	switch (Object.prototype.toString.call(v)) {
	case '[object String]':
		ty = 'String';
		break;
	case '[object Array]':
		ty = 'Array';
		break;
	case '[object Boolean]':
		ty = 'Boolean';
		break;
	}
	return ty;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gm.utils.unescape"></a>[function <span class="apidocSignatureSpan">gm.utils.</span>unescape (arg)](#apidoc.element.gm.utils.unescape)
- description and source-code
```javascript
function escape(arg) {
    return String(arg).trim().replace(/"/g, "");
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
