# npmdoc-gulp-csslint

#### api documentation for  gulp-csslint (v1.0.0)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-csslint.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-csslint) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-csslint.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-csslint)

#### CSSLint plugin for gulp

[![NPM](https://nodei.co/npm/gulp-csslint.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/gulp-csslint)

- [https://npmdoc.github.io/node-npmdoc-gulp-csslint/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-gulp-csslint/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-csslint/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-csslint/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-csslint/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-csslint/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "name": "gulp-csslint",
    "version": "1.0.0",
    "description": "CSSLint plugin for gulp",
    "main": "index.js",
    "files": [
        "index.js"
    ],
    "dependencies": {
        "csslint": "^1.0.2",
        "gulp-util": "^3.0.7",
        "rcloader": "^0.2.1",
        "through2": "^2.0.1"
    },
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
    "scripts": {
        "clean": "rimraf coverage/ .nyc_output/",
        "cover": "nyc mocha",
        "postcover": "nyc report --reporter lcov",
        "lint": "node-version-gte-4 && eslint index.js test/main.js || node-version-lt-4",
        "precover": "npm run lint && npm run clean",
        "pretest": "npm run lint",
        "test": "mocha"
    },
    "repository": {
        "type": "git",
        "url": "git://github.com/lazd/gulp-csslint.git"
    },
    "keywords": [
        "csslint",
        "gulpplugin"
    ],
    "author": "Larry Davis <lazdnet@gmail.com>",
    "license": "MIT",
    "bugs": {
        "url": "https://github.com/lazd/gulp-csslint/issues"
    },
    "engines": {
        "node": ">=0.10"
    }
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
