## 

# primitive values vs. objects

#### Primitive Value

**primitive value**: is data that is not an object and has no methods. 

- Primitive values are **immutable** which means that the value doesn't change. 
- The variable can be assigned to a different vale, but the primitive value itself cannot be changed. 
- When using primitive values in operations, they always evaluate to a new value. 
- For example `0 + 0` evaluates to a new value `0`. 

Primitive types are simple and basic. 

There are 5 primitive data types. 

- string

  - Data enclosed in single, double quotation marks, or string literals.

- number

  - can't use commas for grouping

  - **`NaN`** 

    - Is the result of an attempted math operation that is not valid number nor an infinite number. 
    - NaN is a number.
    - It's the only value in JavaScript that is not equal to itself
    - You must use `Number.isNaN` or `Object.is` to determine whether a number is `NaN`. 

    ```js
    > let value = NaN;
    > Number.isNaN(value)
    = true
    
    > Object.is(value, NaN)
    = true
    ```

  - **`Infinity`** = 1/0

  - negative infinity - 1/0

- undefined

  - Undefined is assigned to any object that has been declared but not yet initialized or defined.
  - It signifies an absence of value. 
  - It may arise implicitly. 

- `null`

  - Null is a keyword that signifies an absence of value. 
  - It's similar to undefined but it never arises implicitly, you must use `null` explicitly if you want to use it. 
  - Null's type is 'object'.

- boolean

  - Boolean is a datatype that returns either true or false.
  - **Double not (!!)** converts an object/variable to a boolean value. !!Bcondition === Bcondition

#### Objects

**Objects**: Objects are comprised of primitive values or other objects. Objects are **mutable:** If you change something about the the object, all variables that reference that object will also change. 

- simple objects
- **arrays**: 
  - an indexed based list of elements, each element has a value of any type. You can define an array by placing a list of values between brackets  (`[]`). 
  - Uses zero-based indexing system.
  - Replace and add elements with brackets `[]` and assignment operator
- Dates
- Functions

**Neither an Object nor Primitive**

- Anything that isn't data or a function is neither a primitive value nor an object. This includes
  - variables and other identifiers such as function names
  - statements such as `if`, `return`, `try`, `while`, and `break`
  - keywords such as `new`, `function`, `let`, `const`, and `class`
  - comments
  - anything else that is neither data nor a function
- Note that variables and other identifiers have or reference objects or primitive values, but the names, by themselves, are not.

# Type Coercions

**Type Coercions** : Type coercion is converting a value from one type to another. There are two types of coercion. 

#### Implicit Type Coercion

**Implicit type coercion**: is when values are converted between different types automatically by the JavaScript engine. It usually happens when we use operators on values of different types. 

- The most common operations of implicit coercion are the non-strict equality operator  `==` and the binary plus operator `+`. [Reference](Lesson 2 ImplicitTypeCoercion.md) 

- Whenever you use a string operand in numeric expression with these operators `-, *, /, %`, the operands will be converted to strings similar to calling the `Number` function on the value. 

- The **non-strict equality operator** `==` coerces one operand into the other operand's type, then compares the two. 

  This chart displays how `==` coerces different data types. 

  ```javascript
  number == string // true, string coerced to number
  object == primitive // true, == object ceorced to primitive
  undefined == null // true
  boolean == any data type //bolean ceorced to number, then compared again using == 
  object == object // false, same as ===, operator, objects are equal only when they're the same object. 
  ```

- When using **binary plus**`+` operator, the general rule is that if one operand is a String and the other operand isn't, then the non-String operand is coerced into a String and concatenated with the String operand.

  - Concatenation is the **process of appending one string to the end of another string**. You concatenate strings by using the + operator. 

  ```terminal
  > '1' + 2
  = '12'
  
  ```

  ```markdown
  This demonstrates the principle of implicit coercion through the binary plus `+` operator, when one operand is a String and the other operand is not, the non-String operand is coerced into a string and concatenated with the String operand. 
  ```

  

  If one operand is an object, both operands are converted to strings and concatenated together. 

  ```
  [1] + 2;        // "12"
  42 + {};        // "42[object Object]"
  [1, 2] + 3;     // "1,23"
  [] + 5;         // "5"
  ```

  If both operands are numbers, booleans, nulls, or undefined, they are converted to numbers and added together. 

  ```
  1 + true;       // 2
  1 + false;      // 1
  true + false;   // 1
  null + false;   // 0
  null + null;    // 0
  1 + undefined;  // NaN
  ```

- **relational operators**: `<`, `>`, `<=`, and `>=`  are used for numeric comparison and string comparison (lexicographic order), and perform implicit coercion. 

  - When comparing a string with a number, JavaScript will convert the string to a number when doing the comparison. 

```
11 > '9';       // true -- '9' is coerced to 9
'11' > 9;       // true -- '11' is coerced to 11
123 > 'a';      // false -- 'a' is coerced to NaN; any comparison with NaN is false
123 <= 'a';     // also false
true > null;    // true -- becomes 1 > 0
true > false;   // true -- also becomes 1 > 0
null <= false;  // true -- becomes 0 <= 0
undefined >= 1; // false -- becomes NaN >= 1
```

- Another example is  `if (value) {...}` ,  `value` is implicitly coerced to boolean. 

##### Template Literals

- **Template Literals** implicitly coerce the interpolation expressions to strings by invoking the `toString()` method. 
- Hence we don't write `${something.toString()}` or `${String(something)}`.

#### Explicit Type Coercion

**Explicit type coercion**: is when we intentionally use a built-in function to coerce one type of value to another. [Reference](Lesson 2 Explicit Type Coercion.md)

>  **Best practice is to always use explicit type coercion**
>
>  The only exception is to not use  `String()` or `toString()` inside interpolation expressions of template literals. `${...}` because template literals implicitly coerce the interpolation expressions to strings. 
>
>  Hence we don't write `${something.toString()}` or `${String(something)}`.

-  **`Number(any type)`** function coerces a string to a number. 

```terminal
> Number(undefined)
= NaN

> {}.toString();
= '[object object]'

```

- The **unary plus** `+` operator coerces values to number, same as using **Number()**

```js
> +""
0
> +'1'
1
> +'2.3'
2.3
> +[]
0
> +'abc'
NaN
```

- **`parseInt(any type)`** converts first argument to string, parses that string, then returns an integer or `NaN`. 

  - It parses up to the first non-digit, then returns whatever it has parsed. Think: this function is normally used to slice off the decimal digits in a floating number. 

  ```js
  parseInt(string)
  parseInt(string, radix)
  ```

  - Parameters
    - `string`: the value to parse. If it's not a string, it's converted to one using toString. If string part doesn't have a digit, then `NaN` is returned. 
    - `radix` (optional), integer between 2 -36 that represents the base.

```js
Number('12 oz');   // NaN
parseInt('12 oz'); // 12

Number('');        // 0
parseInt('');      // NaN

parseInt("123qwe") // 123
Number("123qwe") // NaN

// Number() wants to convert entire string to number. parseInt() parses up to first non-digit and returns whatever it has parsed. 
```

- **`toString`** method converts all data types except `null` and `undefined` to string. 

  - you can use the **`toString`** method on all JavaScript data types except `null` and `undefined`. It returns a string representation of the value. 
  - We can't call the method on a number literal because the `.` is interpreted as being part of a floating point number, so we should wrap the number in parentheses. 

  ```terminal
  > 42.toString()
  SyntaxError: Invalid or unexpected token
  
  > (42).toString()
  '42'
  ```

  - You can also use two `.` characters instead, though it looks a bit strange:

  ```terminal
  > 42..toString()
  '42'
  ```

- **`String`** coerces any data type to to string. Works with `null` and `undefined`

  - It does this by invoking `toString()`. 

  ```terminal
  > String(42)
  '42'
  > String([1, 2, 3])
  '1,2,3'
  > String({ a: 'foo', b: 'bar' })
  '[object Object]'
  ```

  ```terminal
  > String(null)
  'null'
  > String(undefined)
  'undefined'
  ```

boolean vs. truthiness

array and object syntax

array properties and methods: `array.length`, `array.push`, `array.pop`, `array.reverse`

object methods: `Object.keys`

operators

- numeric operators: `+`, `-`, `*`, `/`, `%`
- string operators: `+`
- conditional operators: `===`, `!==`, `<`, `>`, `<=`, `>=`, `==`, `!=`, ternary
- loose and strict equality
- logical operators and short-circuit evaluation: `!`, `&&`, `||`
- the `typeof` operator
- operator precedence

# variables

#### identifier: 

- variable names 

- constant names

- function names

- property names

#### variable and constant declarations

**Declarations**: 

- Declarations define variables and functions. It binds a variable or function to an identifier. It's a statement that reserves space for a variable or function with a particular name, called identifier.  
- When you declare a variable it is automatically initialized, which means memory is allocated for the variable.
- Variables declared with `let` or `const` have block scope.
- The preferred way in JS is to use the `let` keyword to declare variables. Variables declared with `let` can be reassigned.
- **Declaring constants**: Variables declared using **`const`** cannot be reassigned to a different value. However, it doesn't mean that the value is always <u>immutable.</u> If you declare an <u>object</u> with `const`, the object's properties can still be changed. Although the identifier cannot be reassigned to a different value. 
  - `Const` prohibits changing what `const` points to, but does not prohibit changing the `const` object properties.
  - we can't reassign an object declared with `const`, but we can still mutate it (add and change the properties of the object). 

#### initialization, assignment, and reassignment

**Initialization**: 

- During declaration, the variable is initialized to a provided value, or undefined if no explicit value is provided. 

- In a declaration, what is normally the assignment operator `=` is instead a token that indicates you are going to supply an initial value for the variable. 

  ```js
  let x = 1; // x is initialized to 1
  ```

- If you declare variable without an **initializer**, variable is initialized to undefined. 

  ```js
  let x; // x is initialized to undefined
  ```

**Assignment**: 

"An assignment does not copy an object. The assigned value is a reference to an object, not the object itself. The value stored in an object reference variable is a pointer to the data that makes up the object. "

- Primitive values are assign by value
- Objects are assign by reference. 

- Assigns a value to its left operand based on the value of its right operand. 
- `=` is the assignment operator. 

**Re-assignment**: 

- assigns a new a new value for a variable using the assignment `=` operator. 

#### scope

- A variable's scope determines where it is is available in a program. A variable's scope is determined by where its declared. 

- **scope** means the part of the program that can access that variable by name. There are two different types of scope

- **local scope**:  Local scope has two forms: function scope & block scope.  **Local Variables** exist within function scope and block scope.

- **function scope**: Functions define a new scope for local variables. 

  Rules

  1. Outer scope variables can be accessed by the inner scope.

  2. Inner scope variables cannot be accessed in the outer scope.

  3. Peer scopes do not conflict. (variables in different scopes don't conflict)

     ```js
     function funcA() {
       let a = 'hello';
       console.log(a);
     }
     
     function funcB() {
       console.log(a); // ReferenceError: a is not defined
     }
     
     funcA();
     funcB();
     ```

  4. Nested Functions have their own variable scope. 

     ​	- Nested Functions follow the same rules of inner and outer scoped variables. 

     ```js
     let a = 1;           // first level variable
     
     function foo() {     // second level
       let b = 2;
     
       function bar() {   // third level
         let c = 3;
         console.log(a);  // => 1
         console.log(b);  // => 2
         console.log(c);  // => 3
       }
     
       bar();
     
       console.log(a);    // => 1
       console.log(b);    // => 2
       console.log(c);    // => ReferenceError
     }
     
     foo();
     ```

     ​	- This includes functions inside functions

     ```js
     function logElements(array) {
       array.forEach(function(element) {
         console.log(element);
       });
     }
     
     logElements([1, 2, 3]);
     ```

  5. Inner scope variables can **shadow** outer scope variables. 

     - **Variable shadowing** happens when you have a local variable with the same identifier name as the outer scope variable. The local variable **shadows** the outer scope variable and prevents access to the outer scope local variable, or making any changes to the outer scoped variable. 

       Most identifier names- variables, parameters, function names, or class names - can shadow names from the outer scope. The only names that do not shadow are property names for objects. 

     - Example

       ```js
       let number = 10;
       
       [1, 2, 3].forEach(number => {
         console.log(number);
       });
       // 	console.log(number) will use the parameter number and discard the outer scoped local variable. 
       ```

       ```js
       let a = 1;
       
       function doit(a) {
         console.log(a); // => 3
       }
       
       doit(3);
       console.log(a); // => 1
       
       // parameter a is shadowing global variable a. 
       ```

- **block scope**:  

  - A block is a related set of JavaScript statements and expressions between a pair of opening and closing curly braces. 
  -  `if / else` and `for` and `while` loops define new block scopes. 

  ```js
  if (expression) {  // block starts at {
    doSomething();   // block body
  }                  // block ends here
  ```

  Rules

  1. Outer blocks cannot access variables from inner scopes. 
  2. Inner blocks can access variables from outer scopes. 
  3. Variables defined in an inner block can shadow variables from outer scopes. 

  - But not everything between curly braces is a block. Function bodies are not blocks, nor are braces that surround an object literal, but we can treat them like blocks. Blocks that aren't functions bodies are **non**-**function blocks**.

- **global scope**: variables declared outside of blocks. 

  -  global variables are available across your entire program. You can use them anywhere in the program, either globally or from inside a block. 
  -  **Global variables**: are variables not inside functions or blocks. 

```js
if (1 === 1) {
  let a = 'foo';
}

console.log(a); // ReferenceError: a is not defined
```

```js
let a = 'foo';
if (1 === 1) {
  a = 'bar';
}

console.log(a);    // => 'bar'
// a has a braoder scope here than the a variable in the previous example. 
```

#### Variable shadowing

Inner scope variables can **shadow** outer scope variables. 

- **Variable shadowing** happens when you have a local variable with the same identifier name as the outer scope variable. The local variable **shadows** the outer scope variable and prevents access to the outer scope local variable, or making any changes to the outer scoped variable. 

  Most identifier names- variables, parameters, function names, or class names - can shadow names from the outer scope. The only names that do not shadow are property names for objects. 

- Example

  ```js
  let number = 10;
  
  [1, 2, 3].forEach(number => {
    console.log(number);
  });
  // 	console.log(number) will use the parameter number and discard the outer scoped local variable. 
  ```

  ```js
  let a = 1;
  
  function doit(a) {
    console.log(a); // => 3
  }
  
  doit(3);
  console.log(a); // => 1
  
  // parameter a is shadowing global variable a. 
  ```


#### variables as pointers

- Variables as **pointer** means that variable's value is a reference to an object's address place in memory. 

```js
let a = [1, 3];
let b = [2];
let arr = [a, b];
arr // => [ [ 1, 3 ], [ 2 ] ]
```

- Mutating array `a` changes `arr` because the object at index 0 of `arr` and `a` point to the same object.  This demonstrates the variables as pointers concept where a variable's value is a reference or pointer to an object's memory address. 

- Variables with primitive values on the other hand store the value at the location of the variable's memory address. 

# mutability vs. immutability vs. `const`

- **Immutable**: means that the data's structure or value cannot be altered. 
  - Primitive values are **immutable**. This means that the value can't be altered. You can only reassign the variable to a different value. When using primitive values in operations, they always evaluate to a new value. For example `0 + 0` evaluates to a new value `0`. 
- **Mutable**: means a type of variable that can be changed. 
  -  Objects and arrays (which are also objects) are **mutable** -  it has parts that can be altered. 
- Variables declared using **`const`** are not necessarily immutable. If you declare an object with `const`, the object's properties can still be changed. However, the variable identifier cannot be reassigned to a different value. 
  - `Const` prohibits changing what `const` points to, but does not prohibit changing the `const` object properties.
  - we can't reassign an object declared with `const`, but we can still mutate it (add and change the properties of the object). 

# conditionals and loops

#### Incrementing

- The **increment operator** (`++`) increments its operand by `1`; that is, it adds `1` to the existing value. 
- There's a corresponding **decrement operator** (`--`) that decrements a variable's value by `1`. That is, it subtracts `1` from the value. 

- There's a growing sentiment among some developers that the increment and decrement operators are harmful. It's easy to mistype them in ways that can lead to strange bugs, especially if you're not mindful of the return values. They recommend using the `+=` and `-=` operators instead; it's only a few characters more to type.

- Most developers still use them in the increment clause of a `for` loop:

  ```js
  for (var index = 0; index < 5; ++index) {
    // body of loop
  }
  ```

​	However, they shouldn't be used anywhere else.

#### Loops

**`While` loops**

- A `while` loop uses the `while` keyword followed by a conditional expression in parentheses and a block. 
  - The loop executes the block again and again for as long as the conditional expression remains truthy. In most programs, that loop should ultimately stop repeating. 
  - That means that the block must do something that tells JavaScript when the loop should stop; that is, it needs to arrange for the conditional expression to become falsy. Otherwise, the loop is an **infinite loop** that never stops repeating.

**`for` loops**

- `for` loops have the same purpose as `while` loops, but they use a condensed syntax that works well when iterating over arrays and other sequences. 

- `for` loops let you see and understand the looping logic at a single glance. The syntax also lets you move the `index` variable from the global scope into the scope of the `for` statement, and it helps make your code cleaner and more organized.

- A `for` loop combines variable initialization, a loop condition, and the variable increment/decrement expression all on the same line:

  ```js
  for (initialization; condition; increment) {
    // loop body
  }
  ```

  This structure behaves almost the same as:

  ```js
  initialization;
  while (condition) {
    // loop body
    increment;
  }
  ```

**`do/while` loop**

- A **do/while loop** differs visibly from a `while` loop, but its behavior is almost identical. 
- The crucial difference is that `do/while` always executes the code in the block at least once. A `while` loop can't make that guarantee since the initial condition may be falsy; if it is, the loop body doesn't run. 
- In a `do/while` loop, the conditional check occurs at the end of the loop instead of the beginning which allows it to run the code at least once, even if the condition is falsy when the loop begins.

```js
let answer;
do {
  answer = prompt("Do you want to do that again?");
} while (answer === 'y');
```

#### Controlling loops

- JavaScript uses the keywords `continue` and `break` to provide more control over loops. `continue` lets you start a new iteration of the loop, while `break` lets you terminate a loop early.

`continue`

- `continue` lets you start a new iteration of the loop.

`break`

- Terminate the loop early --> Skip all remaining iterations of a loop and terminate.
- For instance, when you search an array for a specific value, you probably want to stop searching once you find it. There's no reason to keep searching if you don't need any subsequent matches.

# `console.log`

- This built-in function takes any JavaScript value, regardless of type, and logs it to the console. 
- It is used for outputting values into the command line console.

# `readline-sync` and the `question` method

- Node.js has an API called **readline** that lets JavaScript programs read input from the command line.
- However, the API isn't straightforward or simple: it requires an understanding of asynchronous programming and higher-order functions. We don't explore these concepts in this book. For now, we can use a simplified version of the readline library called **readline-sync**.

#### Install readline-sync

To install readline-sync, see if there's already a package.json file.

```terminal
## see if there's already a package.json file
$ ls package.json
package.json
```

```terminal
$ ls package.json
ls: cannot access 'package.json': No such file or directory

$ npm init -y
Wrote to .../package.json:

{
  "name": "Downloads",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

if not, run `npm init -y`

 Once you have a `package.json` file, you can install `readline-sync` as follows:

```terminal
$ npm install readline-sync --save
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN Downloads@1.0.0 No description
npm WARN Downloads@1.0.0 No repository field.

+ readline-sync@1.4.10
added 1 package from 1 contributor and audited 1 package in 0.423s
found 0 vulnerabilities
```

The `npm install` command with a `--save` option installs the package in the `node_modules` subdirectory of your current directory. By placing it in this subdirectory, any Node.js programs stored in the current directory can require the package with a simple call to `require`, as we'll see in the following example:

```js
let rlSync = require('readline-sync');
let name = rlSync.question("What's your name?\n");
console.log(`Good Morning, ${name}!`);
```

#### `require`

- We use node's built-in `require` function to import `readline-sync` into our program. 

```js
let rlSync = require('readline-sync');
```

#### readline.Question()

- we use `rlSync` to call the `question` method. This method displays its given string argument, then waits for the user to respond.

```js
let rlSync = require('readline-sync');

let number1 = rlSync.question('Enter the first number\n');
let number2 = rlSync.question('Enter the second number\n');
let sum = number1 + number2;

console.log(`The numbers ${number1} and ${number2} add to ${sum}`);
```

# Functions

#### functions vs. methods



#### declarations, expressions, arrow functions

3 ways to <u>**define**</u> a function

1. **Function declaration** 

   - Function declaration binds a function to an identifier, declares the existence of the function. 

   - Function declarations can't be anonymous.
   - Function declarations are **hoisted**: can be called before function is defined. 

   ```js
   functionName(); // can invoke function before function is defined.   
   
   function functionName() {
     ...
   }
   ```

2. **Function expression** 

   - `Function` keyword can be used to define a function inside an expression, or omitted to create anonymous function expressions. 

   - Function expressions can be named or anonymous. 

     - However the name is  only local to the function body -> can't be used to reference function outside of the function. 
     - If the name is omitted, the function is anonymous. 

   - Are not **hoisted** : can't use function expressions before you define them. 

   - Any function definition that doesn't have the word `function` at the **<u>beginning</u>** of a statement is a function expression. . 

     ```js
     let functionName = function () { // Anonymous function expression
       ...
     }; // note the semi colon here! It's an expression so it needs semicolon. 
     ```

     ```js
     let functionName = (parameter) => {
       
     };
     ```

   - Wrapping what looks like a function declaration in parentheses creates a function expression

     ```js
     // Function expression, not declaration
     (function greetPeople() {
       console.log("Good Morning!");
     }); 
     ```

     ```js
     function makeGreeter(name) {
       return function greeter() {
         console.log(`Hello ${name}`); 
       }
     }
     // Greeter is a function expression because it starts with return. 
     ```

3. **Arrow function**

   - Arrow functions are always anonymous. 

   ```js
   let greetPeople = () => console.log("Good Morning!"); // 0 parameters
   let greetPeople = paramOne => console.log("Good Morning!"); // 1 parameter,
   let greetPeople = (paramOne, paramTwo) => console.log("Good Morning!") // 2 parameters
   
   greetPeople(); // Must invoke after defining the function. 
   ```

   - Arrow functions have an interesting feature: **implicit returns**: can omit return statement when function body contains a single expression, on a <u>**single line**</u>. 

   ```js
   [1, 2].map(element => return 1 );
   ```

**Anonymous Function**: a function with no name. They are invoked by the variable name. Arrow functions are always anonymous.  

```js
let name = function (x) { // function expression
  
});
```

#### definition and invocation

- **Function**: a reusable block of code that groups together a sequence of statements to perform a specific task. 

- **Function definition: ** are **defined** with the `function` keyword. 
  - The 3 ways to define a function are function declaration, function expression, and arrow functions. 
- functions are only executed when they are **invoked**, called upon. 

#### default parameters

- **Default parameters** allow parameters to have predetermined value in case there is no argument passed into the function or the argument is `undefined` when called. 

```js
function foo(x, y, z = 2){
    //...
}
foo(1);
```

```js
function foo(x, y, z){
    x === 1
    y === undefined
    z === 2 // default parameter value. 
}
```

#### return values

**Return values** are the values a function returns to the call location when it finishes running. All JavaScript function calls evaluate to a value. By default, the value is `undefined` --> the **implicit return value**. 

- **`return`** statement ends function execution and returns a specific value to the *function* caller. This is an **explicit return value**. 

- Thus, REMEMBER that `return` exits the "nearest" function. So a return statement inside an array iteration function such as `forEach` or `filter` does not exit the function, because it's ending the execution and returning to the **callback** function. 

#### parameters vs. arguments

- **Parameters** are the names assigned to a function's arguments; **arguments** are the values that are passed to and received by a function. When you define a function you also define its **parameters**. 

- Parameter rules

  - JavaScript function definitions do not specify data types for parameters.

  - JavaScript functions do not perform type checking on the passed arguments.

  - JavaScript functions do not check the number of arguments received.

- Variables are not passed to or returned by functions: **values **or **references** are passed. 

- if you pass fewer arguments than the declared arguments to the function,  then the missing values are set to undefined. 

- You can also pass more arguments like

  ```js
  foo(1,2,3,4,5,7); // Valid!
  ```

  Use `arguments.length` to know the amount of parameters supplied. 

  ```js
  function foo(x, y, z) {
  	return arguments.length; 
  }
  foo(1, 2, 3, 4);
  ```

#### function, block, local, and global scope

#### nested functions

#### function composition

#### output vs. return values, side effects

#### *pass-by-reference* and *pass-by-value*

- **Pass by value** means passing a copy of the original variable's value. **Pass by reference** means passing a reference (pointer) of an object, rather than the actual value.

[Lesson 2](https://launchschool.com/lessons/64655364/assignments/33123902)

- **Pass by value** means passing a copy of the original variable's value. **Pass by reference** means passing a reference (pointer) of an object, rather than the actual value.

  - They refer to how *function arguments* are passed and returned. 

- **Pass by value** means passing a copy of the original variable's value, the function can't alter the original variable 

  - When you return the value, you can returning a new value.  The original variable retains the same value. 
  - <u>*A copy of the actual parameter's value*</u> is made in the memory: so the caller and caller have two independent variables with the same value. 
  - Primitive values are always pass-by-value. Primitive values cannot be permanently altered by any function or operation. 
  - Passing by value creates new **instances** of the 

- **Pass by reference** means passing a reference (pointer) of an object, rather than the actual value.

  - So if the original object is mutated, any variables that reference the original object also changes. If an object is not mutated, it's not pass-by-value. 
  - Function is able to change the original object. 
  - Passing the **pointer**/ reference of an argument to the called function so *<u>a copy of the address of the actual parameter</u>* is made in the memory. 

- Pass-by-sharing

  - Objects exhibit both pass-by-reference and pass-by-value (*pass- by-sharing*). 

  - Rule: If an operation in a function mutates its object argument, the original object is also mutated. 

  - Methods that mutate callers are called **destructive functions**. 

  - Rules

    - **Reassignment is never destructive**: original array not changed. 

    ```js
    function addName(arr, name) {
      arr = arr.concat([name]);
    }
    
    let names = ["bob", "kim"];
    addName(names, "jim");
    console.log(names); // => [ 'bob', 'kim', ]
    // reassignment itself is not destructive. 
    ```

    - `array.push()` is destructive

    ```js
    function addNames(arr, name) {
      arr = arr.push(name); // push returns lengt of new array. 
      console.log(arr); // arr is now 3, the length of new array. 
    }
    
    let names = ["bob", "kim"];
    addNames(names, "jim");
    console.log(names); // => [ 'bob', 'kim', 'jim' ] but names was mutated. 
    // 
    ```

- `Array.slice()` uses pass-by-sharing because it creates a shallow copy.  It performs pass-by-value on the first level by creating a copy of the values of the original array. But if that array contains nested objects, some nested objects may still be connected to its own original variables and hence  `Array.slice` performs pass-by-reference for those sub-objects. 

  - slice() is a **shallow copy** because **<u>certain</u>** sub values are still connected to *their* original variable*s*. If you alter the sub-values, that change will be reflected in the original array. 

  ```js
  let a = ['hi'];
  let b = [a, 'bye']
  let c = b.slice(); // c is a shallow copy of b. 
  
  console.log(c) 
  c.push('random');
  console.log(c) // [ [ 'hi' ], 'bye', 'random' ]
  console.log(b) // [ [ 'hi' ], 'bye' 
  // changes made to c's outer array doesn't change original variable (b). The outer aray is pass-by-value. 
  
  c = b.slice(); // let's reassign c back to b. 
  
  c[0].push(1) // This mutates all the arrays. 
  console.log(a) // [ 'hi', 1 ]
  console.log(b) // [ [ 'hi', 1 ], 'bye' ]
  console.log(c) // [ [ 'hi', 1 ], 'bye' ]
  
  c[0] = 'hello';
  console.log(a) // [ 'hi', 1 ]
  console.log(b) // [ [ 'hi', 1 ], 'bye' ]
  console.log(c) // [ 'hello', 'bye' ]
  
  // b is not mutated here because c[0] reassigns it's 0th index to 1 instead of a. So a doesn't get changed. Reassignment is never a mutating change.  You must mutate sub-value's original variable (a) in order to mutate b.  Whether you mutate a directly, or mutate a by accessing it through b or c, the change will be reflected in all of the arrays.
  ```

  > - **Deep copy**: makes a duplicate of every item in an existing array or object.  
  >   - It creates **completely new instances** of any subarrays or subobjects in the source object. 
  >   - All values are copied and disconnected from the original variable.
  >
  > - **Shallow copy**: only makes a duplicate of the outermost values in an array or object. Shallow copy stores the copy of the original object and references to objects. 
  >   - **<u>Certain</u>** sub-values are still connected to the original variable. (Not all sub-values in nested array are connected to original variable. ) If you alter the sub-values, that change will be reflected in the original array, and all variables that reference that original array

  

#### the call stack

# expressions and statements

# exceptions: throwing and catching

# common `Math` methods: 

#### `Math.floor`

#### `Math.random`

#### `Math.pow`

# naming conventions: legal vs. idiomatic, illegal vs. non-idiomatic

- **Idiomatic names**: are names that follow the name conventions in [reference](https://launchschool.com/books/javascript/read/preparations#namingconventions)
- Naming Conventions
  - use **camelCase** for variable and function names. 
  - use **SCREAMING_SNAKE_CASE** to represent constants, which serve as unchanging configuration values in the program. Usually those constants are *magic numbers*. 
  - use **PascalCase** for constructor functions and classes. 

| Category                                     | Name              | Notes             |
| :------------------------------------------- | :---------------- | :---------------- |
| Non-constant variables and object properties | `employee`        |                   |
|                                              | `number`          |                   |
|                                              | `fizzBuzz`        |                   |
|                                              | `speedOfLight`    |                   |
|                                              | `destinationURL`  | URL is an acronym |
|                                              | `m00n`            |                   |
| Constructor functions and classes            | `Cat`             |                   |
|                                              | `BoxTurtle`       |                   |
|                                              | `FlightlessBird`  |                   |
| Other functions                              | `parseURL`        | URL is an acronym |
|                                              | `goFaster`        |                   |
| Configuration and magic constants            | `ABSOLUTE_PATH`   |                   |
|                                              | `TODAY`           |                   |
| Other `const` names                          | `employeeOfMonth` | Local style       |
|                                              | `HairyCat`        | Local style       |
|                                              | `ABSOLUTE_PATH`   | Local style       |

- **Legal names**: are names that are syntactically valid, but non-idiomatic (don't follow naming convention). 

#### Valid but Non-Idiomatic Names

| Category                                     | Name           | Notes                        |
| :------------------------------------------- | :------------- | :--------------------------- |
| Universally non-idiomatic                    | `$number`      | Begins with $                |
|                                              | `fizz_buzz`    | snake_case not allowed       |
|                                              | `fizzBUZZ`     | BUZZ is not an acronym       |
|                                              | `_hello`       | Begins with `_`              |
|                                              | `goodbye_`     | Ends with `_`                |
|                                              | `milesperhour` | Undifferentiated words       |
|                                              | `MILESPERHOUR` | Undifferentiated words       |
| Non-constant variables and object properties | `Employee`     | Begins with capital letter   |
|                                              | `fizzBUZZ`     | BUZZ is not an acronym       |
|                                              | `FIZZ_BUZZ`    | SCREAMING_SNAKE_CASE         |
| Constructor functions and classes            | `cat`          | Begins with lowercase letter |
|                                              | `makeTurtle`   | Begins with lowercase letter |
|                                              | `FIZZ_BUZZ`    | SCREAMING_SNAKE_CASE         |
| Other functions                              | `ParseURL`     | Begings with capital letter  |
|                                              | `FIZZ_BUZZ`    | SCREAMING_SNAKE_CASE         |
| Configuration and magic constants            | `absolutePath` | Not SCREAMING_SNAKE_CASE     |
|                                              | `Today`        | Not SCREAMING_SNAKE_CASE     |

#### Invalid Names

| Name       | Notes                         |
| :--------- | :---------------------------- |
| 42ndStreet | Begins with number            |
| fizz-buzz  | Hyphen not allowed            |
| fizz.buzz  | Looks like property reference |

# discuss a function's use and purpose (a "user-level" description) instead of its implementation