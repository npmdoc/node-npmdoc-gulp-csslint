# api documentation for  [gulp-csslint (v1.0.0)](https://github.com/lazd/gulp-csslint#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-csslint.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-csslint) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-csslint.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-csslint)
#### CSSLint plugin for gulp

[![NPM](https://nodei.co/npm/gulp-csslint.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/gulp-csslint)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-csslint/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-csslint/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-csslint/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-csslint/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Larry Davis"
    },
    "bugs": {
        "url": "https://github.com/lazd/gulp-csslint/issues"
    },
    "dependencies": {
        "csslint": "^1.0.2",
        "gulp-util": "^3.0.7",
        "rcloader": "^0.2.1",
        "through2": "^2.0.1"
    },
    "description": "CSSLint plugin for gulp",
    "devDependencies": {
        "coveralls": "^2.11.12",
        "csslint-stylish": "0.0.4",
        "eslint": "^3.2.2",
        "eslint-config-semistandard": "^7.0.0-beta.0",
        "eslint-config-standard": "^6.0.0-beta.2",
        "eslint-plugin-promise": "^2.0.1",
        "eslint-plugin-standard": "^2.0.0",
        "mocha": "^3.0.2",
        "node-version-check": "^2.1.0",
        "nyc": "^7.1.0",
        "rimraf": "^2.5.4",
        "should": "^11.0.0",
        "sinon": "^1.17.5"
    },
    "directories": {},
    "dist": {
        "shasum": "d95a56f7719466147fa9a07302fdba1690391523",
        "tarball": "https://registry.npmjs.org/gulp-csslint/-/gulp-csslint-1.0.0.tgz"
    },
    "engines": {
        "node": ">=0.10"
    },
    "files": [
        "index.js"
    ],
    "gitHead": "371a4ce3825be7cc92e0f2dc789afe48bcfce091",
    "homepage": "https://github.com/lazd/gulp-csslint#readme",
    "keywords": [
        "csslint",
        "gulpplugin"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "lazd"
        }
    ],
    "name": "gulp-csslint",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git://github.com/lazd/gulp-csslint.git"
    },
    "scripts": {
        "clean": "rimraf coverage/ .nyc_output/",
        "cover": "nyc mocha",
        "lint": "node-version-gte-4 && eslint index.js test/main.js || node-version-lt-4",
        "postcover": "nyc report --reporter lcov",
        "precover": "npm run lint && npm run clean",
        "pretest": "npm run lint",
        "test": "mocha"
    },
    "version": "1.0.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp-csslint](#apidoc.module.gulp-csslint)
1.  [function <span class="apidocSignatureSpan"></span>gulp-csslint (options)](#apidoc.element.gulp-csslint.gulp-csslint)
1.  [function <span class="apidocSignatureSpan">gulp-csslint.</span>addFormatter (formatter)](#apidoc.element.gulp-csslint.addFormatter)
1.  [function <span class="apidocSignatureSpan">gulp-csslint.</span>addRule (rule)](#apidoc.element.gulp-csslint.addRule)
1.  [function <span class="apidocSignatureSpan">gulp-csslint.</span>failFormatter ()](#apidoc.element.gulp-csslint.failFormatter)
1.  [function <span class="apidocSignatureSpan">gulp-csslint.</span>formatter (customFormatter, options)](#apidoc.element.gulp-csslint.formatter)
1.  [function <span class="apidocSignatureSpan">gulp-csslint.</span>toString ()](#apidoc.element.gulp-csslint.toString)



# <a name="apidoc.module.gulp-csslint"></a>[module gulp-csslint](#apidoc.module.gulp-csslint)

#### <a name="apidoc.element.gulp-csslint.gulp-csslint"></a>[function <span class="apidocSignatureSpan"></span>gulp-csslint (options)](#apidoc.element.gulp-csslint.gulp-csslint)
- description and source-code
```javascript
gulp-csslint = function (options) {
  options = options || {};
  var rcLoader = new RcLoader('.csslintrc', options, { loader: 'async' });
  return through.obj(function(file, enc, cb) {
    if (file.isNull()) return cb(null, file); // pass along
    if (file.isStream()) return cb(new gutil.PluginError('gulp-csslint: Streaming not supported'), file);

    var ruleset = {};
    // Build a list of all available rules
    csslint.getRules().forEach(function(rule) {
      ruleset[rule.id] = 1;
    });

    var content = file.contents.toString(enc);

    if (!content) return cb(null, file); // pass along

    rcLoader.for(file.path, function(err, opts) {
      if (err) return cb(err);

      for (var rule in opts) {
        if (!opts[rule]) {
          // Remove rules that are turned off
          delete ruleset[rule];
        }
        else {
          ruleset[rule] = opts[rule];
        }
      }

      var report = csslint.verify(content, ruleset);

      // send status down-stream
      file.csslint = { report: report, success: !report.messages.length };

      cb(null, file);
    });
  });
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gulp-csslint.addFormatter"></a>[function <span class="apidocSignatureSpan">gulp-csslint.</span>addFormatter (formatter)](#apidoc.element.gulp-csslint.addFormatter)
- description and source-code
```javascript
addFormatter = function (formatter) {
  formatter = typeof formatter === 'string' ? require(formatter) : formatter;
  validateFormatter(formatter);

  csslint.addFormatter(formatter);
}
```
- example usage
```shell
...
### Custom formatters

Custom formatters can be provided by first adding a valid CSSLint-formatter, such as 'csslint-stylish', then using it:

'''js
var csslint = require('gulp-csslint');

csslint.addFormatter('csslint-stylish');

gulp.task('lint', function() {
  gulp.src('lib/*.css')
    .pipe(csslint())
    .pipe(csslint.formatter('stylish'))
});
'''
...
```

#### <a name="apidoc.element.gulp-csslint.addRule"></a>[function <span class="apidocSignatureSpan">gulp-csslint.</span>addRule (rule)](#apidoc.element.gulp-csslint.addRule)
- description and source-code
```javascript
addRule = function (rule) {
  if (typeof rule !== 'object') {
    throw new Error('Invalid rule: rules need to be objects.');
  }
  csslint.addRule(rule);
}
```
- example usage
```shell
...
});
'''

This functionality is only available when not using a custom formatting function.

## Custom rules

Use the 'csslint.addRule(rule)' method to define custom rules that run in addition to the rules defined in the csslintrc file. See
 [Working with Rules](https://github.com/CSSLint/csslint/wiki/Working-with-Rules) for details.

'''js
var csslint = require('gulp-csslint');

csslint.addRule({
  // rule information
});
...
```

#### <a name="apidoc.element.gulp-csslint.failFormatter"></a>[function <span class="apidocSignatureSpan">gulp-csslint.</span>failFormatter ()](#apidoc.element.gulp-csslint.failFormatter)
- description and source-code
```javascript
failFormatter = function () {
  return through.obj(function(file, enc, cb) {
    // Nothing to report or no errors
    if (!file.csslint || file.csslint.success) {
      return cb(null, file);
    }

    return cb(new gutil.PluginError('gulp-csslint', 'CSSLint failed for ' + file.relative), file);
  });
}
```
- example usage
```shell
...
  .pipe(csslint())
  .pipe(csslint.formatter())
});
'''

## Fail on errors

Pipe the file stream to 'csslint.failFormatter()' to fail on errors.

'''js
var csslint = require('gulp-csslint');

gulp.task('lint', function() {
gulp.src('lib/*.css')
  .pipe(csslint())
...
```

#### <a name="apidoc.element.gulp-csslint.formatter"></a>[function <span class="apidocSignatureSpan">gulp-csslint.</span>formatter (customFormatter, options)](#apidoc.element.gulp-csslint.formatter)
- description and source-code
```javascript
formatter = function (customFormatter, options) {
  var formatter = csslint.getFormatter('text');
  var builtInFormatter = true;
  var output;

  options = options || {};

  var logger = options.logger || process.stdout.write.bind(process.stdout);
  if (customFormatter) {
    if (typeof customFormatter === 'function') {
      formatter = customFormatter;
      builtInFormatter = false;
    }
    else if (typeof customFormatter === 'string') {
      if (customFormatter === 'fail') {
        return cssLintPlugin.failFormatter();
      }

      formatter = csslint.getFormatter(customFormatter);

      if (typeof formatter === 'undefined') {
        throw new Error('Invalid reporter: ' + customFormatter);
      }
    }
    else if (typeof customFormatter === 'object') {
      validateFormatter(customFormatter);
      formatter = customFormatter;
    }
    else {
      throw new Error('Invalid custom formatter passed, please pass 'null' or 'undefined' if you want to pass options while using
 default formatter.');
    }
  }

  if (builtInFormatter) {
    output = [formatter.startFormat()];
  }

  return through.obj(
    function(file, enc, cb) {
      // Only report if CSSLint was ran and errors were found
      if (file.csslint && !file.csslint.success) {
        if (builtInFormatter) {
          output.push(formatter.formatResults(file.csslint.report, file.path, options));
        }
        else {
          formatter(file.csslint.report, file.path, options);
        }
      }

      return cb(null, file);
    },
    function(cb) {
      if (builtInFormatter) {
        output.push(formatter.endFormat());

        output
          .filter(function(str) {
            return str;
          })
          .forEach(logger);
      }

      return cb();
    }
  ).resume(); // Force flow-mode https://nodejs.org/docs/latest/api/stream.html#stream_event_end
}
```
- example usage
```shell
...

'''js
var csslint = require('gulp-csslint');

gulp.task('css', function() {
  gulp.src('client/css/*.css')
    .pipe(csslint())
    .pipe(csslint.formatter());
});
'''

## API

### csslint(ruleConfiguration)
...
```

#### <a name="apidoc.element.gulp-csslint.toString"></a>[function <span class="apidocSignatureSpan">gulp-csslint.</span>toString ()](#apidoc.element.gulp-csslint.toString)
- description and source-code
```javascript
toString = function () {
    return toString;
}
```
- example usage
```shell
...

    var ruleset = {};
    // Build a list of all available rules
    csslint.getRules().forEach(function(rule) {
ruleset[rule.id] = 1;
    });

    var content = file.contents.toString(enc);

    if (!content) return cb(null, file); // pass along

    rcLoader.for(file.path, function(err, opts) {
if (err) return cb(err);

for (var rule in opts) {
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
