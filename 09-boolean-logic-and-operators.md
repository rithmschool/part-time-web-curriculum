#### [⇐ Previous](./08-variables-and-data-types.md) | [Table of Contents](./readme.md) | [Next ⇒](./10-objects-and-arrays.md)

# Boolean Logic and Operators

### Objectives:

By the end of this chapter, you should be able to:

- Write conditional logic using boolean operators
- List all of the falsey values in JavaScript
- Use if/else and switch statements to include conditional logic in your JavaScript code

### Boolean Logic

An essential part of writing programs is being able to execute code that depends on certain conditions. The way we write conditional logic is by using booleans and boolean logic (`true` or `false`). To write conditional logic we can use `if` statements and `switch` statements. 

An if statement looks something like this: 

```javascript
var instructor = "Elie"

// we begin with an "if" statement followed by a condition in () and a block of code inside of {}
if(instructor === "Elie") {
    console.log("Yes!")
}
else {
    console.log("No")
}
```

Notice that we used a `===` instead of `=`. Anytime that we use more than one equals operator (we can either use `==` or `===`) we are doing what is called **comparison** (comparing values). When we use a single equals operator `=`, we are doing what is called **assignment** (setting a variable equal to some value). 

What's the difference between `==` and `===`, you ask? Great question! We'll get to that down below. For now, though, it might be helpful to play around with these operators in the Chrome console, and see if you can come up with a guess as to how these operators behave differently.

```javascript
var number = 55

// we begin with an "if" statement followed by a condition in () and a block of code inside of {}
if(number == "55") {
    console.log("Yes!")
}
else {
    console.log("No")
}
```

### Falsey Values

Another essential concept to understand in JavaScript is that some values (aside from `false`) are actually false as well, when they're used in a context where JavaScript expects a boolean value! Even if they do not have a "value" of false, these values will be translated (or "coerced") to false when evaluated in a boolean expression. 

In JavaScript there are 6 falsey values: 

- `0`
- `""`
- `null`
- `undefined`
- `false`
- `NaN` (short for not a number)

If you ever want to determine if a value is truthy or falsey, you can prefix it with `!!`.

What do these values return?

`!!false`
`!!-1`
`!!-`
`!![]`
`!!{}`
`!!""`
`!!null`

You can read more about these [here](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)

### Difference between `==` and `===`

In JavaScript we have two different operators for comparison, the double and triple equals. Both operators check whether the two things being compared have the same value, but with one important difference: `==` allows for type coercion of the values, while `===` does not. So to understand the difference between these operators, we first need to understand what is meant by type coercion. 

Consider the following examples:

```javascript
// 1. 
5 + "hi" // "5hi"

// 2. 
if ("foo") {
  console.log("this will show up!");
}  

// 3.
if (null) {
  console.log("this won't show up!");
}

// 4.
+"304" // 304
```

Let's figure out what's happening in each of these examples. In the first one, you've asked JavaScript to add a number and a string. In a lot of programming languages, this would throw an error, but JavaScript is more accomodating! It evaluates the expression 5 + "hi" by first _coercing_ 5 into a string, and then interpreting the "+" operator as string concatenation. 

The next two examples show a similar sort of _coercion_. JavaScript expects the values inside of parentheses that come after the keyword `if` to be booleans. If you pass in a value which is not a boolean, JavaScript will _coerce_ the value to a boolean according to the rules for truthy/falsey values defined above. Since "foo" is not a falsey value, it will be coerced to `true`, which is why the second example logs something to the console. `null`, however, is a falsey value, so it gets coerced to false and nothing shows up in the third example.

The last example shows a very common way to coerce a stringified number back into a number. By prefacing the string with the plus sign, JavaScript will perform a _coercion_ on the value and convert it from a string value to a number value.

In essence, then, coercion is just the process of converting a value from one type to another. JavaScript using coercion pretty liberally among programming languages, so if you don't understand how coercion in JavaScript works, it can be easy to introduce bugs into your code.

But what does all of this have to do with `==` and `===`? Let's look at some examples:

```javascript
5 == "5" // true
5 === "5" // false
"true" === true // false
"true" == true // false
true == 1 // true
true === 1 // false
undefined === null // false
undefined == null // true
```

What's going on here? Let's deal with the expressions involving `===` first. As you can see, the expressions `5 === "5"`, `"true" === true`, `true === 1`, and `undefined === null` all evaluate to `false`. In some sense, perhaps this shouldn't be so surprising: none of the values being compared are the same! One way to think about this is to recall the types of the primitives being compared. In the first case, we're comparing a number to a string; in the second case, a boolean and a string; in the third case, a boolean and a number; and in the last case, `undefined` and `null`. How can these values be the same when the primitives involved aren't even of the same type?? 

From the above examples, you can see that the `==` operator is a little less strict (in fact, `===` is sometimes referred to as the "strict" equality operator, while `==` is sometimes referred to as the "loose" equality operator). The reason that comparisons like `5 == "5"` evaluate to true is because `==` allows for type coercion!

But what gets coerced? Does `5` become `"5"` or does `"5"` become `5`? In this case, according to the specification the string gets coerced into a number, not the other way around. This might seem like an unimportant detail, but there are a couple of gotchas in the way coercion works that can be confusing when you first encounter them. 

For example, it might seem like `"true" == true` should evaluate to `true`, since `"true"` is a truthy value! But in fact, what actually happens is that the boolean `true` gets coerced to a number (1), and then `"true"` is compared to `1`, which returns false. (This is also why `true == 1` evaluates to `true`.)

It's less important to memorize these rules for how coercion works with `==` than to recognize that `==` allows for coercion while `===` doesn't. If you don't want to have to think about coercion in your comparisons, stick to `===`.

### If / else statements

We previously saw what an `if` statement looks like. Let's examine this a bit more:

```javascript
var x = 4
if(x <= 5){
    console.log("x is less than or equal to five!")
}
else {
    console.log("x is not less than five!")   
}
```

We saw before that we can use `==` or `===` to compare values. We can also check for inequality, using 

 `<` - less than,
 
 `<=` - less than or equal to, 
 
 `>` - greater than, 
 
 `>=` - greater than or equal to,
  
 `!=` - not equal (loose), and 
 
 `!==` - not equal (strict). 

### !, || and &&

In our conditions (and assignments) we can use certain logical operators to write more complex statements. Here are some other useful operators:

`!` - the **not** operator, which flips the boolean value (`!true === false`)

`||` - the **or** operator, which in a boolean context returns true if either condition is true

`&&` - the **and** operator, which in a boolean context returns true if both conditions are true

what do the following expressions return?

```javascript
true && false  
false || true 
!false && true

var number = 10
number > 20 || number === 10
number > 20 && number < 15
```

Let's look at another example - walk through what is happening here.

```javascript
var x = Math.random();
if(x > .66){
    console.log("x is greater than .66")
}
else if (x > .33 && x <= .66) {
    console.log("x is between .33 and .66!")   
}
else {
    console.log("x is less than .33")      
}
```

We've essentially built some pretty decent logic for randomly choosing 1 of three options. This will be useful when building an AI for a future assignment (rock/paper/scissor)

You can read more about logical operators [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators).

### Switch statements

Another way to write conditional logic is to use a `switch` statement. While these are used less frequently, they can be quite useful when there are multiple conditions that can be met. Notice that each `case` clause needs to end with a `break` so that we exit the `switch` statement. Here is an example:

```javascript
var instructors = ["Elie", "Matt", "Tim"];
var randomIndex = Math.floor(Math.random()*instructors.length-1);

switch(randomIndex){
    case 0:
        console.log("You got Elie!");
        break;
    case 1:
        console.log("You got Matt!");  
        break;
    default:
        console.log("You got Tim!"); 
}
```

### Exercise

Answer the following questions:

- What is a falsey value? List all the falsey values in JavaScript.
- Research `Math.random` [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random) and write an if statement that console.log's "Over .5" if Math.random returns a number greater than `.5`. Otherwise console.log "Under .5".

### Additional Resources

#### [⇐ Previous](./08-variables-and-data-types.md) | [Table of Contents](./readme.md) | [Next ⇒](./10-objects-and-arrays.md)