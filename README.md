# api documentation for  [babel-eslint (v7.2.2)](https://github.com/babel/babel-eslint)  [![npm package](https://img.shields.io/npm/v/npmdoc-babel-eslint.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-babel-eslint) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-babel-eslint.svg)](https://travis-ci.org/npmdoc/node-npmdoc-babel-eslint)
#### Custom parser for ESLint

[![NPM](https://nodei.co/npm/babel-eslint.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/babel-eslint)

[![apidoc](https://npmdoc.github.io/node-npmdoc-babel-eslint/build/screenCapture.buildCi.browser.apidoc.html.png)](https://npmdoc.github.io/node-npmdoc-babel-eslint/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-babel-eslint/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-babel-eslint/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Sebastian McKenzie"
    },
    "bugs": {
        "url": "https://github.com/babel/babel-eslint/issues"
    },
    "dependencies": {
        "babel-code-frame": "^6.22.0",
        "babel-traverse": "^6.23.1",
        "babel-types": "^6.23.0",
        "babylon": "^6.16.1"
    },
    "description": "Custom parser for ESLint",
    "devDependencies": {
        "babel-eslint": "^7.0.0",
        "dedent": "^0.7.0",
        "eslint": "^3.18.0",
        "eslint-config-babel": "^6.0.0",
        "eslint-plugin-flowtype": "^2.30.3",
        "espree": "^3.4.0",
        "mocha": "^3.0.0"
    },
    "directories": {},
    "dist": {
        "shasum": "0da2cbe6554fd0fb069f19674f2db2f9c59270ff",
        "tarball": "https://registry.npmjs.org/babel-eslint/-/babel-eslint-7.2.2.tgz"
    },
    "engines": {
        "node": ">=4"
    },
    "files": [
        "index.js",
        "babylon-to-espree"
    ],
    "gitHead": "f59d2009652e14acf1231a1268a8324cf046514e",
    "homepage": "https://github.com/babel/babel-eslint",
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "danez"
        },
        {
            "name": "hzoo"
        },
        {
            "name": "sebmck"
        }
    ],
    "name": "babel-eslint",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git+https://github.com/babel/babel-eslint.git"
    },
    "scripts": {
        "changelog": "git log 'git describe --tags --abbrev=0'..HEAD --pretty=format:' * %s (%an)' | grep -v 'Merge pull request'",
        "fix": "eslint index.js babylon-to-espree test --fix",
        "lint": "eslint index.js babylon-to-espree test",
        "preversion": "npm test",
        "test": "npm run lint && npm run test-only",
        "test-only": "mocha"
    },
    "version": "7.2.2"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module babel-eslint](#apidoc.module.babel-eslint)
1.  [function <span class="apidocSignatureSpan">babel-eslint.</span>parse (code, options)](#apidoc.element.babel-eslint.parse)
1.  [function <span class="apidocSignatureSpan">babel-eslint.</span>parseNoPatch (code, options)](#apidoc.element.babel-eslint.parseNoPatch)



# <a name="apidoc.module.babel-eslint"></a>[module babel-eslint](#apidoc.module.babel-eslint)

#### <a name="apidoc.element.babel-eslint.parse"></a>[function <span class="apidocSignatureSpan">babel-eslint.</span>parse (code, options)](#apidoc.element.babel-eslint.parse)
- description and source-code
```javascript
parse = function (code, options) {
  options = options || {};
  eslintOptions.ecmaVersion = options.ecmaVersion = options.ecmaVersion || 6;
  eslintOptions.sourceType = options.sourceType = options.sourceType || "module";
  eslintOptions.allowImportExportEverywhere = options.allowImportExportEverywhere = options.allowImportExportEverywhere || false
;
  if (options.sourceType === "module") {
    eslintOptions.globalReturn = false;
  } else {
    delete eslintOptions.globalReturn;
  }

  if (!hasPatched) {
    hasPatched = true;
    try {
      monkeypatch(getModules());
    } catch (err) {
      console.error(err.stack);
      process.exit(1);
    }
  }

  return exports.parseNoPatch(code, options);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.babel-eslint.parseNoPatch"></a>[function <span class="apidocSignatureSpan">babel-eslint.</span>parseNoPatch (code, options)](#apidoc.element.babel-eslint.parseNoPatch)
- description and source-code
```javascript
parseNoPatch = function (code, options) {
  var opts = {
    codeFrame: options.hasOwnProperty("codeFrame") ? options.codeFrame : true,
    sourceType: options.sourceType,
    allowImportExportEverywhere: options.allowImportExportEverywhere, // consistent with espree
    allowReturnOutsideFunction: true,
    allowSuperOutsideMethod: true,
    plugins: [
      "flow",
      "jsx",
      "asyncFunctions",
      "asyncGenerators",
      "classConstructorCall",
      "classProperties",
      "decorators",
      "doExpressions",
      "exponentiationOperator",
      "exportExtensions",
      "functionBind",
      "functionSent",
      "objectRestSpread",
      "trailingFunctionCommas",
      "dynamicImport"
    ]
  };

  var ast;
  try {
    ast = parse(code, opts);
  } catch (err) {
    if (err instanceof SyntaxError) {

      err.lineNumber = err.loc.line;
      err.column = err.loc.column;

      if (opts.codeFrame) {
        err.lineNumber = err.loc.line;
        err.column = err.loc.column + 1;

        // remove trailing "(LINE:COLUMN)" acorn message and add in esprima syntax error message start
        err.message = "Line " + err.lineNumber + ": " + err.message.replace(/ \((\d+):(\d+)\)$/, "") +
        // add codeframe
        "\n\n" +
        codeFrame(code, err.lineNumber, err.column, { highlightCode: true });
      }
    }

    throw err;
  }

  babylonToEspree(ast, traverse, tt, code);

  return ast;
}
```
- example usage
```shell
...
    monkeypatch(getModules());
  } catch (err) {
    console.error(err.stack);
    process.exit(1);
  }
}

return exports.parseNoPatch(code, options);
};

exports.parseNoPatch = function (code, options) {
var opts = {
  codeFrame: options.hasOwnProperty("codeFrame") ? options.codeFrame : true,
  sourceType: options.sourceType,
  allowImportExportEverywhere: options.allowImportExportEverywhere, // consistent with espree
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
