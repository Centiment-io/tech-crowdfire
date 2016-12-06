## JavaScript

### Language

#### Semicolon

Don't use them except in four situations:

- for (;;) loops. They're actually required.
- null loops like: while (something) ; (But you'd better have a good reason for doing that.)
- case "foo": doSomething(); break
- In front of a leading ( or [ at the start of the line. This prevents the expression from being interpreted as a function call or property access, respectively.

Some examples of good semicolon usage:
```javascript
;(x || y).doSomething()
;[a, b, c].forEach(doSomething)
for (var i = 0; i < 10; i ++) {
  switch (state) {
    case "begin": start(); continue
    case "end": finish(); break
    default: throw new Error("unknown state")
  }
  end()
}
```
Note that starting lines with - and + also should be prefixed with a semicolon, but this is much less common.

#### Variable declarations

  - Give descriptive names
    - Do not use similar names or synonyms for different variables unless following a convention
    - `for...in` iterators should use descriptive names
    - `for` iterators should use single character names
    - Use combination of plural for array and singular for each item in the array
  - Use camelCase
  - Avoid using numbered variables (e.g. i1, i2, i3)
  - Use `var` for every variable declaration
```javascript
// Right

var async   = require('async')
var request = require('request')

// Wrong

var async = require('async'),
  request = require('request')
```

#### Scope

  - No implicit or single statement scopes
  - All scopes must be wrapped in `{}`

```javascript
// Right

if (condition) {
  return;
}

// Wrong

if (condition) return;

if (condition)
  return;
```

#### For loops

  - Iterator variable should be declared inside the `for` parentheses, unless already defined
  - Use `for` with arrays, `for...in` for objects (and always check `hasOwnProperty()`)
  - Always `i += 1`, never `i++` or `++i`

```javascript
// Right

var name = 'john'

for (var i = 0; i < name.length; i += 1) {
  console.log(name[i])
}

// Wrong

var position
var name = 'john'

for (position = 0; position < name.length; position++) {
  console.log(name[position])
}
```

#### Prototype members

  - Prefix private members with `_`
```javascript
Example.prototype.method = function () {

  this.public = 'external'
  this._private = 'internal'
}
```

  - Define `self` for passing `this` into nested functions
```javascript
Example.prototype.method = function () {

  var self = this

  call(123, function (err) {

    self.display(err)
  })
}
```

#### Function declaration

  - Declare functions via assignment
``` javascript
// Right

var method = function () {

}

// Wrong

function method() {

}
```

#### Private functions
  - Use _ before the name of a private function
```javascript
// Right
let _method = function () {
  //Body of a private function
}

// Wrong (Only if its a private funciton.)
let method = function () {
   
}
```

#### Enforcing new on Constructor

  - Use this.constructor `===` to check if a constructor function was called with new
```javascript
// Right
Hoek.assert(this.constructor === Server, 'Server must be instantiated using new')

// Wrong
Hoek.assert(this instanceof Server, 'Server must be instantiated using new')
```

### Style

#### Whitespace

  - Always spaces, never tabs
  - 2 spaces indents
  - No trailing whitespace at end-of-line

```javascript
// Right

if (test) {
  if (value === 12) {
    console.log('result')
  }
}

// Wrong

if (test) {
    if (value === 12) {
        console.log('result');
    }
}
```

#### String literals

  - Always `'` never `"`
```javascript
// Right
var string = 'text in single quotes'

// Wrong
var string = "text in single quotes"
```

#### Newlines

  - All files need to end with a newline (or more accurately end of line).  IDEs will often do a line separator instead.  This is to ensure it is unix friendly.  The "cat" command is a good example of seeing this behavior.  Git does a good job of pointing these out when doing pull requests.  

  - Two empty lines between module functions or assignments (end of function to comment about next function)
```javascript
exports.get = function () {

  // Some code
}
                                                          // 1
                                                          // 2
/**
* jsDoc comment
*/
var utility = function () {

  //Some code
}
```

  - Newline after `{` except for inlined or empty objects
    - Inline an object when it improves readability and unlikely to change often
    - No inline object in assignment unless empty

```javascript
  // Right

  if (condition) {
      execute(value, { strict: true });
  }

  if (condition) {
      var options = {
          strict: true
      };
      execute(value, options);
  }

  var empty = {};

  // Wrong

  if (condition) { execute(value, { strict: true }); }

  if (condition) {
      var options = { strict: true };
      execute(value, options);
  }

  var empty = {
  };
```

  - Newline after `}`
    - Only exception is when followed by `,`, `;`, `)` which must be followed by a newline
    - Doesn't include before `else`, `catch`, etc.
    - Empty line after `}` if not last statement in scope

```javascript
// Right

if (condition) {
  value = {
    func: function () {

      console.log('example')
    },
    message: 'hello'
  }

  execute(value, function (err) {

      console.log(err)
  })
} else {
  console.log('otherwise')
}

// Wrong

if (condition) {
  value = {
    func: function () {

      console.log('example');
    }, message: 'hello'
  };
  execute(value, function (err) {

    console.log(err) }
  );
}
else {
  console.log('otherwise')
}
```

  - No empty line before end of scope
```javascript
// Right

if (condition) {
  if (otherCondition) {
    console.log('done')
  }
}

// Wrong

if (condition) {
  if (otherCondition) {
    console.log('done');

  }

}
```

#### Spaces

  - Use one and only one space (when required)
```javascript
// Right
var value = calculate(1, 3)

// Wrong
var  value =  calculate(1,  3);
```
  - One space between function and `(` when declaring a function
```javascript
// Right
var example = function () {

  return value
}

// Wrong
var example = function() {

  return value;
};
```

  - No space between function name and `(` when invoking a function
```javascript
// Right
var key = example()

// Wrong
var key = example ()
```

  - No space after `(` or before `)`
```javascript
// Right

execute('order', 34)

if (result === 'ok') {
  console.log('success')
}

// Wrong

execute( 'order', 34 )

if ( result === 'ok' ) {
  console.log( 'success' )
}
```

  - No space before object key `:`, always after object key `:`
```javascript
// Right
var obj = {
  a: 1,
  b: 2,
  c: 3
}

// Wrong
var obj = {
  a : 1,
  b :2,
  c:3
}
```

  - Always space after reserved keywords (`if`, `else`, `for`, `return`, `function`, etc.)
```javascript
// Right

for (var book in books) {
  if (books.hasOwnProperty(book)) {
    console.log(book.name)
  }
}

// Wrong

for(var book in books) {
  if(books.hasOwnProperty(book)) {
    console.log(book.name)
  }
}
```

  - Always space after `{` and before `}` in inlined object
    - No space for empty objects `{}`
    - One space for empty functions `{}`

```javascript
// Right

var user = { name: 'john', email: 'john@example.com' }
var empty = {}
var callback = function () {}

// Wrong

var user = {name: 'john', email: 'john@example.com'}
var empty = {  }
var callback = function () { }
```

  - No space after `[` and before `]` in inlined arrays
```javascript
// Right
var numbers = [1, 2, 3]

// Wrong
var numbers = [ 1, 2, 3 ]
```

  - Always space after `//`
```javascript
// Right
// Some comment

// Wrong
//Some comment
```

  - No space before `,`, always after `,` unless end-of-line
```javascript
// Right

var numbers = [1, 2, 3]
var user = { name: 'john', email: 'john@example.com' }

for (var i = 0; i < name.length; i += 1) {
  console.log(name[i])
}

// Wrong

var numbers = [1,2 ,3]
var user = { name: 'john',email: 'john@example.com' }

for (var i = 0; i < name.length; i += 1) {
  console.log(name[i])
}
```

  - Always space before and after operators, unless following an indent or end-of-line

```javascript
// Right

var a = 1 + 3
var b = 'john' +
        ' ' +
        'doe'

// Wrong

var a=1+3
var b='john'+
      ' '+
      'doe'
```

#### Commas

  - Never begin a line with `,` (always at the end of the previous line)
```javascript
// Right
execute('some error message',
        12345,
        this)

// Wrong
execute('some error message'
        ,12345
        ,this)
```

#### Operators

  - Never begin a line with an operator (always at the end of the previous line)
```javascript
// Right
var message = 'Hello ' +
              'Steve, ' +
              'How are you?'

if (value === 'hello' &&
    result === 'ok') {

    console.log('yes')
}

// Wrong
var message = 'Hello '
              + 'Steve, '
              + 'How are you?'

if (value === 'hello'
    && result === 'ok') {

    console.log('yes')
}
```

#### Comments

  - Always use `//` unless it's a jsDoc declaration or license header
  - Always begin sentences with an upper case
  - No trailing `.` unless comment contains multiple sentences
  - Formal style, consistent voice, no humor, present tense
  - No developer name or other personal notes
  - No TODOs

  - Line
    - Provides narrative for the following single code line (or single statement broken for readability)
    - One line of comment only
    - One empty line before and none after the comment line
    - No empty line before when following `{` unless other rules require it

```javascript
function execute() {

  // Initialize state
  var position = 0

  if (condition) {
    // Return message
    return 'hello'
  }
}
```

  - Note
    - Explains the behaviour of a single code statement (can be broken into multiple lines)
    - Used to document unexpected behaviour or non-standard practice
    - Appears immediately at the end of the line (or statement) it describes, following whitespace to separate it from code block

```javascript
function execute(value) {

  if (value !== null &&
    value !== undefined) {      // Explicit check as 'value' can be 0

    console.log(value)
  }
}
```

#### Multi-line statements

  - Statements should only be broken into multiple lines to improve readability
  - Break statements if they are longer than 150 characters long
  - No empty lines in the middle of a single statement
  - Indent multi-line statements

  - Conditions should be indented to the first character of the condition in the first line

```javascript
if (result &&
  result.status &&
  result.status.statusCode === 200) {

  console.log('success')
}
```

  - Variable should be indented to the first character of the value in the first line
```javascript
var message = 'hello' +
              ' and welcome'
```

## Node

### Require

  - Use uppercase variable names for imported modules
  - All require statements must be declared at the top of the module
  - Always use relative paths

### Variable names

  - `err` is reserved for errors received via a callback. Use `error` for local function variables
  
### Using let
  - Try to use `let` instead of `var`. let allows you to declare variables that are limited in scope to the block, statement, 
    or expression on which it is used. This is unlike the var keyword, which defines a variable globally,
    or locally to an entire function regardless of block scope. 
    let is allowed in ECMAScript 6. and node version 4.2.1. In node let should be used in strict mode

### Errors

- Always create a new Error object with your message. Don't just return a string message to the callback. Stack traces are handy.

### Case, naming, etc.

- Use lowerCamelCase for multiword identifiers when they refer to objects, functions, methods, properties, or anything not specified in this section except required files.

- Use UpperCamelCase for class names (things that you'd pass to "new") or required files.

- Use lowerCamelCase for multiword filenames and config keys.

- Use CAPS_SNAKE_CASE for constants, things that should never change and are rarely used.

### Callback

  - First argument must always be `err`
  - Callbacks should always be called with explicit `return`
  
### Module.exports
  - All the methods which are to be exported should be assigned to the Module.exports as object
    e.g.  Module.exports = {
            method1: method1,
            method2: method2
          }
          
### Mocking for test cases
  - For mocking functions while running test cases `simple-mock` should be used over `rewire` unless
   we want to mock the logical private method, where `simple-mock` will not work.

