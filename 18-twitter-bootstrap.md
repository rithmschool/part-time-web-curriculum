#### [⇐ Previous](./17-jQuery-events.md) | [Table of Contents](./readme.md) | [Next ⇒](./19-deploying-static-sites.md)

# Twitter Bootstrap

### Objectives:

By the end of this chapter, you should be able to:

- Explain what Twitter Bootstrap is and include the Bootstrap stylesheet in an application
- Utilize the grid system Bootstrap provides to create a responsive design
- Use Bootstrap components to quickly style applications
- Include Bootstrap.js to add dynamic behavior in an application

### Including Twitter Bootstrap

You can include Bootstrap quite a few ways: you can download the code, use a CDN, or use a package manager (e.g. npm/bower) to install it. For now, we will be using the CDN as it is the easiest way to get started. If you head to [http://getbootstrap.com/getting-started/#download](http://getbootstrap.com/getting-started/#download), you can copy and paste the CDN link tag into your HTML file and you will have Bootstrap right away! 

As an aside, wondering what a CDN is? Let us [google that for you](http://lmgtfy.com/?q=what+is+a+cdn)!

### Layout

Probably the most commonly used feature of Bootstrap is its grid system. With the right combination of CSS classes, you can build sophisticated grids (based on 12 columns) to lay out your page. Bootstrap will handle the responsive design based on the classes that you choose.

From the docs: 

>Bootstrap includes a responsive, mobile first fluid grid system that appropriately scales up to 12 columns as the device or viewport size increases. It includes predefined classes for easy layout options.

> - Rows must be placed within a .container (fixed-width) or .container-fluid (full-width) for proper alignment and padding.

> - Use rows to create horizontal groups of columns.

> - Content should be placed within columns, and only columns may be immediate children of rows.

> - Predefined grid classes like .row and .col-xs-4 are available for quickly making grid layouts. Less mixins can also be used for more semantic layouts.

> - Columns create gutters (gaps between column content) via padding. That padding is offset in rows for the first and last column via negative margin on .rows.

> - The negative margin is why the examples below are outdented. It's so that content within grid columns is lined up with non-grid content.

> - Grid columns are created by specifying the number of twelve available columns you wish to span. For example, three equal columns would use three .col-xs-4.

> - If more than 12 columns are placed within a single row, each group of extra columns will, as one unit, wrap onto a new line.

> - Grid classes apply to devices with screen widths greater than or equal to the breakpoint sizes, and override grid classes targeted at smaller devices. Therefore, e.g. applying any .col-md-* class to an element will not only affect its styling on medium devices but also on large devices if a .col-lg-* class is not present.

[http://getbootstrap.com/css/#grid-options](http://getbootstrap.com/css/#grid-options)

```html
<!-- Stack the columns on mobile by making one full-width and the other half-width -->
<div class="row">
  <div class="col-xs-12 col-md-8">.col-xs-12 .col-md-8</div>
  <div class="col-xs-6 col-md-4">.col-xs-6 .col-md-4</div>
</div>

<!-- Columns start at 50% wide on mobile and bump up to 33.3% wide on desktop -->
<div class="row">
  <div class="col-xs-6 col-md-4">.col-xs-6 .col-md-4</div>
  <div class="col-xs-6 col-md-4">.col-xs-6 .col-md-4</div>
  <div class="col-xs-6 col-md-4">.col-xs-6 .col-md-4</div>
</div>

<!-- Columns are always 50% wide, on mobile and desktop -->
<div class="row">
  <div class="col-xs-6">.col-xs-6</div>
  <div class="col-xs-6">.col-xs-6</div>
</div>
```

If we want to offset columns (add columns of whitespace) we can do that with offset classes:

```html
<div class="row">
  <div class="col-md-4">.col-md-4</div>
  <div class="col-md-4 col-md-offset-4">.col-md-4 .col-md-offset-4</div>
</div>
<div class="row">
  <div class="col-md-3 col-md-offset-3">.col-md-3 .col-md-offset-3</div>
  <div class="col-md-3 col-md-offset-3">.col-md-3 .col-md-offset-3</div>
</div>
<div class="row">
  <div class="col-md-6 col-md-offset-3">.col-md-6 .col-md-offset-3</div>
</div>
```

We can also nest rows inside of each other. Every new row gains access to its own 12-column grid system: 

```html
<div class="row">
  <div class="col-sm-9">
    Level 1: .col-sm-9
    <div class="row">
      <div class="col-xs-8 col-sm-6">
        Level 2: .col-xs-8 .col-sm-6
      </div>
      <div class="col-xs-4 col-sm-6">
        Level 2: .col-xs-4 .col-sm-6
      </div>
    </div>
  </div>
</div>
```

Here is another grid example with nesting:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <!-- Latest compiled and minified CSS -->
  <link rel="stylesheet" href="http://netdna.bootstrapcdn.com/bootstrap/3.1.1/css/bootstrap.min.css">

  <!-- Optional theme -->
  <link rel="stylesheet" href="http://netdna.bootstrapcdn.com/bootstrap/3.1.1/css/bootstrap-theme.min.css">
  <style>
    .left1 {
      background-color: red;
    }
    .right1 {
     background-color: blue;
    }
    .inside1 {
     background-color: green;
    }
    .inside2 {
      background-color: orange;
    }
    .offsetExample {
      background-color: magenta;
    }

  </style>
</head>
<body>
<div class="container text-center">
  <div class="row">
    <div class="col-md-6 col-sm-6 col-xs-12 left1">
      One Col
    </div>
    <div class="col-md-6 col-sm-6 col-xs-12 right1">
    Two Col
      <div class="row">
        <div class="col-md-6 col-sm-8 col-xs-10 inside1">
          L
        </div>
        <div class="col-md-6 col-sm-4 col-xs-2 inside2">
          R
        </div>
      </div>
    </div>
  </div>
  <div class="row">
  <div class="col-md-6 col-md-offset-3 offsetExample">
      I AM A COL MD 6 THAT IS OFFSET
  </div>
  </div>

</div>
</body>
</html>
```

### Typography and Buttons

Bootstrap's global default font-size is 14px, with a line-height of 1.428. This is applied to the <body> and all paragraphs. You can also use classes like `lead` for making paragraphs stand out, as well as some [inline](http://getbootstrap.com/css/#type-inline-text) text elements for additional modification.

Bootstrap has quite a few colors and sizes for [buttons](http://getbootstrap.com/css/#buttons). Here are some examples:

```html 
<!-- Standard button -->
<button type="button" class="btn btn-default">Default</button>

<!-- Provides extra visual weight and identifies the primary action in a set of buttons -->
<button type="button" class="btn btn-primary">Primary</button>

<!-- Indicates a successful or positive action -->
<button type="button" class="btn btn-success">Success</button>

<!-- Contextual button for informational alert messages -->
<button type="button" class="btn btn-info">Info</button>

<!-- Indicates caution should be taken with this action -->
<button type="button" class="btn btn-warning">Warning</button>

<!-- Indicates a dangerous or potentially negative action -->
<button type="button" class="btn btn-danger">Danger</button>

<!-- Deemphasize a button by making it look like a link while maintaining button behavior -->
<button type="button" class="btn btn-link">Link</button>

<p>
  <button type="button" class="btn btn-default btn-lg">Large button</button>
</p>
<p>
  <button type="button" class="btn btn-default">Default button</button>
</p>
<p>
  <button type="button" class="btn btn-default btn-sm">Small button</button>
</p>
<p>
  <button type="button" class="btn btn-default btn-xs">Extra small button</button>
</p>
<p>
    <button type="button" class="btn btn-primary btn-lg btn-block">Block level button</button>
</p>
```

### Tables

Bootstrap can quickly turn your tables into very nice and even responsive ones! By adding the class of `table`, `table-striped`, `table-hover`, and `table-bordered`, you can change the look of tables quite easily. Try it out!

### Forms

Bootstrap also gives you a whole suite of classes for building forms, both horizontally and with a block layout.

```html
<form>
  <div class="form-group">
    <label for="exampleInputEmail1">Email address</label>
    <input type="email" class="form-control" id="exampleInputEmail1" placeholder="Email">
  </div>
  <div class="form-group">
    <label for="exampleInputPassword1">Password</label>
    <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password">
  </div>
  <div class="form-group">
    <label for="exampleInputFile">File input</label>
    <input type="file" id="exampleInputFile">
    <p class="help-block">Example block-level help text here.</p>
  </div>
  <div class="checkbox">
    <label>
      <input type="checkbox"> Check me out
    </label>
  </div>
  <button type="submit" class="btn btn-default">Submit</button>
</form>
```

#### Inline Forms

Here is an example of an inline form:
```html
<form class="form-inline">
  <div class="form-group">
    <label for="exampleInputName2">Name</label>
    <input type="text" class="form-control" id="exampleInputName2" placeholder="Jane Doe">
  </div>
  <div class="form-group">
    <label for="exampleInputEmail2">Email</label>
    <input type="email" class="form-control" id="exampleInputEmail2" placeholder="jane.doe@example.com">
  </div>
  <button type="submit" class="btn btn-default">Send invitation</button>
</form>
```

### Components

Bootstrap has over a dozen reusable components built to provide iconography, dropdowns, input groups, navigation, alerts, and much more. You can see them here - 
[http://getbootstrap.com/components/](http://getbootstrap.com/components/). We will be examining a couple of them, but you will get much more practice in the assignment!

### Glyphicons

Bootstrap Includes over 250 icons which are part of the Glyphicon Halflings set. You can see all of them and their corresponding classes [here](http://getbootstrap.com/components/#glyphicons)

To add one, use a span tag and add a class like this:

```html
`<span class="glyphicon glyphicon-search"</span>`
```

Note: `glyphicon` is really easy to misspell. If you're trying to use an icon and it's not showing up on the page, make sure you haven't typed `glpyhicon`, `gylphicon`, or some other annoying variation of `glyphicon`. When in doubt, copy and paste from the docs!

### Navbar

Bootstrap makes it very easy to add styled navigation to a website with its navbar component. You can see how it looks here (we've toned down the example from the website a bit to make it easier to digest):

```html
<nav class="navbar navbar-default">
  <div class="container-fluid">
    <!-- Brand and toggle get grouped for better mobile display -->
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="#">Brand</a>
    </div>

    <!-- Collect the nav links, forms, and other content for toggling -->
    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <ul class="nav navbar-nav">
        <li class="active"><a href="#">Link <span class="sr-only">(current)</span></a></li>
        <li><a href="#">Link</a></li>
      </ul>
      <form class="navbar-form navbar-left" role="search">
        <div class="form-group">
          <input type="text" class="form-control" placeholder="Search">
        </div>
        <button type="submit" class="btn btn-default">Submit</button>
      </form>
      <ul class="nav navbar-nav navbar-right">
        <li><a href="#">Link</a></li>        
      </ul>
    </div><!-- /.navbar-collapse -->
  </div><!-- /.container-fluid -->
</nav>
```

#### A word of advice

As with many tools, it's easier to read through the Bootstrap documentation and feel like you understand it than it is to implement Bootstrap's features in practice. The best way to reach mastery using Bootsrap is, well, to use Bootstrap. A lot. Build some simple webpages and add a couple of Bootstrap components. Break things and fix them. This page should hopefully serve as a useful reference, but the only way you'll learn how to use Bootstrap is to practice using Bootstrap regularly.

### Bootstrap JS

While Bootstrap is a CSS Framework, it comes with some handy JavaScript to add dynamic interactivity to your page. Fortunately, to get started with this you do not need to know any JavaScript (unless you would like to customize some of these things). However, you must know that bootstrap.js (the extension for JavaScript) depends on another common JavaScript library called jQuery. Therefore, we must include the script for jQuery before the script for bootstrap JS. Below is the script for jQuery

```html
<script src="https://code.jquery.com/jquery-2.2.3.min.js" integrity="sha256-a23g1Nt4dtEYOj7bR+vTu7+T8VP13humZFBJNIYoEJo=" crossorigin="anonymous"></script>
```

When combined with bootstrap CSS + JS - here is what that all looks like: 

```html
<!-- Latest compiled and minified CSS -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" integrity="sha384-1q8mTJOASx8j1Au+a5WDVnPi2lkFfwwEAa8hDDdjZlpLegxhjVME1fgjWPGmkzs7" crossorigin="anonymous">

<!-- Optional theme -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap-theme.min.css" integrity="sha384-fLW2N01lMqjakBkx3l/M9EahuwpSfeNvV63J5ezn3uZzapT0u7EYsXMjQV+0En5r" crossorigin="anonymous">

<!-- jQuery -->
<script src="https://code.jquery.com/jquery-2.2.3.min.js" integrity="sha256-a23g1Nt4dtEYOj7bR+vTu7+T8VP13humZFBJNIYoEJo=" crossorigin="anonymous"></script>

<!-- Latest compiled and minified JavaScript -->
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js" integrity="sha384-0mSbJDEHialfmuBBQP6A4Qrprq5OVfW37PRR3j5ELqxss1yVqOtnepnHVP9aJ7xS" crossorigin="anonymous"></script>
```

Now that you have Bootstrap's JavaScript - you can add a [carousel](https://getbootstrap.com/javascript/#carousel), [modal](https://getbootstrap.com/javascript/#modals), [popover](https://getbootstrap.com/javascript/#popovers) and more!

As an aside, in case you're wondering what the `integrty` and `crossorigin` attributes are doing, it's part of a security measure used when fetching resources from a CDN. If you'd like to read more about these attributes, [check out the docs](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity).

### Bootswatch

Bootswatch is a wonderful open source set of themes for Bootstrap to add some more customization and flavor so that your page doesn't look like every other Bootstrap page. You can check it out [here](https://bootswatch.com/)

To include it you can click the "Download" button and copy the CSS to a file and link to it using a `link` tag. You can also access the themes via CDN [here](https://www.bootstrapcdn.com/bootswatch/).

### Exercise

- Complete the [Bootstrap Mocks Exercises](https://github.com/rithmschool/prework_exercises/tree/master/bootstrap_mocks)

### Additional Resources

#### [⇐ Previous](./17-jQuery-events.md) | [Table of Contents](./readme.md) | [Next ⇒](./19-deploying-static-sites.md)