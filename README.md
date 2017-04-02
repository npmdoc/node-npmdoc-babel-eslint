# api documentation for  [babel-eslint (v7.2.1)](https://github.com/babel/babel-eslint)  [![npm package](https://img.shields.io/npm/v/npmdoc-babel-eslint.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-babel-eslint) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-babel-eslint.svg)](https://travis-ci.org/npmdoc/node-npmdoc-babel-eslint)
#### Custom parser for ESLint

[![NPM](https://nodei.co/npm/babel-eslint.png?downloads=true)](https://www.npmjs.com/package/babel-eslint)

[![apidoc](https://npmdoc.github.io/node-npmdoc-babel-eslint/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-babel-eslint_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-babel-eslint/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-babel-eslint/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "author": {
        "name": "Sebastian McKenzie",
        "email": "sebmck@gmail.com"
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
        "eslint": "^3.18.0",
        "eslint-config-babel": "^6.0.0",
        "eslint-plugin-flowtype": "^2.30.3",
        "espree": "^3.4.0",
        "mocha": "^3.0.0"
    },
    "directories": {},
    "dist": {
        "shasum": "079422eb73ba811e3ca0865ce87af29327f8c52f",
        "tarball": "https://registry.npmjs.org/babel-eslint/-/babel-eslint-7.2.1.tgz"
    },
    "engines": {
        "node": ">=4"
    },
    "files": [
        "index.js",
        "babylon-to-espree"
    ],
    "gitHead": "3cda62ee066c741b766526155dcdb98db1a2a2d5",
    "homepage": "https://github.com/babel/babel-eslint",
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "danez",
            "email": "daniel@tschinder.de"
        },
        {
            "name": "hzoo",
            "email": "hi@henryzoo.com"
        },
        {
            "name": "sebmck",
            "email": "sebmck@gmail.com"
        }
    ],
    "name": "babel-eslint",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
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
    "version": "7.2.1"
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

  try {
    monkeypatch();
  } catch (err) {
    console.error(err.stack);
    process.exit(1);
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

  // remove EOF token, eslint doesn't use this for anything and it interferes with some rules
  // see https://github.com/babel/babel-eslint/issues/2 for more info
  // todo: find a more elegant way to do this
  ast.tokens.pop();

  // convert tokens
  ast.tokens = babylonToEspree.toTokens(ast.tokens, tt, code);

  // add comments
  babylonToEspree.convertComments(ast.comments);

  // transform esprima and acorn divergent nodes
  babylonToEspree.toAST(ast, traverse, code);

  // ast.program.tokens = ast.tokens;
  // ast.program.comments = ast.comments;
  // ast = ast.program;

  // remove File
  ast.type = "Program";
  ast.sourceType = ast.program.sourceType;
  ast.directives = ast.program.directives;
  ast.body = ast.program.body;
  delete ast.program;
  delete ast._paths;

  babylonToEspree.attachComments(ast, ast.comments, ast.tokens);

  return ast;
}
```
- example usage
```shell
...
try {
  monkeypatch();
} catch (err) {
  console.error(err.stack);
  process.exit(1);
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
