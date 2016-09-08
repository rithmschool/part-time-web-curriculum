#### [⇐ Previous](./15-introduction-to-the-dom.md) | [Table of Contents](./readme.md) | [Next ⇒](17-jQuery-events.md)

# Introduction to the DOM

### Objectives

By the end of this chapter - you should be able to

- Explain in your own words, what the DOM is and how it is created
- Use the document object to manipulate the DOM
- Iterate over elements and add attributes 

### What is the DOM

From MDN: 

"The Document Object Model (DOM) is a programming interface for HTML, XML and SVG documents. It provides a structured representation of the document as a tree. The DOM defines methods that allow access to the tree, so that they can change the document structure, style and content. The DOM provides a representation of the document as a structured group of nodes and objects, possessing various properties and methods. Nodes can also have event handlers attached to them, and once an event is triggered, the event handlers get executed. Essentially, it connects web pages to scripts or programming languages."

To access the DOM, we make use of the `document` object. This object has properties and functions that we use to access our HTML elements which we can manipulate with JavaScript. 

### How to access elements in the DOM

Let's get started with this sample HTML. Copy and paste this into a file called `index.html` and add an external script tag (or use a <script></script> in the <head></head>). We will explain later why for now, we put our scripts on the top.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <!-- make sure for now that your script tag is in the head -->
    <title>Document</title>
</head>
<body id= "container">
    <div class="hello">
        Hello World
    </div>
    <div class="hello">
        Hello Everyone!
    </div>
    <a href="#">This link goes nowhere!</a>
    <button>Click me!</button>
</body>
</html>
```

The easiest way to select elements is by their `id` using the `getElementById` function on the `document` object (`document.getElementById`) - this returns a **SINGLE** element (because id's must be unique!)

```javascript
var container = document.getElementById("container");
```

We can also use a function called `querySelector` function which selects a **SINGLE** element using `CSS` selectors.

```javascript
var container = document.querySelector("#container")
```

To select multiple elements we can use the `getElementsByTagName` or `getElementsByClassName` or we can use `querySelectorAll` and pass in a `CSS` selector. These will return what appear to be arrays (they are not **exactly** arrays, but for right now - that is not a problem).

```javascript
var divs = document.getElementsByTagName("div");
var divs = document.querySelectorAll("div");
```

Here is another example using `getElementsByClassName` and the same thing with `querySelectorAll`.

```javascript
var divsWithClassOfHello = document.getElementsByClassName("hello");
var divsWithClassOfHello = document.querySelectorAll(".hello");
```

### Modifying properties and attributes on elements in the DOM

We can change the text of an element through the `innerHTML` property.

```javascript
var firstDiv = document.getElementsByTagName("div")[0]

firstDiv.innerHTML = "Just changed!"
```

This can also be done using the `innerText` property.

```javascript
var secondDiv = document.getElementsByTagName("div")[1]

firstDiv.innerHTML = "Just changed Again!"
```

What's the difference between `innerText` and `innerHTML`? You can find it [here](http://stackoverflow.com/questions/19030742/difference-between-innertext-and-innerhtml-in-javascript)

We can also directly manipulate the `CSS` properties for elements (through inline styling) with the `style` property

```javascript
var firstDiv = document.getElementsByTagName("div")[0]

firstDiv.innerHTML = "Just changed Again!"
```

If we want to access/modify attributes on elements, we can do that with `getAttribute` and `setAttribute`

```javascript
var body = document.getElementById("container")

firstDiv.getAttribute("id") // "container"
firstDiv.setAttribute("id", "new_container") 
firstDiv.getAttribute("id") // "new_container" 
```

We can also add and remove classes to elements using `classList`

```javascript
var secondDiv = document.getElementsByTagName("div")[1]

secondDiv.classList // ["hello"]
secondDiv.classList.add("another_class") 
secondDiv.classList // ["hello", "another_class"]
secondDiv.classList.remove("hello") 
secondDiv.classList // [another_class"]
```

### Nodes vs Elements

When you read documentation about the DOM, you will see the terms `node` and `element`. In JavaScript these two are different and you can read more about the difference [here](http://stackoverflow.com/questions/9979172/difference-between-node-object-and-element-object). In short, there are many different types of nodes, but the ones we will most often be working with are ELEMENT_NODE and TEXT_NODE (you can see them all [here](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeType)). Element nodes are HTML elements (`div`, `span` etc.). Text nodes are the actual text of an element node.

### Traversing the DOM

Another very common operation when working with the DOM is trying to find elements inside of other elements. When we travel through the DOM in search of something, we are doing what is called DOM `traversal`. Let's start with this HTML and then look at some functions we can use to make things easier.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <!-- make sure for now that your script tag is in the head -->
    <title>Document</title>
</head>
<body id= "container">
    <div class="hello">
        Hello World
    </div>
    <div class="hello">
        Hello Everyone!
    </div>
    <a href="#">This link goes nowhere!</a>
    <button>Click me!</button>
</body>
</html>
```

Here are a few common methods we can use for finding elements and/or text nodes in relation to an element that we have already found. 

```javascript
var container = document.getElementById("container");
container.childNodes // // this contains all of the nodes (including text nodes) that are children
container.childNodes.length // 11
container.children // this contains all of the elements that are children of the element we have selected
container.children.length // 5

var link = document.querySelector("a");
link.parentElement // <body id="container">...</body>
link.previousElementSibling // <div class="hello">Hello Everyone!</div>
link.previousSibling // text node
link.nextSibling // text node
link.nextElementSibling // <button>​Click me!​</button>​
```

### Creating elements

To create elements we use the `.createElement` function on the `document` object and pass in a string with the name of the element that we would like to create. This will just return a new HTML element without any text/attributes or placement on the page!

```javascript
var newDiv = document.createElement("div")
```

So now that we created this element - how do we place it on the page?

### Appending elements

```javascript
var button = document.createElement("button");
button.innerText = "I am a button created with JavaScript!"

var container = document.getElementById("container")
container.appendChild(button)
```

And now that we created an element, how do we remove one?

### Removing elements

```javascript
var linkToBeRemoved = document.querySelector("a")

var container = document.getElementById("container")
container.removeChild(linkToBeRemoved)
```

### Changing multiple elements

So what would happen if we wanted to change all of our divs to have a background color of red? Unfortunately we can not do that without a loop

```javascript
var divs = document.querySelectorAll("div");
divs.style.backgroundColor = "red" // this will not work

// we have to use a loop for each one instead.
for(var i=0; i< divs.length i++){
    divs[i].backgroundColor = "red" // this will work!
}
```

### Exercise

Review all of these code examples. Really make sure you have an understanding of what's happening in this section, because the next section builds off of all of this. When you're ready - continue on!

### Additional Resources

#### [⇐ Previous](./15-introduction-to-the-dom.md) | [Table of Contents](./readme.md) | [Next ⇒](17-jQuery-events.md)