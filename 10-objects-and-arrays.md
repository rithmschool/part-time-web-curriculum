#### [⇐ Previous](./09-boolean-logic-and-operators.md) | [Table of Contents](./readme.md) | [Next ⇒](./11-nested-data-structures.md)

# Objects and Arrays

### Objectives:

By the end of this chapter, you should be able to:

- Compare and contrast objects and arrays, and explain good use cases for each one
- Iterate over arrays and objects 
- Add and remove properties/elements from objects and arrays
- Use common methods (such as `splice`, `slice`, `concat`, and `join` to manipulate arrays)
- Explain the difference between passing by value and passing by reference

### Objects

#### Introduction 

Objects are one of the built in types in JavaScript and consist of unordered key-value pairs. Let's look at our first object:

```javascript
var tim = {
    name: "Tim",
    catOwner: true,
    boatOwner: true
}
```

In the object above we have a set of keys (`name`, `catOwner`, `boatOwner`) and values (`"Tim"`, `true` and `true`). It is important to note that the typeof a key in an object is ALWAYS a string.

#### Accessing values in objects

If we want to access values in the object we can do it two different ways: either using brackets (`[]`) or dot notation. Let's take a look at both.

```javascript
var obj = {
    firstName: "Elie",
    lastName: "Schoppik",
    favoriteColor: "purple",
    job: "instructor",
    isDeveloper: true
}

obj.firstName // Elie
obj["lastName"] // Schoppik
obj[favoriteColor] // This gives us an error, because there is no variable called "favoriteColor"!
```

So which one should we use? Well, best practice is to use the dot notation _if you can use it_. But there are cases in which you'll need to use bracket notation. Let's take a look at this example:

```javascript
var obj = {}
var person = "Tom"

obj[person] = "This is a person"
obj[1+1+1] = "Three"

obj 
/* 
{
    Tom: "This is a person"
    3: "Three"
}
*/

obj.3 // Syntax Error! Can't use the dot notation
obj[3] // "Three" - we NEED to use the bracket notation
obj[person] // "This is a person"
obj["Tom"] // "This is a person"
obj.person // undefined
```

In short, use the bracket notation when you need to evaluate some expression or pass in a variable, but when you know the name of the key and it is not a variable or expression, always use the dot notation.

#### Looping over objects

One of the most important ideas in programming is the idea of iteration, or looping. Let's say we want to print out all of the properties in an object. One way we can do this is by printing the values individually, one per line.

```javascript

var obj = {
    firstName: "Elie",
    lastName: "Schoppik",
    favoriteColor: "purple",
    job: "instructor",
    isDeveloper: true
}

obj.firstName
obj.lastName
obj.favoriteColor
obj.job
obj.developer
```

Although this will work, looping is a much better idea - what if we don't know the names of the keys beforehand, or even how many there are? Let's take a look at how we write loops in JavaScript, starting with objects. 

To iterate over objects, we use a `for in` loop.  

```javascript
var instructor = {
    name: "Matt",
    mathWizard: true,
    dogOwner: true
}

for(var key in instructor){
    console.log(instructor[key])
}

// the loop will log:
// "Matt"
// true
// true
```

#### Adding to objects

To add properties or functions (which are sometimes called methods) to our objects, we can use the `.` or `[]` operator (as before, the dot notation is preferred, but not always possible).

```javascript
var obj = {
    name: "Jon Snow",
    watchMember: true
}

obj.gameOfThrones = "awesome"
obj 
/* 
{
    name: "Jon Snow",
    watchMember: true,
    gameOfThrones: "awesome"    
}
*/
```

#### Removing from objects

- using the delete keyword

```javascript
var obj = {
    name: "Elie",
    job: "Instructor"
}

delete obj.job; // returns true

obj
/*
{
	name: "Elie"
}
```

### Arrays

#### Introduction

An array is a special type of object in which the keys are numberical indices which indicate a value's position in the array. Arrays are created using these brackets - `[]`. To access an element in an array, we specify the name of the array followed by the brackets and the position (also called the index) where the element is. **Arrays are zero-based** which means that the first element is accessed at index 0. Let's see some more detail:

```javascript
var arr = [5,3,10]
arr[0] // 5
arr[1] // 3
arr[2] // 10
arr[3] // undefined
arr[1+1] // 10
arr[arr.length-1] // 10
```

### Iterating Through Arrays

#### For loops

One of the most common ways to loop is through the use of a `for` loop. A `for` loop consists of three parts followed by a block of code inside of `{}`

`for (initializer, condition, counter) {}`

`initializer` - where we can declare variables to be used in the loop. We usually declare a variable called `i` which will serve as a counter variable for the number of times that we should loop.

`condition` - this MUST be an expression that returns `true` or `false`. You can read this condition as "Keep looping as long as this condition is true."

`counter` - this is how we change the variables initialized (typically, either by increasing or decreasing them). We commonly increment variables by 1 using the `++` operator and decrement by 1 using `--`.

As long as the condition is true, the code inside the curly braces will run. After running, the counter expression will run, and then the condition will be checked again.

```javascript
// start with a variable called i and set it to 0
// keep looping as long as i is less than 5
// at the end of each for loop, increase the value of i
for(var i=0; i<5; i++){
    console.log(i)
}

// prints out:

// 0
// 1
// 2
// 3
// 4
```

What gets logged if you change `i<5` to `i<10`? If you change `i++` to `i+=3`? Experimenting with the initializer, condition, and counter is a great way to develop your intuition for `for` loops!

#### While loops

Along with `for` loops, we can also use a while loop. Make sure you initialize your counter variable before the loop and ensure that you increment/decrement inside the loop or else you will be stuck in an infinite loop!

```javascript
var i = 0
while(i<5){
    console.log(i)
    i++
}
```

#### Do While Loops

Similar to while loops we can use a do...while loop and specify our condition at the end. Here is an example:

```javascript
var i = 0
do {
    console.log(i)
    i++
} while(i<5)
```

The main difference between a `while` loop and a `do...while` loop is that the code inside of a `do...while` loop is guaranteed to execute at least once. For example:

```javascript
var i = 0
while(i<0) {
	console.log(i)
	i++
}
// nothing is logged, since 0 < 0 is false

var j = 0
do {
	console.log(j)
	j++
} while(j<0)
// 0 gets logged, since the code inside the block runs once 
// before the while condition is checked
```

#### For of Loop

ES2015 (the newest version of JavaScript) gives us a new way to iterate through arrays using what is called a `for...of` loop. This iterates through the _values_ in an array, rather than the _indices_. Here is an example:

```javascript
for(var i of [4, 5, 3, 1, 2]){
    console.log(i)
}
// 4
// 5
// 3
// 1
// 2
```

#### Exiting out of loops

Sometimes we want to exit a loop before it has finished. To do that, we use the word `break`

```javascript
for(var i = 0; i<5; i++){
    if(Math.random() > .5){
        console.log("Breaking out of the loop when i is " + i)
        break;
    }
    else {
        console.log(i)
    }
}
```

We can also go back to the top of the loop using the word `continue`

```javascript
for(var i = 0; i<5; i++){
    if(Math.random() > .5){
        console.log("Skipping the console.log when i is " + i)
        continue;
    } 
    console.log(i)
}
```

### Adding to arrays

There are a number of ways you can add elements to an array.

One way is by setting a value at a certain index in the array.

```javascript
var arr = [1,2,3]
arr[3] = 4
arr // [1,2,3,4]
```

Be careful with this approach, though -- you can add an element at any index, and any elements that don't have values in them will be filled with `undefined` values.

```javascript
var arr = [1,2,3]
arr[5] = "whoa"
arr // [1, 2, 3, undefined, undefined, 5]
```

If you want to add to the end of an array, a better approach is to use the `push` function - this function returns the new length (how many elements are in the array) of the array.

```javascript
var arr = [3, 2, 5]
arr.push(7); // returns the new length, i.e. 4
arr // [3, 2, 5, 7]
```

On the other hand, if you want to add to the beginning of an array, you can use the `unshift` function. As with `push`, `unshift` returns the length of the modified array. 

```javascript
var arr = [1,2,3]
arr.unshift(0); // returns the new length, i.e. 4
arr // [0,1,2,3]
```

### Removing from arrays

We've seen how we can add elements from arrays. But what about removing elements? 

One (not common) way to remove elements is to manually set the length of the array to a number smaller than its current length. For example:

```javascript
var arr = [1,2,3]
arr.length = 2 // returns the new length
arr // [1,2]
```

A more common way to remove elements from the back of an array is to use `pop()`. This function works in sort of the opposite way as `push`, by removing items one by one from the back of the array. Unlike `push`, however, `pop` doesn't return the length of the new array; instead, it returns the value that was just removed.

```javascript
var arr = [1,2,3]
arr.pop() // returns 3
arr // [1,2]
```

If you want to remove an element from the _front_ of an array, you should `shift()` (like `unshift`, but the opposite)! As with `pop()`, `shift()` returns the removed value.

```javascript
var arr = [1,2,3]
arr.shift(); // returns 1
arr // [2,3]
```

Arrays in JavaScript are objects, which means that we can also use the `delete` keyword. However, this approach should usually be avoided with arrays, because deleting an element from an array doesn't actually change the length of the array. Instead, the value at the index where you delete will simply be replaced by `undefined`.

```javascript
var arr = [5, 4, 3, 2]
delete arr[1]
arr // [5, undefined, 3, 2]
```

### Removing/Adding or both with splice

One of the more powerful array methods is `splice`, which allows you to either add to an array or remove elements or even do both! You can think of `splice` as a powerful generalization of `push`, `pop`, `unshift`, and `shift` all in one!

The splice method accepts at least two arguments. The first argument is the starting index, indicating where values will be removed or added. The second parameter is the number of values to remove. Optionally, you can pass in an unlimited number of additional arguments; these correspond to values you'd like to add to the array. The splice method always returns an array of the **removed** elements. Here are some examples:

```javascript
var arr = [1,2,3,4]
arr.splice(0,1) // returns [1]
arr // [2,3,4]
```

```javascript
var arr = [1,2,3,4]
arr.splice(0,1,5) // returns [1]
arr // [5,2,3,4]
```

```javascript
var arr = ["a","b","c","d"]
arr.splice(1,2,"x","y","z") // ["b", "c"]
arr // ["a", "x", "y", "z", "d"]
```

### Common array functions and properties

- `length ` - returns how many elements are in the array. This is a property, NOT a function (you can tell because we type `length`, not `length()`. As we've seen, it can (but is almost never) be used to remove elements/clear an array.

```javascript
var arr = [1,2,3,4] 
arr.length // 4
arr[arr.length] // undefined
arr[arr.length-1] // 4 - this is a nice way to access the last element of an array when you don't know how many elements are inside it.
```

- `slice` - makes a copy of an array. We can use it to copy the entire array, or create a copy of a _subarray_. If we just invoke `slice()` with no arguments, we'll create a copy:

```javascript
var arr = [1,2,3,4]
var copy = arr.slice()
```

Alternatively, you can pass in two arguments to `slice`. Like `splice`, the first argument indicates the starting index of the subarray you want. The second argument indicates the ending index. The subarray you get will consist of all the values starting from the starting index and going up to (but **not including**) the ending index:

```javascript
var arr = [7, 6, 5, 4, 3, 2]
arr.slice(1, 2) // [6]
arr.slice(2, 5) // [5, 4, 3]
arr.slice(2, 1) // []
```

- `concat` - joins two arrays together.

```javascript
var arr1 = [1,2,3]
var arr2 = [4,5,6]
var combined = arr1.concat(arr2)
```

- `join` - joins elements of an array into a string separated by a delimiter

```javascript
var arr = ["Hello","World"]
arr.join(" ") // "Hello World"

var arr2 = ["I", "have", "a", "big", "announcement"]
arr.join("! ") + "!" // "I! have! a! big! announcement!"
```

- `indexOf` - finds the first index of the element passed in (starting from the left). If the element is not found, it returns -1.

```javascript
var arr = [1,2,3,4,5,4,4]
arr.indexOf(2) // 1
arr.indexOf(3) // 2
arr.indexOf(1) // 0 - remember, arrays are zero indexed
arr.indexOf(4) // 3 - indexOf stops once it finds the first 4.
arr.indexOf(10) // -1
```

- `lastIndexOf` - just like `indexOf`, but starts from the end of the array.

```javascript
var arr = [1,2,3,4,5,4,4]
arr.indexOf(2) // 1
arr.indexOf(3) // 2
arr.indexOf(1) // 0 
arr.indexOf(4) // 6 - this one is different now!
arr.indexOf(10) // -1
```

- `fill` - a new function in ES2015, `fill` fills in values in an array. It takes at least one argument, which represents the value with which you want to fill in the array.

```javascript
var arr = [1,2,3,4]
arr.fill(10) // [10,10,10,10]
```

Optionally, you can also pass in start and end values to restrict what part of the array you wish to fill.

```javascript
var arr = [1, 2, 3, 4]
arr.fill("hi", 1, 3) // [1, "hi", "hi", 4]
```

- `Array.isArray` - returns `true` if the value passed in is an array, returns `false` if not.

```javascript
var arr = []
var obj = {}

Array.isArray(arr) // true
Array.isArray(obj) // false
Array.isArray("") // false
Array.isArray(false) // false
Array.isArray([false]) // true
```

### Reference vs Value

An essential distinction between primitives and objects as how their values are passed when assigned to new variables. Let's examine the following example:

```javascript
var instructor = "Elie";
var anotherInstructor = instructor;
anotherInstructor = "Matt";

instructor; // "Elie"
anotherInstructor; // "Matt"
```

In this example, even though we changed the `anotherInstructor` variable, it did not affect the `instructor` variable. This is because each one of these primitive types have a specific address in memory (it is a bit more complex than that, but we'll keep things simple to start).

Now let's take a look at an object (which is not a primitive):

```javascript
var instructor = {
    firstName: "Elie"
};

var anotherInstructor = instructor;
anotherInstructor.firstName = "Matt"

instructor.firstName // Matt
anotherInstructor.firstName // Matt

```

We see here that the properties of the original instructor variable were changed as well! This is because the `anotherInstructor` did not create a new object, it just created a reference (or pointer) to the `instructor` object.

How about arrays? What do you think will happen here:

```javascript
var arr = [1,2,3];
var anotherArr = arr;

anotherArr.push("New Value")
anotherArr // [1,2,3,"New Value"]

arr // [1,2,3,"New Value"]
```

The `arr` variable was overwritten! Why did that happen? Remember, that arrays are just a special type of object! A quick `typeof []` will show us that this is the case.

You can read more about it [here](http://stackoverflow.com/questions/518000/is-javascript-a-pass-by-reference-or-pass-by-value-language) and [here](http://stackoverflow.com/questions/6605640/javascript-by-reference-vs-by-value)

### Exercise

- Complete the [Objects and Arrays Exericse](https://github.com/rithmschool/prework_exercises/tree/master/objects_and_arrays_exercise)

### Additional Resources

#### [⇐ Previous](./09-boolean-logic-and-operators.md) | [Table of Contents](./readme.md) | [Next ⇒](./11-nested-data-structures.md)