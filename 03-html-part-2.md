#### [⇐ Previous](./02-html-part-1.md) | [Table of Contents](./readme.md) | [Next ⇒](./04-css-part-1.md)

# HTML Part II

### Objectives:

By the end of this chapter, you should be able to:

- Define what semantic HTML is and what tags can be used to create it
- Build forms using various inputs and understand their specific attributes
- Embed audio and video into an HTML page 

### Semantic HTML

From [Wikipedia](https://en.wikipedia.org/wiki/Semantic_HTML): 

>Semantic HTML is the use of HTML markup to reinforce the semantics, or meaning, of the information in webpages and web applications rather than merely to define its presentation or look. Semantic HTML is processed by traditional web browsers as well as by many other user agents. 

This basically means that we can use HTML tags that do not alter our page in any specific way, but make more sense to the developer and reader of the HTML as to what they do. Here are some semantic HTML5 tags (there are many more):

- `header` - used to display the header information on a page
- `nav` - used to display a navbar for navigating a page
- `section` - used to display a section of the page 
- `article` - used to display independent, self-contained content.
- `aside` - used to display content aside from main content (on the side)
- `footer` - used to display the footer information on a page

### Building HTML Forms

Forms are another essential part of HTML and will be used quite a bit when we get to server side programming. We use forms to transmit data to other pages/servers. 

From [MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/My_first_HTML_form):

>HTML Forms are one of the main points of interaction between a user and a web site or application. They allow users to send data to the web site. Most of the time that data is sent to the web server, but the web page can also intercept it to use it on its own.

>An HTML Form is made of one or more widgets. Those widgets can be text fields (single line or multi line), select boxes, buttons, check boxes, or radio buttons. Most of the time, those widgets are paired with a label that describes their purpose.

To get started with a form, we need a `<form></form>` tag and an `action` attribute (where the form should go when submitted). We will use `#` as the value of this attribute to signify that the form should not go anywhere. Forms also have another essential attribute called `method` which specifies how the form should be submitted (but don't worry about this one - we'll talk much more about it later)

`<form action="#"></form>`

Like we just read, forms need to have widgets (or inputs) which can be paired with a label to describe their purpose. Let's take a look at this form:

```html
<form action="#">
    <div>
        <label for="username">Username</label>
        <input type="text" id="username">
    </div>
    <div>
        <label for="password">Password</label>
        <input type="password" id="password">
    </div>
    <div>
        <label>Favorite Instructor</label>
        <label for="elie">Elie</label>
        <input type="radio" name="favorite_instructor" id="elie">
        <label for="matt">Matt</label>
        <input type="radio" name="favorite_instructor" id="matt">
        <label for="tim">Tim</label>
        <input type="radio" name="favorite_instructor" id="tim">
    </div>
    <div>
        <label>Favorite Programming Language(s)</label>
        <label for="ruby">Ruby</label>
        <input type="checkbox" name="favorite_language" value="Ruby" id="ruby">
        <label for="javascript">JavaScript</label>
        <input type="checkbox" name="favorite_language" value="JavaScript" id="javascript">
        <label for="python">Python</label>
        <input type="checkbox" name="favorite_language" value="Python" id="python">
        <label for="go">Go</label>
        <input type="checkbox" name="favorite_language" value="Go" id="go">
    </div>
    <div>
        <label>Additional Comments</label>
        <textarea name="" id="" cols="30" rows="10"></textarea>
    </div>
    <div>
        <input type="submit" value="">
    </div>
</form>
```

You can see that some of these inputs have `name` attribute. While we will not be discussing this in great detail for now (we will come back to this later), this input is necessary if we are trying to collect form values to be transmitted to a server/another page. 

### Building Semantic HTML Tables

Although they are not as popular as they used to be (entire web pages used to be designed just using tables!), it's still quite valuable to know how to build tables as they are great for displaying certain kinds of data!

`<table>` - This tag encompasses the entire table and wraps all of your HTML code for a table

`<tr>` - The table row element defines a row of cells which can include `td` and/or `th` tags

`<th>` - The table header tag defines a cell as the "header" for group of cells. This is traditionally placed inside of a `thead` tag.

`<td>` - The table data tag defines a cell of a table that contains some data.

`<thead>` - The table head tag defines a set of rows which define the columns of a table

`<tbody>` - From MDN - The HTML Table Body Element (`<tbody>`) defines one or more `<tr>` element data-rows to be the body of its parent `<table>` element (as long as no `<tr>` elements are immediate children of that table element.)  In conjunction with a preceding `<thead>` and/or `<tfoot>` element, `<tbody>` provides additional semantic information for devices such as printers and displays. Of the parent table's child elements, `<tbody>` represents the content which, when longer than a page, will most likely differ for each page printed; while the content of `<thead>` and `<tfoot>` will be the same or similar for each page printed. For displays, `<tbody>` will enable separate scrolling of the `<thead>`, `<tfoot`>, and `<caption>` elements of the same parent `<table`> element.  

`<tfoot>` - The table foot tag defines a set of rows summarizing the columns of the table.

Here is an example of what a semantic table looks like in HTML:

```html
<table>
    <thead>
        <tr>
            <th>heading</th>
            <th>heading</th>
            <th>heading</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>content</td>
            <td>content</td>
            <td>content</td>
        </tr>
        <tr>
            <td>content</td>
            <td>content</td>
            <td>content</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>content</td>
            <td>content</td>
            <td>content</td>
        </tr>
    </tfoot>
</table>
```

### HTML5 Media

With HTML5 comes the ability to embed audio and video into our HTML. We can do this using the audio tag and video tag. You can read more about the audio tag [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio) and the video tag [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video)

### iframe (inline frame)

A bit of an older tool that you will see sometimes is an `<iframe></iframe>` tag. The `iframe` tag is used to embed another document (HTML page) within the current page. You can read more about it [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) and how they are (or are mostly not) used [today](http://stackoverflow.com/questions/3721929/when-should-i-use-html-frames). Although you will rarely be creating your own `iframe` tags, it is very common to embed content from other websites on your page through an `iframe` tag. You can read how to embed an audio player from Spotify [here](https://developer.spotify.com/technologies/widgets/spotify-play-button/) and a YouTube video [here](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds)

### Exercise

- Complete Part II of the [HTML Exercises](https://github.com/rithmschool/prework_exercises/tree/master/html_exercises)

### Additional Resources

#### [⇐ Previous](./02-html-part-1.md) | [Table of Contents](./readme.md) | [Next ⇒](./04-css-part-1.md)