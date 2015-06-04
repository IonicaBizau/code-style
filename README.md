:book: Ionică Bizău's JavaScript Code Style :heart:
===================================================
**OK.** Now you want to contribute to one of my projects I maintain. :heart:
That's awesome. The content below is for you. :sunglasses:

[Open issues](/code-style/issues) with any questions, ideas, fixes etc. :innocent:

# Contents
 - [Variable declarations](#variable-declarations-pencil)
   - [Variables](#variables-speech_balloon)
   - [Constants](#constants-triangular_flag_on_post)
   - [Globals](#globals-earth_africa)
 - [Semicolons](#semicolons-pencil2)
 - [Method and property definitions](#method-and-property-definitions-paperclip)
 - [Deleting properties](#deleting-properties-x)
 - [`eval()`](#eval)
 - [Iterating objects and arrays](#iterating-objects-and-arrays)
 - [Multiline strings](#multiline-strings-guitar)
 - [Modifying prototypes of built-in objects](#modifying-prototypes-of-built-in-objects-shit)
 - [Naming things](#naming-things-thought_balloon)
 - [Curly braces](#curly-braces-curly_loop)
 - [Array and Object Initializers](#array-and-object-initializers-file_folder)
 - [Commas](#commas)
 - [Blank lines](#blank-lines)
 - [Binary and Ternary operators](#binary-and-ternary-operators)
 - [Quotes](#quotes-speech_balloon)
 - [Comments](#comments-notes)
 - [Project naming](#project-naming)

## Variable declarations :pencil:
### Variables :speech_balloon:
Always with `var`.

```js
// One declaration
var foo = 1;

// Multiple declarations
var foo = 1
  , bar = "Hello World"
  , anotherOne = [{ foo: "bar" }]
  ;
```

### Constants :triangular_flag_on_post:
On the **client**, always with `var`. On the **server** with `const`. The
constant names are written with UPPERCASE letters.

  - On the client

  ```js
  // Constants
  var PI = Math.PI
    , MY_CONSTANT = 42
    ;
  ```
  - Node.JS

  ```js
  // Constants
  const PI = Math.PI
      , MY_CONSTANT = 42
      ;
  ```

### Globals :earth_africa:
I define globals using `window.MyGlobal` (on the client) and `global.MyGlobal`
(on the server).

  - Client
  ```js
  (function (window) {
      var MyLibrary = ...;
      window.MyLibrary = MyLibrary;
  })(window);

  ```
  - Node.JS

  ```js
  // Dependencies
  var Fs = require("fs")
    , Http = require("http")
    , Util = require("util")
    ;

  // Constants
  const FOO = 42;

  // Define some global
  global.someGlobal = Math.PI;

  // Constructor
  var MyModule = module.exports = {};
  MyModul.method = ...;
  ```

## Semicolons :pencil2:
Almost always. The only exception is the function declaration with
`function <name> () {}`.

```js
var foo = 1;
function bar (x) {
    this.method = function (m) {
        console.log(m);
    };
    return { y: x };
}
```

## Method and property definitions :paperclip:
See the examples below.

```js
function Person (name, age) {
    this.name = name;
    this.age = age;
    this.doSomething = function () {
        ...
    };
}
Person.prototype.getName = function () {
    return this.name;
};
```

## Deleting properties :x:
I nullify the properties when that's fine:

```js
var foo = {
    bar: 42
};
foo.bar = null;
```

However, I use the `delete` keyword when I want to delete them.

```js
delete foo.bar;
```

## `eval()`
`eval` is evil. :rage: Do not use it. However I use it in some test files and in places
where I have to execute the JavaScript code provided by the user.

For converting strings to JSON, use `JSON.parse(strObj)`.

## Iterating objects and arrays

For arrays, most of times, I use the `forEach` function:

```js
arr.forEach(function (c) {
    // do something
});
```

However, using `for` loops is fine too:

```js
for (var i = 0; i < arr.length; ++i) {
    for (var ii = 0; ii < arr[i].length; ++ii) {
        ...
    }
    ...
}
```

For objects, I use the following style:

```js
Object.keys(obj).forEach(functions (k) {
    var cValue = obj[k];
    // do something
});
```

## Multiline strings :guitar:
Use `+` operator to concatenate multiline strings:

```js
var multiLineStr = "Lorem ipsum dolor sit amet, consectetur adipisicing elit, "
                 + "sed do eiusmod tempor incididunt ut labore et dolore magna "
                 + "aliqua. Ut enim ad minim veniam, quis nostrud exercitation "
                 + "ullamco laboris nisi ut aliquip ex ea commodo consequat"
          + "\n" + "New line paragrph..."
          + "\n" + "New line again...";
```

## Modifying prototypes of built-in objects :shit:
Just don't, unless that's the scope of the library.

## Naming things :thought_balloon:
See the examples below.

```js
// Node.JS require
var SomeLibrary = require("somelibrary");

// Defining the library name
/// Node.JS
var MyAwesomeModule = module.exports = ...;
/// Client
(function (window) {
    var MyAwesomeModule = ...;
    window.MyAwesomeModule = MyAwesomeModule;
})(window);

// Constants
/// Node.JS
const SOME_CONSTANT = 42;
/// Client
var SOME_CONSTANT = 42;

// Local variables
var x = 1
  , twoWords = "Hello World"
  ;

// Functions
function fooBar () {...}
obj.methodA = function () {...}

// Object fields
var obj = {
    full_name: "Johnny B."
  , age: 19
};
```

## Curly braces :curly_loop:
Open the curly brace at the end of the line. Always put the instructions between
curly braces, even there is only one instruction.

```js
if (expr) {
    instr;
} else {
    instr2;
    instr3;
}
```

## Array and Object Initializers :file_folder:
See examples.

```js
// Arrays
var arr = [1, 2, 3, 4];

var lotOfElms = [
    1, 2, 3, 4, 5, 6, 7
  , 8, 9, 10, 11, 12, 13
  , 14, 15, 16, 17, 18
];

var bigElms = [
    "Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod."
  , "Tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim."
  , "Veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea."
  , "Commodo consequat. Duis aute irure dolor in reprehenderit in voluptate"
];

// Objects
var obj = { a: 1 };

var obj1 = {
    full_name: "Johnny B."
  , age: 19
};
```
## Commas
Put commas at the beginning of the line, not at the end.

```js
var x = 1
  , y = 2
  ;

const C_1 = 42
    , C_2 = -42
    ;

var obj = {
    x: 1
  , y: 2
};
```

## Blank lines
Group the instructions inserting some blank lines where it's needed.

```js
foo(x);
bar(x);

foo(y);
bar(y);
```

## Binary and Ternary operators
See examples.

```js
var foo = someObj
    .method()
    .method2()
    .method3()
    ;

var a = cond ? v1 : v2;

var b = long_condition_here
        ? v1 : v2
        ;

var c = another_long_condition_here
        ? with_some_long_value
        : or_another_some_long_value
        ;
```

## Quotes :speech_balloon:
Double quotes, with some exceptions when single quotes are used.

```js
var foo = "\"Hello\", he said.";
var jQuerySelector = "div.myClass[data-foo='bar']";
```

## Comments :notes:
Put relevant comments. The comments start with uppercase letter.

```js
// Dependencies
var Lib1 = require("lib1")
  , Lib2 = require("lib2")
  ;

// Constants
const FOURTY_TWO = 42;
```

Use JSDoc comments for functions and methods.

```js
/**
* sum
* Calculates the sum of two numbers.
*
* @name sum
* @function
* @param {Number} a The first number,
* @param {Number} b The second number.
* @return {Number} The sum of the two numbers.
*/
function sum (a, b) {
  return a + b;
};
```

I use the [`blah` tool](https://github.com/IonicaBizau/node-blah) to generate documentation.

```sh
$ npm install -g blah
$ blah readme
$ blah docs some-file.js
```

## Project naming
I try to use short and creative names for my projects. However, there are some things
to make a distinction between the projects:

 - For Node.JS I mostly use `node-<lib-name>`
 - For jQuery plugins I use `jQuery-<name>` or `jQuery.<name>`
 - In other cases I just use the lib name without any preffix

## Project licenses
Most of my projects are licensed under [*The KINDLY License*](https://github.com/IonicaBizau/kindly-license).

## How do I start writing a project?

### Node.JS Modules
Everything starts with a `git init`, to initialize the git repository. Then I 
create the folder structure:

```sh
$ mkdir lib test example bin
```

Then I start writing an example (`vim example/index.js`):

```js
// Dependencies
var LibName = require("../lib");

// Do something
LibName.something(function (err, data) {
    console.log(err || data);
});
```

The next thing is to write the `lib/index.js` file:

```js
// Dependencies
var SomeDependency = require("...");

// Constants
const FOO = 42;

// Configurations
SomeDependency.defaults.something = 24;

/**
 * LibName
 * Creates a new instance of `LibName`.
 *
 * @name Sum
 * @function
 * @return {LibName} The `LibName` instance.
 */
function LibName () {
    // ...
}

/**
 * something
 * Does something.
 *
 * @name something
 * @function
 * @return {Function} The callback function.
 */
LibName.prototype.something = function (callback) {
    // do something
    callback(null, {...});
};

module.exports = new LibName();
```

If I have time, I probably write some tests in `test/index.js` as well.
If it makes sense I will create a global executable (`bin/libname`):

```js
#!/usr/bin/env nodejs

// Dependencies
var LibName = require("../lib")
  , Logger = require("bug-killer")
  , CLP = require("clp")
  , Package = require("../package")
  ;

// Configurations
Logger.config.displayDate = false;
Logger.config.logLevel = 4;

// Parse the command line arguments
var someOpt = new CLP.Option(["s", "something"], "Does something.", "value", "some default value")
  , verboseOpt = new CLP.Option(["verbose"], "Enables the verbose mode")
  , parser = new CLP({
        name: "LibName"
      , version: Package.version
      , exe: Package.name
      , examples: [
            "libname # Default behavior"
          , "libname -s 'Alice'"
          , "libname --verbose -s 'Bob'"
        ]
      , docs_url: "https://github.com/IonicaBizau/node-libname"
      , process: true
    }, [
        someOpt, verboseOpt
    ])
  ;

// Enable verbose mode
if (verboseOpt.is_provided) {
    Logger.log("Verbose mode enabled.", "info");
}

// Do something
LibName.foo(someOpt.value, function (err, data) {
    if (err) { return Logger.log(err, "error"); }
    Logger.log(data, "info");
});
```

The next step is creating the `package.json` file (`npm init`).

Creating documentation is also important:

```sh
$ kindly-license
$ blah --gitignore -readme --contributing
# or `blah -g -r -c`
```

Then I create the GitHub repository (`node-<libname>`) doing:

```sh
$ git remote add origin <git-url>
$ git push --all
$ npm publish
```

### jQuery Plugins

todo
