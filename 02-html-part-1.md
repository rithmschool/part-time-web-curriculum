#### [⇐ Previous](./01-welcome.md) | [Table of Contents](./readme.md) | [Next ⇒](./03-html-part-2.md)

# HTML Part I

### Objectives:

By the end of this chapter, you should be able to:

- Create simple pages using only HTML
- Compare and contrast divs and spans
- Structure code using lists and tables
- Speed up writing HTML using Emmet
- Describe the difference between an element and an attribute

### Getting started with HTML

From Wikipedia -

<blockquote>HyperText Markup Language, commonly abbreviated as HTML, is the standard markup language used to create web pages.</blockquote>

The building blocks for HTML are `elements`. We specify the name of the element using its name along with `<>`. To denote the ending of a tag, we use `</>`.

#### Adding a doctype

Another essential building block for our web pages is to specify the doctype declaration, which tells the browser that the page is written in HTML. We will be using `<!DOCTYPE html>` to tell the page that we are using HTML5.

At the top of any HTML page, there are a few essential tags that we want to have:

`<html>` - This is where all of our elements that comprise the contents of our page are placed.
`<head>` - This is the container for the head elements, which are elements that have content that does not need to be displayed on the page (like metadata, the title, or, as we will see, scripts and stylesheets )
`<meta>` - This is a tag for providing metadata (data about our data) to the page. We can use meta tags to display what character set we are using or for SEO purposes.
`<title>` - This tag gives the page a title that can be displayed in the tab of your browser
`<body>` - This defines the main content of the HTML page.

So a sample structure could look like

```html
<!DOCTYPE html>
<html>
<head>
  <title>My First Page</title>
</head>
<body>
  Hello World!
</body>
</html>
```

### Installing Emmet

Sometimes typing all of these tags is quite a pain. Thankfully, there is a nice tool to help us out called Emmet, which makes writing HTML a breeze. To install it, open package manager in sublime (command + shift + p), type "install package," and press enter. Then wait a second for a list to pop up and search for "Emmet." After the installation, restart sublime and make sure you have saved a file with a `.html` extension.

In your `.html` file - type in `!` and press tab and this should appear:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>

</body>
</html>
```

Another nice sublime trick when working with HTML files is to right click anywhere in the .html file and head to "Open in Browser". This will open your page right in a browser!

### Headings, Paragraphs, Breaks and horizontal rows

In HTML we have quite a few ways to display and separate text. We have heading tags `<h1></h1>` (h1 largest - h6 smallest), paragraph tags `<p></p>`, line breaks `<br>` (notice that this tag does not close), and horizontal rows `<hr>` (this tag does not close as well).

### Lists in HTML

To create list items in HTML we can either use ordered lists or unordered lists:

```html
<ol>
  <li>First</li>
  <li>Second</li>
  <li>Third</li>
</ol>

<ul>
  <li>Something Not Ordered</li>
  <li>Something Not Ordered</li>
  <li>Something Not Ordered</li>
</ul>
```

### Divs + Spans

In HTML there are two important tags which do not have much significance, but are useful for laying out a page. These tags are `<div></div>` and `<span></span>`. Try adding these tags and see the difference! Then answer the following questions:

- What is a div?
- What is a span?
- What are some differences between the two?

### Text modifications

To change the text we can use tags like `<b></b>`, `<u></u>`, `<em></em>`, `<small></small>`, `<sup></sup>`, `<sub></sub>`, `<blockquote></blockquote>` and `<cite></cite>`. Take a look at what these do!

### Anchor tags

When we want to create hyperlinks to other pages, we use an anchor tag `<a></a>`. To specify what link we want to go to we use the `href` attribute. Attributes are used to provide additional information about an element and are always inside of the opening tag.
To add an `href` attribute to our anchor tag we would write something like `<a href="http://www.google.com">Go To Google!</a>`

### Images

We can add images and specify their source using the `src` attribute. Another important attribute for image tags is the `alt` attribute which is what is displayed when the image fails to load and is very important for SEO purposes as well. It looks something like this - `<img src="http://lorempixel.com/200/200" alt="Some random 200x200 picture">`

### HTML Comments

Sometimes we want to explain certain parts of our HTML, but not have it display on the page. These are called comments and are useful when documenting our code. To add them, we simply include text inside of this `<!--  -->`:

```html
<!-- Tell the reader to keep up the good work -->
<h1>
  Well done! You made it to the end of this section! Now go and practice some HTML with the exercises below!
</h1>
```

### Exercise

- Complete Part I of the [HTML Exercises](https://github.com/rithmschool/prework_exercises/tree/master/html_exercises)

### Additional Resources

#### [⇐ Previous](./01-welcome.md) | [Table of Contents](./readme.md) | [Next ⇒](./03-html-part-2.md)