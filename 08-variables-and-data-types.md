#### [⇐ Previous](./07-javascript-introduction-and-history.md) | [Table of Contents](./readme.md) | [Next ⇒](./09-boolean-logic-and-operators.md)

# Variables and Data Types

### Objectives:

By the end of this chapter, you should be able to:

- List all of the data types in JavaScript
- Compare and contrast primitive data types with objects
- Initialize and assign variables in JavaScript

### Variables

- In JavaScript, you initialize variables using the `var` keyword. Strictly speaking, using this keyword is not necessary, but in practice it should almost always be there (we'll discuss why a bit later).

### Primitive Data Types in JavaScript

JavaScript has 6 primitive data types - let's see what those look like:

- string - `var greeting = "hello";`
- number - `var favoriteNum = 33`;
- boolean - `var isAwesome = true;`
- undefined - `var foo;` or `var setToUndefined = undefined;`
- null - `var empty = null`
- symbol - `var sym = Symbol()`

JavaScript is known as a "weakly" typed language. What this means is that when you create variables and assign them to values, you do not have to specify the type of data you are working with. In statically (or strongly) typed languages, like Java and C++, you do need to specify the type.

#### Objects

In JavaScript, along with primitives we have objects. We will discuss the difference between objects and primitives later on, but for now let's see what an object (a set of key-value pairs) looks like.

```javascript
var firstObj = {
    firstName: "Elie",
    lastName: "Schoppik",
    isInstructor: true
}
```

In this object, we have `keys` of "firstName," "lastName," and "isInstructor" and values of "Elie," "Schoppik," and true. Note that **ALL** keys in JavaScript objects are strings.

To access values in an object, we can either use the `dot` notation, as in `firstObj.firstName` or we can use brackets, as in `firstObj["firstName"]`. We will learn the difference between these two later on.

#### Figuring out a variable's type in JavaScript 

In JavaScript, we have a keyword called `typeof` that returns the type of the variable. While this seems pretty fool-proof, there are some quirks that we should be aware of. In the Chrome console, let's type out each one of these:

- `typeof ""` - "string"
- `typeof 5` - "number"
- `typeof false` - "boolean"
- `typeof Symbol()` - "symbol"
- `typeof undefined`  - "undefined"
- `typeof null` // hmmm, this is not what we expect, it returns "object"!
- `typeof typeof {}` // typeof always returns a string! 

### Exercise

1. Create the following variables
    - `name`, which is a string set to your current name
    - `dayOfBirth`, which is a number set to the day of your birth month
    - `details`, an object that has three keys
        - favoriteColor (set to your favorite color)
        - favoriteSnack (set to your favorite snack)
        - favoriteBeverage (set to your favorite beverage)
2. See what happens when you have multiple variables of the same name. Which one takes precedence? 
3. What is the difference between null and undefined?
4. What is `NaN` in JavaScript? What is the `typeof NaN`? 
5. You can declare a variable by typing `var thing;`. What is the value of `thing`?

### Additional Resources

#### [⇐ Previous](./07-javascript-introduction-and-history.md) | [Table of Contents](./readme.md) | [Next ⇒](./09-boolean-logic-and-operators.md)