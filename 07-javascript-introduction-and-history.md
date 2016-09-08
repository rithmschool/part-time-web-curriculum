#### [⇐ Previous](./06-css-part-3.md) | [Table of Contents](./readme.md) | [Next ⇒](./08-variables-and-data-types.md)

# Introduction to JavaScript

### Objectives:

By the end of this chapter, you should be able to:

- Define what JavaScript is, where it can be used, and how it came to be
- Describe the evolution of JavaScript and how it has changed rapidly
- Include a script in an application

### A very brief Introduction to JavaScript

From [W3C](https://www.w3.org/community/webed/wiki/A_Short_History_of_JavaScript):

>JavaScript, not to be confused with Java, was created in 10 days in May 1995 by Brendan Eich, then working at Netscape and now of Mozilla. JavaScript was not always known as JavaScript: the original name was Mocha, a name chosen by Marc Andreessen, founder of Netscape. In September of 1995 the name was changed to LiveScript, then in December of the same year, upon receiving a trademark license from Sun, the name JavaScript was adopted. This was somewhat of a marketing move at the time, with Java being very popular around then.

### ECMAScript

From [Wikipedia](https://en.wikipedia.org/wiki/ECMAScript#ECMAScript_Harmony):

>ECMAScript (or ES) is a trademarked scripting-language specification standardized by Ecma International. Well-known implementations of the language, such as JavaScript, JScript and ActionScript have come into wide use for client-side scripting on the Web.

From [JavaScript: How Did We Get Here?](http://archive.oreilly.com/pub/a/javascript/2001/04/06/js_history.html)

>The introduction of IE3 and its unfortunate lack of support for the document.images array led Netscape and Sun to standardize the language with help from the European Computer Manufacturers Association (ECMA), giving us yet another name for what had by now become a strange hybrid of powerful and universally supported core functionality and often incompatible object models: ECMAScript. Standardization was begun in conjunction with ECMA in November 1996 and adopted in June 1997 by ECMA and by ISO in April 1998.

JavaScript standardization is now run by a committee called TC39, which governs how ECMAScript features are designed, starting with ECMAScript 2016 (or what is called ES2016).

### Where we will be writing most of our SHORT JavaScript

For most of our short JavaScript examples, we will be using the Chrome console. To open up the console press `Option + Command + j ` or right click, select Inspect, and then move to the tab called `Console`.

Inside of this console you can write JavaScript! So let's start by declaring a variable called `first` and setting it equal to the string "Hello World" 

`var first = "Hello World"`

After you type this, press enter and now we can type in `first` in the console and see our variable - try to declare a couple more!

As you start typing more in the console, you will see it begins to fill up quickly. If you would like to clear the console you can either type in `clear()` and press enter or press `command + k`.

### Writing longer scripts

To write longer scripts we will use a `<script></script>` tag in our HTML files. Similar to our CSS, we can either include a `<script></script>` tag in our HTML and place JavaScript inside of it, or we can use a `<script></script>` tag to link to an external file. Here are two examples:

```html
<!-- option 1 -->
<script>
    var firstName = "Elie"
    console.log(firstName) // since we are outside of the Chrome console, we need to use console.log to print out data to the console (we can't just put 'firstName')
</script>

<!-- option 2 -->

<script src="first.js"></script>
```

And for option 2 - imagine we have a file called `first.js`. Inside of this file we would have:

```javascript
var firstName = "Elie"
console.log(firstName)
```

These examples also illustrate a common convention when writing JavaScript: when declaring variables using multiple words, the standard is to capitalize each word after the first word, and otherwise use lower-case letters (e.g. `firstName`, not `firstname`, `first_name`, `FirstName`, or some other variation). This casing convention is called camel case, and while your JavaScript code will work just fine if you don't abide by this convention, it's good to get in the habit of camel casing your variables.
 
### Exercise

- What is the difference between JavaScript and ECMAScript?
- Who is Brendan Eich?
- How do you hide and show the Chrome console?
- Create a simple page with a script tag. Inside of the script tag declare a couple of variables and then log their values to the console.
- Research alert, prompt and confirm - what do they do?

### Additional Resources

#### [⇐ Previous](./06-css-part-3.md) | [Table of Contents](./readme.md) | [Next ⇒](./08-variables-and-data-types.md)