#### [⇐ Previous](./13-debugging-javascript.md) | [Table of Contents](./readme.md) | [Next ⇒](./15-introduction-to-the-dom.md)

# Timers, Callbacks and Closures

### Objectives:

By the end of this chapter - you should be able to

- Use setTimeout and setInterval for timing future execution 
- Compare and contrast synchronous vs. asynchronous code 
- Diagram the call stack, heap and queue and explain how the event loop works

#### setTimeout + setInterval

It's quite common to write code that we want to be executed after a specific amount of time. To do this, we use the `setTimeout` and `setInterval` functions. Both of these functions are attached to the `window`, but `setTimeout` will only run the function to be executed once, whereas setInterval will run it an infinite amount of times (until the timer is cleared)

```javascript
setTimeout(function(){
    console.log("Hello!")
},1000)
```

This will log out `Hello` after one second! But what happens if we want to stop the timer? Well, `setTimeout` and `setInterval` `return` a special value called a timer `id`. If we pass this value in to the `clearTimeout` or `clearInterval` method - we can stop our timer!

```javascript
var timerId = setTimeout(function(){
    console.log("Hello!")
},1000)

clearInterval(timerId);
```

What is this code doing?

```javascript
var timerId = setInterval(function(){
    console.log("HI!")
},1000)

setTimeout(function(){
   clearTimeout(timerId)
},3000)
```

We can see that each of these functions `setTimeout` and `setInterval` take in as their first parameter a function! This is actually something special about JavaScript, not all languages allow us to pass as parameters to functions - other functions! The function that is passed as a parameter to another function is called a `callback`

#### Callbacks

So we just defined callbacks as functions that are passed as a parameters to other functions, and we saw that `setTimeout` and `setInterval` (which are functions on their own), take in as their first parameter a function, but we can also write our own callbacks to help with re-usability of functions.

```javascript
function add(a,b){
    return a+b
}

function subtract(a,b){
    return a-b
}

function math(a,b,callback){
    return callback(a,b);
}

math(1,4,add) // returns 5
math(5,5,subtract) // returns 0
```

Let's try to write a function called `each` which loops over an array and runs a function on each element in it! Try to do this before you look at the solution 

```javascript
function each(array, callback){
    for(var i=0; i< array.length; i++){
        callback(array[i])
    }
}

function printValues(val){
    console.log(val)
}

function printDoubledValues(val){
    console.log(val*2)
}

function printTripledValues(val){
    console.log(val*3)
}

each([1,2,3], printValues)
// 1
// 2
// 3

each([1,2,3], printDoubledValues)

// 2
// 4
// 6

each([1,2,3], printTripledValues)

// 3
// 6
// 9
```

Callbacks are a very powerful tool as they enable us to manage `asynchronous` code - or code that will be executed at a later point in time (that is not always specified).

#### Asynchronous Code

Before we examine asynchronous code - let's understand a fundamental concept about JavaScript - that it is **single threaded**. What this means is that only one process will happen at a time. Unlike other languages where you can create your own threads (a process called `multi-threading`) - JavaScript can not do that. However, we can write asynchronous code (which may give the impression that multiple things are happening at once, but that is not the case).

#### How JS manages asynchronous code

In order to understand how JavaScript manages asynchronous code - we first need to define a few terms:

`call stack` - where function calls are put (each one is called a "stack frame"). The stack is a LIFO (last-in-first-out) data structure. You can think of the stack like a stack of cups (last one you put on the stack is the first one that comes off). What that means is that if there is a function on the stack and it is under another function, it can never execute until the function on top has returned (either by the `return` keyword or finishing all the code in the function).

`event queue` - When an asynchronous event occurs, it gets put into what is called the "queue" (also known as the event queue). It is then moved to the stack when the stack is clear (no functions on the stack). MDN defines the queue as "a list of messages to be processed. To each message is associated a function. When the stack is empty, a message is taken out of the queue and processed. The processing consists of calling the associated function (and thus creating an initial stack frame). The message processing ends when the stack becomes empty again. The queue is a FIFO data structure (first-in-first-out).

`heap` - where objects are stored. The heap is an unstructured/unorganized region of memory.

JavaScript internally has something called the "Event Loop", which checks the queue and sees if there are any processes to execute. 

Let's examine the event loop in action:

```javascript
console.log("first")
setTimeout(function(){
    console.log("second")
},0)
console.log("third")
```

When we run this code, we would expect it to log out "first", "second" and "third", but that's not what happens! It logs "first", "third", "second".

That's because this is what happens

- the `log` function goes on the stack and it prints out "first" and then it goes off
- a message is sent to the queue to execute "second" in 0 milliseconds
- during that time, another `log` function comes on the stack and prints out "third"
- now the stack is clear so another `log` goes on the stack and "third" is printed

You can read all about it [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)

#### Immediately Invoked Function Expressions (IIFEs)

```javascript

(function(){
    var person = "Elie"
    return person;
})();

var personObject = (function invokeRightAway(){
    var person = "Elie"
    return {
        getName: function(){
            return person;
        },
        setName: function(newName){
            person = newName;
        }
    };
})();

personObject.getName() // "Elie"
personObject.setName("Mary") // 
personObject.getName() // "Mary"
```

So we can use IIFE's to protect our variables (from the global scope), but what is pretty interesting here is that even though our function called `invokeRightAway` finished running, we were still able to access variables from that function inside of the `getName` and `setName` method. How is that possible? Well, through the use of something called `closure`.

#### Closure

One of the most difficult concepts to understand when first learning JavaScript is the idea/phenomena of `closure`. Let's take a stab at a definition:

<blockquote>Closure is when a function is able to access variables from an outer function that has already returned.</blockquote>

Thanks to JavaScript's inner workings, a function is able to remember variables defined in parent functions even if that function has returned.

#### Closures in the wild

- private variables

```javascript
function defineAge(){
    var age = 28;
    return function growUp(){
        return ++age
    }
}

var ageOnce = defineAge();
ageOnce() // 29
ageOnce() // 30
```

So who can access our "age" variable? Only the defineAge function which has returned and the growUp function which through the use of closure, has access to the age variable (defined in an outer function that has already returned). Our `age` variable is now protected and no one can gain access to it!

Let's look at another example:

```javascript
function createInstructors(){
    var instructors = ["Elie", "Matt", "Tim"]
    return {
        showInstructors: function displayAllInstructors(){
            return instructors;
        },
        addInstructor: function addNewInstructor(instructor){
            instructors.push(instructor)
            return instructors;
        }
    }
}

var firstClass = createInstructors()
firstClass.addInstructor("Jennifer")
firstClass.showInstructors // ["Elie", "Matt", "Tim", "Jennifer"]

var secondClass = createInstructors()
secondClass.addInstructor("Ashley") // ["Elie", "Matt", "Tim", "Ashley"]

// on one line

var instructors = createInstructors().showInstructors(); ["Elie", "Matt", "Tim"]
```

Now that one line we just wrote was pretty neat! `var instructors = createInstructors().showInstructors();`, but could we do better? What if we do not want to call `createInstructors` every time so we could write something like `createInstructors.showInstructors()`. To do that, we can use IIFEs!

```javascript
var instructorModule = (function createInstructors(){
    var instructors = ["Elie", "Matt", "Tim"]
    return {
        showInstructors: function displayAllInstructors(){
            return instructors;
        },
        addInstructor: function addNewInstructor(instructor){
            instructors.push(instructor)
            return instructors;
        }
    }
})();
```

What we have just created is a small `module`, which is a piece of code that is encapsulated and can be reused quite easily. The pattern we just used to write our code is famously called the module pattern! It's a great way to wrap everything in an IIFE that contains private data that can not be accessed globally. We can even refactor this more so that our logic is not in the `return` statement.

```javascript
var instructorModuleRefactored = (function createInstructors(){
    var instructors = ["Elie", "Matt", "Tim"]
    function displayAllInstructors(){
        return instructors;
    }
    function addNewInstructor(instructor){
        instructors.push(instructor)
        return instructors;
    }
    return {
        showInstructors: displayAllInstructors,
        addInstructor: addNewInstructor
    }
})();
```

### The arguments array (well not exactly...)

Every single time that a function is called - we get access to a special keyword called `arguments` which looks like an array (it is not EXACTLY an array, but we will cover the reason why a bit later) and can be accessed using `[]` notation. Here is an example

```javascript
function add(){
    console.log(arguments)
}

add(2,2) // [2,2]
add(10,5) // [10,5]
add(1) // [1]

function displayFirstArgument(){
    return arguments[0]
}

displayFirstArgument(10,20) // [10]
displayFirstArgument(true) // [true]
displayFirstArgument() // []
```


### Exercise

Complete the [Timers and Callbacks Exercise](https://github.com/rithmschool/prework_exercises/tree/master/timers_and_callbacks_exercise)

### Additional Resources

[http://javascript.info/tutorial/events-and-timing-depth](http://javascript.info/tutorial/events-and-timing-depth)

#### [⇐ Previous](./13-debugging-javascript.md) | [Table of Contents](./readme.md) | [Next ⇒](./15-introduction-to-the-dom.md)