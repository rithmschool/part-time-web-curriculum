#### [⇐ Previous](./12-functions-and-scope.md) | [Table of Contents](./readme.md) | [Next ⇒](./14-timers-and-callbacks.md)

# Debugging JavaScript

### Objectives:

By the end of this chapter - you should be able to

- List common errors in JavaScript and how they created
- Utilize the sources tab for debugging, setting breakpoints and adding snippets
- Step into and through functions to better debug
- Use try/catch statements to handle errors gracefully and throw errors when necessary
- Install eslint and configure Sublime Text 3 to use eslint

#### How Errors work in JavaScript

All errors in JavaScript are actually `objects` that are created by a function called `Error`. You can read more about it [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error). As MDN says - error objects are thrown when runtime errors occur. The Error object can also be used as a base object for user-defined exceptions (which means we can create our own errors).

#### Common JS Errors

- SyntaxError - when we make a mistake with our syntax;

```javascript
var x = "hello

var wrongObj = {
    name: "foo"
    missingComma: true
}
```

- ReferenceError - when we try to access a variable that does not exist in that scope 

```javascript
amazing; // ReferenceError - does not exist in the global scope

function defineSomething(){
    var secret = "I'll never tell";
}

defineSomething();

secret // ReferenceError - only exists in the scope of the defineSomething function
```

- TypeError - occurs when you make incorrect use of certain types in javascript. Here are some very common examples (many of them we guarantee you will make!)

```javascript
undefined() // TypeError - undefined is NOT a function!

var obj = {
    name: "Elie"
}

obj.something // this actually returns undefined! What does that tell us? If you try to access a property on an object and it does not exist, you do NOT get a ReferenceError, you just get undefined

obj.something.foo // but when you try to access a property on `undefined`....well that's a TypeError
```

- RangeError - this happens when we have a function that calls itself (also known as a recursive function), but if we have too many functions that have been called (before they are returned) we run out of memory and cause a RangeError.

```javascript
function callMe(){
    callMe()
}

callMe(); // maximum call stack size exceeded. We will talk more about the call stack and recursion in a later section.
```

#### Adding snippets to the sources tab

In the chrome console, there is a wonderful way to write pieces of code that allow us to easily use the more advanced debugging tools in chrome. If you open up the dev tools (`command + option + j`) and head to the `Sources` tab. You will see a panel on the left with three column names (you might have to drag it out a bit). These names are (`Sources`, `Content scripts` and `Snippets`). The tool we will be using are Snippets.

Click on the `Snippets` panel and inside, right click and select `New`. You can then name your snippet - let's call this one `first snippet`. Inside of here you will see the middle pane is empty so let's write some JavaScript inside of here. We'll use this example:

```javascript
var instructor = "Matt"

instructor = "Elie"

function defineNewInstructor(){
    var newInstructor = "Melissa"
    var secondNewInstructor = "Samantha"
}

defineNewInstructor();
```

#### Debugging with the sources tab and external files

LINK TO VIDEO

#### Catching Errors in JavaScript

Sometimes we don't know if our code is going to error out or not, so instead of our code crashing and not continuing to run, we might want to gracefully handle our errors.

```javascript
try {
    thisDoesNotExist;
}
catch(e){
    console.log("The error is ", e)
}
```

Let's look at another example:

```javascript
try {
    if(Math.random() >= .5) {
        throw "Let's make an error!"    
    }
    console.log("Whew...we made it")
}
catch(e){
    console.log("The error is ", e)
}

console.log("Moving on.....")
```

All we are doing here is generating a random number between 0 and 1 and if it is >= .5 - we create an error so we move to the catch. However, our code continues to run even if an error happens. So - what does the `throw` keyword do?

#### Installing ESLint

ESLint is a wonderful tool that helps to lint (check your code for errors) your code as you type and let's you know about any mistakes/bad practices you may be making.

To install it:

- anywhere in the terminal, run `npm install -g eslint` (if you get an error, try again with `sudo npm install -g eslint` and then type in your password to log in to your computer, and press enter)
- in your home (`~`) directory, create a file called `.eslintrc`
- inside of this file, add the following text and then save and close the file

```json
{
 "parser": "babel-eslint",
  "ecmaFeatures": {
    "modules": true,
    "experimentalObjectRestSpread": true
  },
  "env": {
    "amd": true,
    "browser": true,
    "es6": true,
    "mocha": true,
    "node": true
  },
  "globals": {
    "$": true
  }
}
```

- In sublime install a package called `SublimeLinter` (press in `command + shift +p`, type in `install` and press enter, when the list pops up, type in`SublimeLinter` and press enter)
- In sublime install a package called `SublimeLinter-contrib-eslint` (same steps as above but a different package name)

Once you have installed both of these, close sublime (`command + q`) and open it up again. In a javascript file, try to type some code and if you do anything incorrectly or if there is a warning you will see a red/yellow mark appear in your editor. When you see this - you have installed it correctly!

You can read more about the setup [here](http://jonathancreamer.com/setup-eslint-with-es6-in-sublime-text/) or [here](https://medium.com/@dan_abramov/lint-like-it-s-2015-6987d44c5b48#.gdhyjbh1w)

### Exercise

Complete the [Debugging Exercise](https://github.com/rithmschool/prework_exercises/tree/master/debugging_exercise)

### Additional Resources

#### [⇐ Previous](./12-functions-and-scope.md) | [Table of Contents](./readme.md) | [Next ⇒](./14-timers-and-callbacks.md)