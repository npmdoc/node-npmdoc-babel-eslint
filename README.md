# npmdoc-babel-eslint

#### api documentation for  [babel-eslint (v7.2.2)](https://github.com/babel/babel-eslint)  [![npm package](https://img.shields.io/npm/v/npmdoc-babel-eslint.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-babel-eslint) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-babel-eslint.svg)](https://travis-ci.org/npmdoc/node-npmdoc-babel-eslint)

#### Custom parser for ESLint

[![NPM](https://nodei.co/npm/babel-eslint.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/babel-eslint)

- [https://npmdoc.github.io/node-npmdoc-babel-eslint/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-babel-eslint/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-babel-eslint/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-babel-eslint/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-babel-eslint/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-babel-eslint/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "name": "babel-eslint",
    "version": "7.2.2",
    "description": "Custom parser for ESLint",
    "main": "index.js",
    "files": [
        "index.js",
        "babylon-to-espree"
    ],
    "repository": {
        "type": "git",
        "url": "https://github.com/babel/babel-eslint.git"
    },
    "dependencies": {
        "babel-code-frame": "^6.22.0",
        "babel-traverse": "^6.23.1",
        "babel-types": "^6.23.0",
        "babylon": "^6.16.1"
    },
    "scripts": {
        "test": "npm run lint && npm run test-only",
        "test-only": "mocha",
        "lint": "eslint index.js babylon-to-espree test",
        "fix": "eslint index.js babylon-to-espree test --fix",
        "preversion": "npm test",
        "changelog": "git log 'git describe --tags --abbrev=0'..HEAD --pretty=format:' * %s (%an)' | grep -v 'Merge pull request'"
    },
    "author": "Sebastian McKenzie <sebmck@gmail.com>",
    "license": "MIT",
    "engines": {
        "node": ">=4"
    },
    "bugs": {
        "url": "https://github.com/babel/babel-eslint/issues"
    },
    "homepage": "https://github.com/babel/babel-eslint",
    "devDependencies": {
        "babel-eslint": "^7.0.0",
        "dedent": "^0.7.0",
        "eslint": "^3.18.0",
        "eslint-config-babel": "^6.0.0",
        "eslint-plugin-flowtype": "^2.30.3",
        "espree": "^3.4.0",
        "mocha": "^3.0.0"
    }
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
