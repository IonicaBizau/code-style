:book: :bookmark_tabs: Ionică Bizău's JavaScript Code Style :books: :heart:
===================================================
**OK.** Now you want to contribute to one of my projects I maintain.

:heart: That's awesome. :green_heart: The content below is for you. :sunglasses:

# Contents

 - [Variable declarations](#variable-declarations)
   - [Variables](#variables)
   - [Constants](#constants)
   - [Globals](#globals)
 - [Semicolons](#semicolons)
 - [Method and property definitions](#method-and-property-definitions)
 - [Deleting properties](#deleting-properties)
 - [`eval()`](#eval)
 - [`for` loops](#for-loops)
 - [Multiline strings](#multiline-strings)
 - [Modifying prototypes of built-in objects](#modifying-prototypes-of-built-in-objects)
 - [Naming things](#naming-things)
 - [Curly braces](#curly-braces)
 - [Array and Object Initializers](#array-and-object-initializers)
 - [Commas](#commas)
 - [Blank lines](#blank-lines)
 - [Binary and Ternary operators](#binary-and-ternary-operators)
 - [Quotes](#quotes)
 - [Comments](#comments)

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
I use the `delete` keyword.

```js
var foo = {
    bar: 42
};
delete foo.bar;
```

## `eval()`
`eval` is evil. :rage: Do not use it. However I use it in some test files and in places
where I have to execute the JavaScript code provided by the user.

For converting strings to JSON, use `JSON.parse(strObj)`.

## `for` loops
Use `for (var k in obj) {...}` for objects and
`for (var i = 0; i < arr.length; ++i) {...}` for arrays.

```js
for (var k in obj) {
    ...
}

for (var i = 0; i < arr.length; ++i) {
    for (var ii = 0; ii < arr[i].length; ++ii) {
        ...
    }
    ...
}
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
