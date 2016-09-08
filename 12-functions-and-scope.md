#### [⇐ Previous](./11-nested-data-structures.md) | [Table of Contents](./readme.md) | [Next ⇒](./13-debugging-javascript.md)

# Functions and Scope

### Objectives:

By the end of this chapter - you should be able to

- Define what a function is and how they are essential in programming
- Create functions as a function declaration or function expression
- Explain how scope works in JavaScript and compare function, block and global scope
- Understand what hoisting is and how the JavaScript compiler works when analyzing variables and functions

#### What is a function

One way to think about a function is a process or procedure that takes in some output and returns some input. Functions are one of the most powerful tools in JavaScript so let's see how to write one! While there are two ways to write functions, we will cover the difference in more detail later, but let's start with one way - a function declaration:

```javascript

// this is called the function definition - we are ONLY defining the function here
function firstFunction(){
    console.log("I just wrote my first function!")
}

// to call or invoke the function 
firstFunction()
```

If you run this code in the Chrome Console - you will see the output is "I just wrote my first function" and on the next line, `undefined`. So where is this `undefined` coming from? In JavaScript, if we do not specifically tell the function to output something - it will output `undefined`. So how do we tell a function to output something? We use the `return` keyword!

```javascript

// this is called the function definition - we are ONLY defining the function here
function firstFunction(){
    return("I just wrote my first function!")
}

// to call or invoke the function 
firstFunction() // now we don't see undefined anymore!
```

Remember, the `return` keyword can **ONLY** be used in a function, let's take a look at another example.

```javascript
function secondFunction(){
    return "Hello"
    return "Goodbye"
}

secondFunction(); //"Hello"
```

We see from here that the **return** keyword exits a function immidiately and that we can only `return` from a function once!

#### Adding parameters/arguments to functions

So far our functions have not been taking in any input! They simple are returning an output. So when would we want an input to our functions? Lets imagine we want to calculate the sum of two numbers. If our numbers are 5 and 5 well that's easy.

```javascript
5+5 // 10
```

But what happens if we don't know what our numbers are? How could we possibly do this? Better yet, what if we want to do 4+6, and 2+8 and 7+3...we would have to start writing a whole bunch of code that's not very dry. This is a great example of when we want to add some custom input (which we call parameters or arguments)

So what does a function look like with parameters? Let's write a function called `add` that takes in two values `a` and `b` and returns their sum.

```javascript
function add(a,b){
    return a+b;
}

add(4,6) // 10
add(2,8) // 10
add(7,3) // 10
```

Try to write functions for `subtract`, `multiply`, and `divide`!

#### scope that is created with a function

Now that we have an idea of what functions do - let's talk about what happens when we define variables inside of functions. To do that, we first need to define what `scope` is. 

MDN defines `scope` is "The context in which values and expressions are "visible," or can be referenced". In JavaScript (before ES2015 which is where we will start), there are only 2 kinds of scope - global and function scope. 

The important takeaway here is that - **all variables that defined outside of functions (and inside of functions without the `var` keyword) are declared in the global scope and all variables defined inside of functions can only be accessed by those functions (and any inner functions)**.

Let's see an example

```javascript
var globalVariable = "I live in the global scope"

function makeNewScope(){
    var functionScopeVariable = "I live in the scope of the makeNewScope function";
}

globalVariable // "I live in the global scope"
makeNewScope() // maybe this will define the functionScopeVariable...

functionScopeVariable // This gives us an error! To be specific, a ReferenceError because the functionScopeVariable is not defined.
```

What happens when we remove the `var` keyword?

```javascript
globalVariable = "I live in the global scope" // omitting the var keyword here will not make a difference in terms of the scope of the variable. In fact it is BAD practice to declare variables without the var keyword!

function makeNewScope(){
    functionScopeVariable = "What happens now?";
}

globalVariable // "I live in the global scope"
makeNewScope() // now this will define the functionScopeVariable!

functionScopeVariable // "What happens now?"
```

If we omit the `var` keyword inside of a function, we actually declare that variable in the global scope. While this may seem like the way to go, this is not best practice. If we need to change some variable in a function, we should at least declare it in the global scope and assign it in a function so that our code is more readable.

```javascript
var globalVariable = "I live in the global scope" 
var globalVariableToBeChanged; // we are just declaring the variable now - it's value will be set to undefined

function makeNewScope(){
    globalVariableToBeChanged = "Undefined no more!"; //here we are assigning the value "What happens now" to the globalVariableToBeChanged variable.
}

globalVariable // "I live in the global scope"
makeNewScope() // now this will assign a new value to the globalVariableToBeChanged!

globalVariableToBeChanged // "Undefined no more!"
```

You can read more about scope [here](https://toddmotto.com/everything-you-wanted-to-know-about-javascript-scope/)

#### two different ways of creating functions

We mentioned earlier that there are two ways to create functions. We saw previously that there are two ways to create functions. 

The first is a function declaration:
```javascript
function declaration(){
    return "I am a function expression!"
}
```

The second is a function expression:

```javascript
var expression = function(){
    return "I am a function expression!"
}
```

So what is the difference between these two? One difference is that when we use a function expression, we do not assign a "name" to the function. The second lies in a behavior called "hoisting". It's important to note that `hoisting` is not something the the JavaScript compiler does (you will not see it anywhere in the JavaScript specification). It is just a concept used to explain where/how variables/functions are declared.

#### hoisting

From MDN - Because variable declarations (and declarations in general) are processed before any code is executed, declaring a variable anywhere in the code is equivalent to declaring it at the top. This also means that a variable can appear to be used before it's declared. This behavior is called "hoisting", as it appears that the variable declaration is moved to the top of the function or global code.

When we write code like this:

```javascript
instructor // this will NOT throw an error! 
var instructor = "Elie"
```

What is happening under the hood (REMEMBER - JavaScript does not **actually** rewrite our code or anything like that, this concept of "hoisting" is just a way for use to visualize and understand how the JavaScript compiler works).

```javascript
var instructor;
instructor // this will NOT throw an error! 
instructor = "Elie"
```

This same idea applies in functions (when the `var` keyword is used, if it is not, that variable is inside the global scope.)

```javascript
function displayInstructor(){
    return instructor;
    var instructor = "Elie"    
}
```

So how does this work with function expressions vs declarations?

function declaration:
```javascript
sayHi("Matt") // "Hello Matt"

function sayHi(name){
    return "Hello " + name
}
```

function expression:
```javascript
sayHi("Matt") // Throws an error!

var sayHi = function(name){
    return "Hello " + name
}
```

Why does the function expression do that? Because variables are hoisted to the top! This means our code looks like this:

```javascript
var sayHi;
sayHi("Matt") // Throws an error because undefined is not a function (we are using the type of undefined and trying to invoke it - that's why we get a TypeError)

var sayHi = function(name){
    return "Hello " + name
}
```

You can read more about hoisting [here](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting).

### Exercise

Complete the [Functions and Scope Exercise](https://github.com/rithmschool/prework_exercises/tree/master/functions_exercise)

### Additional Resources

#### [⇐ Previous](./11-nested-data-structures.md) | [Table of Contents](./readme.md) | [Next ⇒](./13-debugging-javascript.md)