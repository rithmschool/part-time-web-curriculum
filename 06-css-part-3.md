#### [⇐ Previous](./05-css-part-2.md) | [Table of Contents](./readme.md) | [Next ⇒](./07-javascript-introduction-and-history.md)

# CSS Part III

### Objectives:

By the end of this chapter, you should be able to:

- Include transitions, transforms and animations to add dynamic behavior to a page
- Explain what responsive design is and how it can be achieved using CSS
- Compare and contrast units of measurement when designing a page to be responsive

### Transformations, Transistions, and Animations

#### Transform

- `transform` -  CSS transforms change the shape and position of the affected content and allow you to translate, rotate, scale, and skew elements.
A transformation is an effect that lets an element change shape, size and position. Here are a few of the methods that can be values of `transform` property:
    - `translate` - The translate() method moves an element from its current position. For example, if you give an element the rule `transform: translate(50px,100px);`, the element will be 50 pixels to the right and 100 pixels down. 
    - `rotate` -  The rotate() method rotates an element clockwise or counter-clockwise according to a given degree. For example, if you give an element the rule `transform: rotate(90deg);`, the element will be rotated 90° clockwise.
    - `scale` - The scale() method increases or decreases the size of an element (according to the parameters given for the width and height). For example, if you give an element the rule `transform: scale(2,3);`, the element will scaled 200% horizontally and 300% vertically.

Here's an example of what these transforms look like in action. This HTML page has two divs with identical content, but one is transformed:

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
    #original, #transformed {
      width: 100px;
      height: 100px;
      color: red;
      background-color: purple;
      text-align: center;
      padding: 20px;
      border: 10px solid black;
    }

    #transformed {
      transform: translate(200px, 100px) rotate(45deg) scale(3,1);
    }
  </style>
</head>
<body>
  <div id="original">Hi, I'm a div.</div>
  <div id="transformed">Hi, I'm a div.</div>
</body>
</html>
```

![transformed div](../screenshots/transform.png)

There are a number of other values that the transform property can take. For an exhaustive list, check out the [documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/transform).

#### Transitions

- `transition` - CSS transitions provide a way to set and control animation speed when changing CSS properties. Instead of having property changes take effect immediately, you can cause the changes in a property to take place over a period of time. For example, if you change the color of an element from white to black, usually the change is instantaneous. With CSS transitions enabled, changes occur at time intervals that follow an acceleration curve, all of which can be customized. You can read more about them [here](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions). 

CSS transitions let you decide which properties to animate (by listing them explicitly), when the animation will start (by setting a delay), how long the transition will last (by setting a duration), and how the transition will run (by defining a timing function, e.g. linearly, or quick at the beginning and slow at the end). You can also set transitions for multiple properties by comma separating values in the `transition` property (an example of this is shown in the example below).

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <a href="">Click me!</a>
</body>
</html>
```

```css
a {
  background-color: #139CFF;
  text-decoration: none;
  color:white;
  padding: 10px;
  border-radius: 7px;
  display: inline-block;
  font-family: helvetica;
  /* transition: <property> (default all) <duration> <timing-function> (default ease) <delay> (default 0); */
  transition: background-color .5s, color .5s linear, border-radius 2s ease-out;
  /* try playing around with the parameters in the value and see how the transition changes! */
}

a:hover {
  background-color: #35EC5C;
  color: black;
  border-radius: 30px;
}
```

When you open up this page in Chrome and hover over the buton, you should see a nice, smooth transition:

![button transition](../screenshots/transition.gif)

If you comment out the `transition` rule in the CSS, however, the change in style will be much more abrubt:

![button transition](../screenshots/no_transition.gif)

#### Animations

CSS animations make it possible to create more complex animation transitions from one CSS style configuration to another. Let's walk through the process of creating the following animation:

![button transition](../screenshots/shapeshift.gif)

To begin, let's create a simple html file and style a single div in it. This div will represent our shape:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
    #ball {
      width: 100px;
      height: 100px;
      margin-top: 400px;
    }
  </style>
</head>
<body>
  <div id="ball"></div>
</body>
</html>
```

To create our animation, we need to things: an `animation` property on the relevant HTML element, and a set of _keyframes_ that describe the animation we're trying to build. In this case, since our shape is changing, let's call our animation `shapeshift`. Our animation property might have a value that looks like this:

```css
#ball {
	width: 100px;
	height: 100px;
	margin-top: 400px;
	animation: shapeshift 6s infinite;
}
```

The `6s` indicates how long it should take to complete our animation, while the `infinite` ensures that the animation will play on loop, rather than stopping after one cycle. There are actually 8 sub-properties that you can set inside of `animation`; [here's](https://css-tricks.com/almanac/properties/a/animation/) an article on all of them if you'd like to dig a little deeper.

If you view the page in Chrome, you'll see that nothing is working yet. That's because we haven't defined what `shapeshift` means! In order to define this animation, we need to use the keyframes at-rule. Underneath your style for the `ball` div, add this: 

```css
@keyframes shapeshift {
	/* here's where we define our animation */
}
```

Inside of this, we can define several different _keyframes_, which describe the state of our div at different points in the animation. These points are described using percentages. For example, we know that at the start and end of our animation, the `ball` div should be red and round. So we might set the following keyframes:

```css
@keyframes shapeshift {
	0%, 100% {
		transform: translate(0,0);	
    	border-radius: 100px;
		background-color: red;
	}
}
```

Meanwhile, one-third of the way through the animation, we want the div to move to the right, move up, and be a smaller blue square. Here's how we might declare that keyframe:

```css
@keyframes shapeshift {
	0%, 100% {
		transform: translate(0,0);	
    	border-radius: 100px;
		background-color: red;
	}
	
	33% {
		transform: translate(200px, -400px) scale(0.5, 0.5);
		border-radius: 0px;
		background-color: blue;
	}
}
```

Finally, two-thirds of the way through the animation, we want the square to spin, move down and to the right, grow larger, and turn green. Adding this rule completes our definition of the `shapeshift` animation:

```css
@keyframes shapeshift {
	0%, 100% {
		transform: translate(0,0);	
    	border-radius: 100px;
		background-color: red;
	}
	
	33% {
		transform: translate(200px, -400px) scale(0.5, 0.5);
		border-radius: 0px;
		background-color: blue;
	}
	
	66% {
		transform: translate(400px, 0) rotate(4545deg) scale(2,2);
		border-radius: 0px;
		background-color: green;
	}
}
```

You should now have a working animation of a shape-shifting div!

You can learn more about CSS Animations [here](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations) and see some examples [here](http://www.w3schools.com/css/tryit.asp?filename=trycss3_animation2) and [here](http://www.w3schools.com/css/css3_animations.asp) - (W3Schools is NOT a good resource for documentation, but they do have some helpful examples).

### CSS Resets

Since we strive to develop the same functionality/style accross all browsers, it would be nice if we could start with a level playing field for all browsers. Unfortunately, different browsers make slightly different assumptions about the default styling of a webpage. For example, in Chrome, the `body` has a default margin of `8px` on all sides.

In order to eliminate possible discrepancies across browsers, it's very common to create what's called a CSS Reset. This is just a stylesheet which attempts to overwrite (or reset) any default browser styles with styling that will then be the same across different environments. You typically don't write a CSS Reset yourself; instead, there are a few commonly used resets you can choose from. Here are a couple:

1. reset.css - this was created by Eric Meyer and it basically resets/clears everything. It's a bit aggressive, but if you want to start from scratch it's a great tool. [http://meyerweb.com/eric/tools/css/reset/](http://meyerweb.com/eric/tools/css/reset/)
2. normalize.css - [https://necolas.github.io/normalize.css/](https://necolas.github.io/normalize.css/)

### Responsive + Mobile First Design

One thing to keep in mind if you really care about design is the way your site looks on different devices. You might spend days meticulously crafting a beautifully designed site on your laptop, only to discover that it looks like garbage on your phone.

_Responsive design_ is a way to approach designing your applications that is mindful of the fact that users will come to your site on different screens. With a responsive design, the goal is to make your site beautiful for users on a variety of devices, while minimizing the amount of CSS you need to write.

One common approach to responsive design is to called _mobile first_. A mobile-first approach to styling means that styles are applied first to mobile devices. Advanced styles and other overrides for larger screens are then added into the stylesheet via media queries.

To get started with responsive design, we need to understand how to write media queries and move from absolute measurement to relative measurement. 

### Media Queries

One of the fundamental building blocks of responsive design along with mobile first design is the ability to show different styles for different conditions. As with keyframes, media queries are declared using an at-rule. Here's a simple example of the syntax:

```css
`@media screen and (max-width: 480px) {
    /* add some styles for a mobile device here*/
}
```

You can check for a lot of things using media queries. To see more examples, check out the [MDN docs](https://developer.mozilla.org/en-US/docs/Web/CSS/@media).

### Different units of measurement 

So far we have only seen pixels, which are an absolute/fixed unit of measurement. These are great when you know "exactly" what the dimensions/properties are. Pixels, inches, centimeters, millimeters, and points are all examples of absolute units of measurement. 

In contrast, relative units, like the name suggests, are always relative to the length of another property. Examples here include percentages, ems, root ems, exes, character units, viewport width, viewport height, viewport minimum, and viewport maximum. 

- `%` - percentages of whatever container or fixed value the element is inside of.
- `em` - when used with `font-size` 1em is equal to the default font-size for the device (usually 16px). The value of `em` does change as an em tells an element to calculate its size relative to the size of the parent. If `em` is not set outside of font-size it will use the device settings. 
- `rem` - just like em's but they are only relative to the root element 
- `vh/vw` - equal to 1/100th of the viewport's height/width
- `vmin/vmax` - equal to 1/100th of the viewport's maximum height/width

### Writing cleaner CSS

1. Shy away from using IDs and lots of classes and instead use more complex selectors (descendant, adjacent, sibling, n-th child etc)

2. Keep your CSS DRY by adding common styles to selectors separated by a comma.

```css

/* BAD */

.heading_content {
    color: #0000F9;
    font-size: 2em;
    margin-top: 1em;
    text-align: center;
}

.footer_content {
    color: #E046CF;
    font-size: 2em;
    margin-top: 1em;
    text-align: center;
}

/* BETTER */

.heading_content, .footer_content {
    font-size: 2em;
    margin-top: 1em;
    text-align: center;
}

.heading_content {
    color: #0000F9;
}

.footer_content {
    color: #E046CF;
}
```

3. Read and learn about CSS organizational structures like [BEM](http://getbem.com/introduction/)

### Exercise

- Complete the [CSS Animations](https://github.com/rithmschool/prework_exercises/tree/master/css_animations) exercise

### Additional Resources

[http://www.html5rocks.com/en/tutorials/speed/high-performance-animations/](http://www.html5rocks.com/en/tutorials/speed/high-performance-animations/)

[http://webdesign.tutsplus.com/articles/7-css-units-you-might-not-know-about--cms-22573](http://webdesign.tutsplus.com/articles/7-css-units-you-might-not-know-about--cms-22573)

[http://www.sitepoint.com/introduction-mobile-first-media-queries/](http://www.sitepoint.com/introduction-mobile-first-media-queries/)
[http://code.tutsplus.com/tutorials/5-ways-to-instantly-write-better-css--net-3003](http://code.tutsplus.com/tutorials/5-ways-to-instantly-write-better-css--net-3003)

#### [⇐ Previous](./05-css-part-1.md) | [Table of Contents](./readme.md) | [Next ⇒](./07-javascript-introduction-and-history.md)


