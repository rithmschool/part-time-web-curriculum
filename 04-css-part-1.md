#### [⇐ Previous](./03-html-part-2.md) | [Table of Contents](./readme.md) | [Next ⇒](./05-css-part-2.md)

# CSS Part I

### Objectives:

By the end of this chapter, you should be able to:

- Define what CSS is and demonstrate three different ways to include it on your page
- Use selectors to target HTML and understand how specificity plays a large factor when using selectors
- Add CSS3 features and understand how to use them
- Create simple layouts using the box model, display, and floats

### Getting started with CSS

From [Wikipedia](https://en.wikipedia.org/wiki/Cascading_Style_Sheets):

>Cascading Style Sheets (CSS) is a style sheet language used for describing the presentation of a document written in a markup language. 

In other words, it's the language we use to style our page (colors/fonts/layout etc.). There are three ways to include CSS in our web pages:

1. Inline styling. This is done by adding a `style` attribute to an HTML tag. We will see shortly that this can have some unintended consequences.
2. `<style></style>`. This is done by using a `style` tag and placing CSS inside of it.
3. External stylesheets. **This is the most common way and almost always the best practice**

Since we will be using external stylesheets, we need to figure out how to link our CSS to our HTML. The answer is with a `link` tag! If we have a file called `style.css` in the same folder as our HTML file, we can link them with the following tag (otherwise just use the relative path to find the CSS file):

`<link rel="stylesheet" href="style.css">`

### Syntax, Selectors and Specificity

Each CSS rule consists of a selector (how we find the element/elements) to target and a pair of curly braces, a.k.a. `{}`. Inside of `{}` we specify properties and values separated by a `:`, and after the value we add a `;`. To add multiple selectors we separate each one by a `,`. This looks something like this:

```css
body {
    background-color: green;
}
```

In this rule, we are targeting the `<body></body>` element and applying a background color to it. While this works, it might be a bit too general (maybe we only want a background color of green on certain parts of the page, not the whole body). In order to be more specific, we can use attributes like `class` and `id` to target our elements. 

Let's take a look at this HTML:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Learn CSS</title>
</head>
<body class="main_styles" id="container">
    <header class="main_heading">
        <h1>Welcome to our website</h1>
        <h4>We're so happy to have you</h4>
    </header>
    <section class="main">
        <ul> Here are some reasons you should keep reading....
            <li>You're learning things!</li>
            <li>CSS is fun!</li>
            <li>Well.....not always, but it is essential to know!</li>
        </ul>
    </section>
    <footer class="main_footer">
        <p>
            Thanks for checking out this page! 
            <a href="#">Here is a link that goes nowhere! It's for showing you stuff with CSS......we promise</a>
        </p>
    </footer>
</body>
</html>
```

We can see from this HTML that we have added some `class` and `id` attributes. Right now they do not alter anything about the page, but we can use them as selectors with CSS. To target a class with CSS, add a `.` before the name of the class. For an id, add a `#` before the name of the id.

This is what some CSS might look like for our page:

```css
#container {
    font-size: 16px;
}
.main_header {
    background-color: grey;    
}
.main {
    background-color: blue;
}
.main_footer {
    background-color: green;
}
.main_header, 
.main_footer {
  color: red;
}
```

So what is the difference between an id and a class? One difference is that id's are unique, whereas classes can be shared amongst elements. Another has to do with specificity. What's _specificity_, you ask? Excellent question!

#### Specificity

One of the most important ideas around CSS is that of specificity, or how specific we are with our selectors. Imagine we have some CSS that looks like this:

```css
body {
    background: red;
}

.main_styles {
    background: yellow;
}

#container {
    background: blue;
}
```

`main_styles` is a class on the `body` element and `container` is an ID on the body element... so we have 3 conflicting rules. Which one wins? To answer this question let's introduce a brief table for understanding.

| Selector  | Weighting  |
|---|---|
| element  | 1  |
| class  | 10  |
| id  | 100  |
| inline-style  | 1000  |
| !important  | 10000+  |

What does this mean? Let's take a look at an example (we are using `<style></style>` tags which are not the best, but easiest for an example)

```html
<!DOCTYPE html>
<html>
<head>
    <title>Specificity</title>
    <style>
        body {
            background: purple;
        }
        .main {
            background: blue;
        }
        #container {
            background: green;
        }
        .winner {
            background: aqua !important;
        }
    </style>
</head>
<body class="main winner" id="container" style="background:red;">
    What color could I possibly be??
</body>
</html>
```

In order of specificity (least to most specific) - what is the background color?

1. purple
2. blue
3. green
4. red
5. aqua

When we previously mentioned that using inline styling (a `<style></style>` tag) can have some unintended consequences, well, strong specificity is one of them!

### Other useful selectors

#### Descendant Selector

```css

/* The descendant selector matches all elements that are descendants of a specified element. In this case, find all the paragraph tags inside of a footer tag (read the selectors from right to left) */
footer p {
    background:red;
}
```

#### Adjacent Selector

```css
/* Find all the h4 tags that are directly adjacent to an h1 tag. */

h1+h4 {
    background:blue;
}
```

#### Direct child selector

```css
/* Find all li's which are children - not just descendents - of a ul */

ul > li {
    background:blue;
}
```

#### Attribute Selector
```css
/* Find all a tags whose href attribute is set to "#" */

a[href="#"] {
    background:blue;
}
```

#### First / Last Child Selector

```css
/* Find all the li's which are the first children of their parents */

li:first-child {
    background:blue;
}
```

#### n-th child selector

```css
/* Find all the li's which are the second children of their parents */

li:nth-child(2) {
    background: teal;
}
```

One important thing to know about CSS is the **C**, or **cascading** nature of CSS. This means that your code is read top to bottom, so if you have the same level of specificity, the rule closest to the bottom wins.

### CSS rules

So far we have seen `background-color` which is a relatively simple property that allows us to set the background color. This can be done with a named color (blue, green, red etc.), a hex (# followed by six values from 0 to F), rgb (red, green, blue) or hsl (hue, saturation, lightness) value. If you don't know what these are, you can mess around with them [here](http://htmlcolorcodes.com/color-picker/)

#### Typography 

If we want to change the text on our page, we commonly use some of these rules:

- `font-size` - select the size of your font (we will discuss other units of measurement in the next unit)
- `text-align` - align the position of the text
- `font-family` - choose what kind of font you want to use
- `letter-spacing` - add positive or negative (less) space between characters
- `text-transform` - capitalize/uppercase/lowercase your text
- `line-height` - choose the amount of height between lines
- `font-variant` - useful for displaying a small-caps font
- `text-shadow` - add a shadow to your text
- `color` - select the color of the text

```css
.some_text {
    color: #BDBFEF;
    font-size: 12px; 
    text-align: center;
    font-family: helvetica, sans-serif; 
    letter-spacing: -1px;
    text-transform: lowercase;
    text-shadow: 0 2px 0 black;
    /* first value is horizontal/x offset */
    /* second value is vertical/y offset */
    /* third value is how much blur */
    /* fourth value is the color */
    /* you can even have multiple shadows separated by a comma! */
    line-height: 1.4;
    font-variant: small-caps;
}
```

#### Using a custom google font

You can head over to [https://www.google.com/fonts](https://www.google.com/fonts) and select some fonts, then click "Use" at the bottom. It will then give you a <link> tag as well as the CSS necessary. Here is an example using Open Sans `<link href='https://fonts.googleapis.com/css?family=Open+Sans' rel='stylesheet' type='text/css'>` and 

```css

body {
    font-family: 'Open Sans', sans-serif;    
}
```

#### The Box Model 

Now that we have an idea around basic color and typography, let's see how to add some space around our elements and the content inside. In order to do that, we first have to understand what the box model is. But before we explain the box model, let's make sure we understand some basic properties for adding space between elements and content.

`width` - The width CSS property specifies the width of the content area of an element.
`height` - The height CSS property specifies the height of the content area of an element. 
`margin` - used to generate space around elements. `margin` is a shorthand for `margin-top`, `margin-right`, `margin-bottom` and `margin-left`.
`padding` - The `padding` property in CSS defines the innermost portion of the box model, creating space around an element's content, inside of any defined margins and/or borders. `padding` is a shorthand for `padding-top`, `padding-right`, `padding-bottom` and `padding-left`.
`border` - The `border` property defines the space between an element's padding and margin. `border` is shorthand for `border-top`, `border-right`, `border-bottom` and `border-left`.

```css
div {
    /* This: */
    margin: 20px;
    /* Is the same as: */
    margin-top:20px;
    margin-right:20px;
    margin-bottom:20px;
    margin-left:20px;

    /* This: */
    padding: 10px 20px;
    /* Is the same as: */
    padding-top:10px;
    padding-right:20px;
    padding-bottom:210px;
    padding-left:20px;
}

h1 {
    /* This: */
    margin: 20px 10px 5px;
    /* Is the same as: */
    margin-top:20px;
    margin-right:10px;
    margin-bottom:50px;
    margin-left:10px;
}   

h2 {
    /* This: */
    margin: 10px 20px;
    /* Is the same as: */
    margin-top: 10px;
    margin-right: 20px;
    margin-bottom: 10px;
    margin-left: 20px;
}
```

Now that we understand this, we can think of every single element on a web page as a rectangular box.

From MDN: 

>In a document, each element is represented as a rectangular box. Determining the size, properties — like its color, background, borders aspect — and the position of these boxes is the goal of the rendering engine.

>In CSS, each of these rectangular boxes is described using the standard box model. This model describes the content of the space taken by an element. Each box has four edges: the margin edge, border edge, padding edge, and content edge.

![./../screenshots/box-model.png](./../screenshots/box-model.png)

The **true** width/height of an element is comprised of its width/height + padding + border. **Margin is not counted when calculating the true width/height!**

```css
div {
    width: 200px;
    height: 200px;
    margin: 20px;
    padding: 20px;
    border: 20px solid black;
}

/* True width =  width (200px) + padding-left(20px) + padding-right(20px) + border-left (20px) + border-right (20px) = 280px
*/

/* True height =  width (200px) + padding-top(20px) + padding-bottom(20px) + border-top (20px) + border-bottom (20px) = 280px
*/
```

#### Additional CSS properties

```css
div {
    box-sizing: border-box;
}
```

By default, the `box-sizing` property is set to `content-box`, which means that the `width` and `height` property values correspond to the width and height of the content area only. When set to `border-box`, however, the `width` and `height` property values correspond to the width and height of content + border + padding.

Also, in CSS3 we can add rounded corners (and turn our boxes into rounded shapes) using the `border-radius` property:

```css
div {
	background-color: blue;
    border-radius: 10px;
}
```

What happens as you increase/decrease the value of `border-radius`?

#### Layout

Since we have a basic understanding of the box model, let's take a stab at trying some layout using the `display` property. This is probably the most simple way of doing layouts and is a great place to start.

`display` is CSS's most important property for controlling layout. Every element has a default display value depending on what type of element it is. The default for most elements is usually `block` or `inline`. A block element is often called a block-level element. An inline element is always just called an inline element.

- `block` -  A block-level element starts on a new line and stretches out to the left and right as far as it can. Common block-level elements are `div`, `p`, `form`, and new in HTML5 are `header`, `footer`, `section`, and more.
- `inline` - `span` is the standard inline element. An inline element can wrap some text inside a paragraph <span> like this </span> without disrupting the flow of that paragraph. The `a` element is the most common inline element, since you use them for links.
- `inline-block` - inline-block works just like `inline` except `height` and `width` are not ignored!

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        /* Let's line up three 200x200 boxes together */

        /* since divs have a display:block; by default, they will stack on top of each other like blocks, but we want to change that. Our first thought might be to use display:inline; but then we will lose our width and height - we need to use display:inline-block; */

        div {
            height: 200px;
            width: 200px;
            background: green;
            display: inline-block;
        }
    </style>
</head>
<body>
    <div class="one">I AM A BOX</div>
    <div class="two">I AM A BOX</div>
    <div class="three">I AM A BOX</div>
</body>
</html>
```

#### Floats + Clearing

Another way to lay out a page, and for specifically moving elements to a certain side of the page, is to use floats. Floats are a bit tricky at first because we need to understand what the idea of `document flow` is. Floats are used a bit less now that there are more advanced (and easier) means of laying out a page, but they are important to know about.

From [here](http://onwebdev.blogspot.com/2011/01/css-understanding-document-flow.html):

>The document flow is the model by which elements are rendered by default in the CSS specifications. In this model, elements are rendered according by their default display rule. In other words, block-level elements are displayed on a new line and inline elements on the same line. Everything is stacked in an ordered way from top to bottom. 

What this means is that when we use floats, we take the elements that are floated, and ignore/remove them from the document flow. To bring them back we can use the `clear` property.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        header {
            background: red;
        }
        section {
            background: green;
        }
        aside {
            float: left;
            background: yellow;
        }
        footer {
            background: brown;
        }
    </style>
</head>
<body>
    <header>
        header
    </header>
    <section>
        Main Content
    </section>
    <aside>
        Sidebar
    </aside>
    <footer>
        Footer
    </footer>
</body>
</html>

```

### Exercise

- Go through the exercises here on CSS selectors - [http://flukeout.github.io/](http://flukeout.github.io/)
- Work through the [CSS Exercises](https://github.com/rithmschool/prework_exercises/tree/master/css_exercises)

### Additional Resources

[http://learnlayout.com/](http://learnlayout.com/)

[http://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048](http://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048)

#### [⇐ Previous](./03-html-part-2.md) | [Table of Contents](./readme.md) | [Next ⇒](./05-css-part-2.md)