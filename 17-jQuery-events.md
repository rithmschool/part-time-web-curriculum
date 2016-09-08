#### [⇐ Previous](./16-jQuery-fundamentals.md) | [Table of Contents](./readme.md) | [Next ⇒](./18-twitter-bootstrap.md)

# Events

### Objectives:

By the end of this chapter - you should be able to

- Explain what browser events are
- Compare and contrast event capturing and bubbling
- Describe what the event object is and some a few commonly used properties that it includes

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <button class="first_button" onclick="=firstClick()">Click me first!</button>
    <button class="second_button" >Click me second!</button>
    <button class="third_button">Click me third!</button>
</body>
</html>
```

#### What an event is

From [MDN](https://developer.mozilla.org/en-US/docs/Web/Events) - "DOM Events are sent to notify code of interesting things that have taken place. Each event is represented by an object which is based on the Event interface, and may have additional custom fields and/or functions used to get additional information about what happened. Events can represent everything from basic user interactions to automated notifications of things happening in the rendering model."

In a nutshell, events are things we can trigger by interacting with the browser. Here are some potential events we can listen (and then execute some code) for:

- clicking on something
- hovering over something with the mouse
- pressing keys
- when the DOM has loaded
- when a form is submitted

You can see a full list [here](https://developer.mozilla.org/en-US/docs/Web/Events)

#### Adding an event listener

There are three ways that we can add event listeners to our code. We can either attach the name of the function in HTML, in JavaScript or use the `addEventListener` method.


```javascript
// Option 1: - directly in HTML
function firstClick(){
    alert("you clicked the first button!")
}

// Option 2 - attach the function to the element
var secondButton = document.querySelector('.second_button');
secondButton.onclick = function(){
    alert("you clicked the second button!")
}
// Option 3 - use addEventListener
var secondButton = document.querySelector('.third_button')
secondButton.addEventListener("click", function(){
    alert("you clicked the second button!")
});
```

So which one is best? 

It is often best to either use the second or third option (we will be using `addEventListener`) because you can customize it a bit more, but it is good to know all options.

So let's go back to our initial example and add an event listener to our buttons

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <button class="first_button">Click me first!</button>
    <button class="second_button" >Click me second!</button>
    <button class="third_button">Click me third!</button>
</body>
</html>
```

Just like when changing multiple elements, we need to iterate through each one - we can not just add an event listener to each element.

```javascript

var buttons = document.getElementsByTagName("button")

// this will NOT work 
buttons.addEventListener("click", function(){
    alert("You just clicked a button")
})

// we have to add the event listener to each button
for(var i=0; i<buttons.length; i++){
    buttons[i].addEventListener("click", function(){
        alert('You just clicked on a button!')
    })
}
```

#### Removing an event listener

Sometimes we want to stop listening for events - to do that we use the `removeEventListener` method - but this one has some quirks as well. Let's see:

```javascript
var buttons = document.getElementsByTagName("button")

// this will NOT work 
buttons.addEventListener("click", function(){
    alert("You just clicked a button")
})

// we have to remove the event listener to each button but this STILL won't work! That is because we are using an annonymous function
for(var i=0; i<buttons.length; i++){
    buttons[i].removeEventListener("click", function(){
        alert('You just clicked on a button!')
    })
}

// We have to make sure we define a function first - so that JavaScript knows what exactly to add and remove
function alertData(){
    alert("You just clicked a button")
}

// in order to remove, we have to name our function instead of using an annonymous one
for(var i=0; i<buttons.length; i++){
    buttons[i].addEventListener("click", alertData)
}

// since we have named our function - we know which one to remove
for(var i=0; i<buttons.length; i++){
    buttons[i].removeEventListener("click", alertData)
}
```

#### Adding an event to wait for the DOM to load

Another issue that we may face is when we have code like this:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        var container = document.getElementById("container");
        container.innerText = "Hello World" // This throws an error!
    </script>
</head>
<body>
    <div id="container">
        
    </div>
</body>
</html>
```

So what's going on here! Well, since our script tag is running before the DOM has loaded, it has no idea what the `<div id="container"></div>` is! What we can do is wait for the DOM to load, before executing any JavaScript. This can be done either with the `load` event or the `DOMContentLoaded` event. You can read about the difference between them [here](http://stackoverflow.com/questions/8835413/difference-between-load-vs-domcontentloaded)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        document.addEventListener("DOMContentLoaded", function(){
            var container = document.getElementById("container");
            container.innerText = "Hello World" // This works now!
        })
    </script>
</head>
<body>
    <div id="container">
        
    </div>
</body>
</html>
```

#### Data in the event object

When an event is triggered we have access to a special object called the `event` object. Inside of this object we can access quite a few useful values:

- target - the target element of the event 
- preventDefault() - a function that prevents the default action. This is used commonly to stop a form submission from refreshing the page (which is the default action of a submit event);

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        document.addEventListener("DOMContentLoaded", function(){
            var container = document.getElementById("container");
            container.addEventListener("click", function(event){
                console.log("Let's look at the event object!", event)
            })
        })
    </script>
</head>
<body>
    <div id="container">
        
    </div>
</body>
</html>
```

#### Capturing vs Bubbling

So far we have seen the `addEventListener` function take in two parameters, the name of the event and a callback function. But there is actually a third parameter we can pass in as a boolean called `useCapture` which determines if we use `capturing` or `bubbling`. 

From MDN - Event bubbling and capturing are two ways of propagating events that occur in an element that is nested within another element, when both elements have registered a handle for that event. The event propagation mode determines the order in which elements receive the event.

You can read more about capturing and bubbling [here](http://javascript.info/tutorial/bubbling-and-capturing) and [here](http://stackoverflow.com/questions/4616694/what-is-event-bubbling-and-capturing)

#### Accessing the value of whatever is clicked

When we listen for events, we sometimes want to know exactly what element triggered the event. We can do this using the `target` property on the `event` object, which is given to us when we use `addEventListener`.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <ul> Ingredients
        <li>Sugar</li>
        <li>Milk</li>
        <li>Eggs</li>
        <li>Flour</li>
        <li>Baking Soda</li>
    </ul>
</body>
</html>
```

Let's access each value using the `event.target` property!

```javascript
for(var i=0; i< listItems.length; i++){
    listItems[i].addEventListener("click", function(event){
        alert("You just clicked on " + event.target.innerText)
    })
}
```

#### Adding event listeners to parent elements

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <ul> Ingredients
        <li>Sugar</li>
        <li>Milk</li>
        <li>Eggs</li>
        <li>Flour</li>
        <li>Baking Soda</li>
    </ul>
</body>
</html>
```

In order to alert the text of whatever element we looked for, we can either listen on the parent or listen on each child. Let's examine both options:

```javascript
var ul = document.querySelector("ul");

// how many event listeners?
ul.addEventListener("click", function(event){
    alert("You just clicked on " + event.target.innerText)
})

var listItems = document.getElementsByTagName("li")

// how many event listeners?
for(var i=0; i< listItems.length; i++){
    listItems[i].addEventListener("click", function(event){
        alert("You just clicked on " + event.target.innerText)
    })
}
```

So which one do you think is more efficient? If you think less listeners you are right! It's always best to have less event listeners as they consume memory and are difficult to manage when there are many of them.

### Exercise

Complete the [DOM Exercises](https://github.com/rithmschool/prework_exercises/tree/master/intro_to_the_dom_exercise)

Complete the [Todo App](https://github.com/rithmschool/prework_exercises/tree/master/todo_exercise)

### Additional Resources

#### [⇐ Previous](./16-jQuery-fundamentals.md) | [Table of Contents](./readme.md) | [Next ⇒](./18-twitter-bootstrap.md)