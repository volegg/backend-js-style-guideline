[Linting](#linting)

[Code style considerations](#code-style-considerations)

* [Whitespaces](#whitespaces)

* [Line length](#line-length)

* [Variables](#variables)

* [Naming](#naming)

* [Semicolons](#semicolons)

* [Quotes](#quotes)

* [Comments](#comments)

* [Blocks](#blocks)

* [Chained method calls](#chained-method-calls)

* [Switch statements](#switch-statements)

* [Delete operator](#delete-operator)

* [Equality](#equality)

* [Ternary operator (?:)](#ternary-operator-)

* [Type checks](#type-checks)

* [Code nesting](#code-nesting)

* [Do not use](#do-not-use)

[Using JSHint in JetBrains WebStorm/PHPStorm](#using-jshint-in-jetbrains-webstormphpstorm)


# Linting #

Use [JSHint](http://jshint.com/docs/options/) to detect errors and potential problems. The options for JSHint are stored in a .jshintrc file, all options must be alphabetized.

[JSHint Options](https://raw.githubusercontent.com/volegg/backend-js-style-guideline/master/.jshintrc)

# Code style considerations #

## Whitespaces ##

Use 4 spaces for indents. Usage of tabs for indents should be avoided (replace tab to spaces).

```js
let config = {
    path: '/users',
    debug: true
};

function fact() {
    let i = 0;
}

if (true) {
    let inc = 2;

    for (let i = 0; i < inc; i++) {
        // statements
    }
}
```

Wrap operators (assignment, comparison, bitwise, logical, string, special) with single spaces.

```js
let i = 1 + 2;
 
1 !== 0;
 
1 & 0;
 
1 || 0;
 
"Hello, " + "world!";
 
true ? 1 : 0;
```

Use single space after functions, loops, operators keywords and after parentheses.

```js
function () {
    // statements
}
 
function fact() {
    // statements
}
 
if (condition) {
    // statements
}
 
while (condition) {
    // statements
}
 
for (let i = 0; i < 3; i++) {
    // statements
}
```

Use single space before parameters and arguments except first.

```js
function fact(i, j, k) {
    // statements
}
 
fact(1, 2, 3);
obj.method('Hello, ', 'world!');
```

Use one blank line after let, functions, loops, if/else statements and one space line before return.

```js
let a = 10;
let b = 20;
let m;
let n;
 
function () {
    // statements
}

if (condition) {
    // statements
}

if (condition) {
    // statements
 
} else {
    // statements
}

while (condition) {
    // statements
}
 
for (let i = 0; i < 3; i++) {
    // statements
}

return 'some return data';
```

## Line length ##

Limit line length to 120 characters.

## Variables ##

Declare variables using only "let" statement (does not use "var"). 

Declare "let" where needed.

```js
let keys = ['vehicle', 'model', 'year'];
let condition = true;
 
if (condition) {
    let inc = 2;
  
    for (let i = 0; i < inc; i++) {
        // statements
    }
}
 
let obj = {
    method: function (greet, text) {
        return greet + text;
    }
}
 
obj.method('Hello, ', 'world!');
```

Declare one variable per "let" statement. 

Declaration variables without "let" should be prohibited.

```js
let keys = ['vehicle', 'model', 'year'];
let obj = {};
let i;

```

## Naming ##

Use camel case with lowercase first letter for variables, properties, arguments and parameters.

```js
let isEmptyItem = true;
 
var carObj = {
    hasFogLights: false
};
 
function fact(stepVal, incVal) {
    // statements
}
```

Use camel case with uppercase first letter for function constructor or sails services.

```js
function CarMaker(maker) {
    // statements
}
 
let elantra = new CarMaker(hyundai);

SomeService().list();
SomeService2.init();
```

Use all uppercase letters for constants and "const" keyword. 

Use @const to indicate a constant (non-overwritable) pointer (a variable or property)

```js
/**
 * PI is the ratio of a circle's circumference to its diameter, commonly approximated as 3.14159
 * @const
 */
const PI = 3.14159;
 
/**
 * Euler's number
 * @const
 */
const E = 2.71;
```

Use "me" as reference to this context or arrow function.

```js
function rt() {
    let me = this;
 
    return function () {
        return me;
    };
}
 
service.isValid = function isValid(obj) {
    let isValid = true;

    Object.keys(obj)
        .forEach(property => isValid = isValid && this.validate(property, obj));
 
    return isValid;
} 
```

## Semicolons ##

Use always semicolons.

## Quotes ##

Use single quotes.

Strings that require inner quoting must use single outside and double inside.

```js
let single = 'I am wrapped in single quotes';
let innerQuoting = 'Some string with "property"';
```

## Comments ##

Use [JSDoc](http://usejsdoc.org/) notation

## Blocks ##

Use multi-line blocks.

```js
if (condition) {
    return true;
}
 
while (x < 10) {
    y++;
}
```

Opening braces { should be on the same line as statements.

```js
if (condition) {
    // statements
}
 
function fact() {
    // statements
}
```

Closing braces } should be on a new line and be indented as statements.

```js
function fact() { 
    if (condition) {
        // statement
 
        for (let i = 0; i < 3; i++) {
            // statements
        }
    }
}
```

## Chained method calls ##

When a chain of method calls is too long to fit on one line, there must be one call per line, with the first call on a separate line from the object the methods are called on. If the method changes the context, an extra level of indentation must be used.

```js
ContentService()
   .list(query)
   .addCreator()
   .then(data => {
       // statements
   })
   .catch(err => {
       // statements
   });
```

## Switch statements ##

The usage of switch statements is generally discouraged, but can be useful when there are a large number of cases - especially when multiple cases can be handled by the same block, or fall-through logic (the default case) can be leveraged.
When using switch statements:
Use a break for each case other than default.
Align case statements with the switch.

```js
function buildFilter(filter) {
    switch (filter) {
        case 'filter1':
            // statements
            break;
        case 'filter2':
        case 'filter4':
            // statements
            break;
        case 'filter3':
            // statements
            break;
        default:
            // statements
    }
}
```

## Delete operator ##

The delete operator deletes only a reference, never an object itself. If it did delete the object itself, other remaining references would be dangling. 
Prefer use:

```js
Foo.prototype.dispose = function() {
  this.property_ = null;
};
```

instead of:

```js
Foo.prototype.dispose = function() {
  delete this.property_;
};
```

## Equality ##

Use strict equality operators ===, !==. Usage of equality operators ==, != should be avoided.

```js
11 === 11; // true
11 === '11'; // false
true === true; // true
1 === true; // false
```

## Ternary operator (?:) ##

Execute function by condition.

Instead of this:

```js
if (val) {
  return foo();
} else {
  return bar();
}
```

Prefer write:

```js
return val ? foo() : bar();
```

Default variable assignment.

```js
function foo(environment) {
  let env = environment || 'production';

  // statements
}
```

Conditional variable assignment.

```js
function foo(arg1, arg2) {
    let param = arg1 > arg2 ? arg2 : arg1;
 
	// statements
} 
```

Don't use OR condition for variable assignment 

```js
condition || (param = 'some value assignment');
```

Don't use nested ternary operators.

```js
let a = condition ? (superCondition ? 10 : 'nested ternary') : true);
```

## Type checks ##

String: typeof object === 'string'

Number: typeof object === 'number'

Boolean: typeof object === 'boolean'

Object: typeof object === 'object'

Function: typeof object === 'function'

Array: object instanceof Array

null: object === null

undefined: 

* Local Variables: variable === undefined

* Properties: object.prop === undefined

## Code nesting ##

Use earlier return to avoid deep nesting code. Possible depth is 3, otherwise move code block to separate function.

```js
function someAction(arg1, arg2, arg3) {
	if (arg1 === undefined) {
		return;
	}

	if (arg2 === undefined) {
		return;
	}

	if (arg1 === true) {
		if (arg3 !== undefined) {
			nested(arg1, arg3);

		} else {
			nested(arg1, arg2)
		}

	} else if (arg2 === false) {
		nested(arg1, arg2);
	}

	return arg3;
}

function nested(arg2, arg3) {
	if (arg2 === arg3) {
		return;
	}

	if (arg2) {
		// statements
		if (arg3 === undefined) {
			// statements
		}
		
	} else {
		// statements
	}
}

```

## Do not use ##

    var

    eval()

    with() {}

# Using JSHint in JetBrains WebStorm/PHPStorm #

![Use custom JSHint file](https://s3.amazonaws.com/public-file-bucket/add-jshint-to-project.png)
