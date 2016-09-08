#### [⇐ Previous](./04-css-part-1.md) | [Table of Contents](./readme.md) | [Next ⇒](./06-css-part-3.md)

# CSS Part II

### Objectives:

By the end of this chapter, you should be able to:

- Use different types of positioning to create more advanced layouts
- Understand what flexbox is and how it assists in creating challenging layouts

### Positioning

Positioning allows you to take an element on the page and control where and how it's positioned relative to things such as its original starting position, other elements, or even the window itself. The type of position we use will either remain in the document flow (relative) or take the element out of the document flow (absolute), just like floats do.

Once `position` is set, offset values can be set for `top`, `right`, `bottom`, `left`, and `z-index` (a 3D axis that we can use to stack elements on top of each other).

By default, the position of an element is set to `static`. `static` positioning and `relative` positioning are basically the same, but with one important difference: a statically positioned element won't respond to the offset properties listed above. If you set `top: 10px` on an element that is statically positioned, this style rule will simply be ignored.

#### Absolute Positioning vs. Relative Positioning

With `relative` positioning, elements are not removed from the document flow, and any offsets you place on the element will be _relative_ to its default position in the document flow. For example, if you set `position: relative;` on a div and then set the `top` offset to be `10px`, the div will be 10 pixels below where it would otherwise be (in other words, you're offsetting the div 10 pixels from the top). 

With `absolute` positioning, the situation is a little different. In this case, the element is removed from the document flow, and any offsets you place on the element will be relative to its parent, _provided its parent is not statically positioned!_ If the parent element _is_ statically positioned, then the offsets will be relative to the grandparent, provided the grandparent is not statically positioned. If the grandparent is statically positioned, we keep going up the chain until we find an element that is not statically positioned. If no such element exists, the offsets are relative to the `body`.

#### Fixed positioning

The fourth type of positioning is `fixed`. This behaves similar to absolute positioning, but elements with fixed positioning are **ALWAYS** positioned relative to the active viewport. Now, what's that mean? If you position, for example, a fixed element with a top offset of 50 pixels and a right offset of 100 pixels, the top right corner of the element will be positioned 50 pixels over to the left and 100 pixels down. Unlike with absolute positioning, scrolling the page content would not affect this element's position at all. It will remain in that position, no matter how the screen was resized or scrolled. It truly is fixed. 

Here is an example with relative and absolute positioning:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
  body {
    margin: 0; /*REMOVE BROWSER MARGIN*/
  }

  .red {
    background-color: red;
    position:  absolute;
    width: 400px;
    height: 400px;
    margin: auto; /*USE THIS TO CENTER THE DIV*/
    /*THESE POSITIONS ARE NOW 20 and 30 PX FROM THE BOUNDRY OF THE PARENT*/
    left: 20px;
    top: 30px;

    /*ONCE WE SET POSITION TO RELATIVE, ABSOLUTE, OR FIXED */
    /*WE HAVE ACCESS TO TOP, BOTTOM, LEFT AND RIGHT*/
    /*THINK OF THESE AS FROM THE ____ PUSH IT ___ PIXELS, */
    /*TOP 200 = PUSH 200 PIXELS FROM THE TOP*/
  }
  .wrapper {
    width: 800px;
    height: 1000px;
    margin: auto;
    background: #e3e3e3;
    position: relative;
  }
  </style>
</head>
<body>
  <div class="wrapper">
    <div class="red">

  </div>
  </div>
  <!-- IF THE PARENT OF THE DIV IS THE BROWSER WINDOW, ABSOLUTE/RELATIVE MAKES NO DIFFERENCE -->

  </div>
</body>
</html>
```

### Flexbox

From [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes): 

>The CSS3 Flexible Box, or flexbox, is a layout mode providing for the arrangement of elements on a page such that the elements behave predictably when the page layout must accommodate different screen sizes and different display devices. For many applications, the flexible box model provides an improvement over the block model in that it does not use floats, nor do the flex container's margins collapse with the margins of its contents.

>Many designers will find the flexbox model easier to use. Child elements in a flexbox can be laid out in any direction and can have flexible dimensions to adapt to the display space. Positioning child elements is thus much easier, and complex layouts can be achieved more simply and with cleaner code, as the display order of the elements is independent of their order in the source code. This independence intentionally affects only the visual rendering, leaving speech order and navigation based on the source order.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <link rel="stylesheet" href="style.css">
  <title>Document</title>
</head>
<body>
  <div class="container">
    <div class="first">
      First
    </div>
    <div class="second">
      Second
    </div>
    <div class="third">
      Third
    </div>
    <div class="fourth">
      Fourth
    </div>
    <div class="fifth">
      Fifth
    </div>
    <div class="sixth">
      Sixth
    </div>
  </div>
</body>
</html>
```


```css
div {
  width: 100px;
  height: 100px;
  color:white;
}

.container {
  display: flex;
  /*FLEX DIRECTION - can reverse etc*/
  flex-direction: column;
  background: #F60009;
  height: 500px;
  width: 500px;
}

.first {
  display: flex;
  background: #53007A;
  /*VERTICAL*/
  align-items: center;
  /*HORIZONTAL*/
  justify-content: space-around;
  /*ORDER  -1 first, highest last */
  order: 1;
}

.second {
  background: #FC9709;

}
.third {
  background: #A800DF;
  align-self: flex-end;
}

.fourth {
  background: #8BE7E6;
}

.fifth {
  background: #93B112;
}

.sixth {
  background: #E6F0BA;
  order: -1;
}
```
You can read more about flexbox [here](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes), [here](http://learnlayout.com/flexbox.html) and [here](https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties). For reference, here is a list of the most common properties you'll be manipulating when using flexbox:

`display` - this property is how you can initially set `flex` (as block level elements) or `inline-flex` to make your elements inline. By default, `display:flex` will set the `flex-direction` to have a value of `row`.

`justify-content` - this affects the space along the `flex-direction`. You can think of this as the horizontal alignment: 
  - top -> `flex-start`
  - center -> `center` 
  - bottom -> `flex-end`
  - even amount of space between elements -> `space-between`
  - even amount of space around elements -> `space-around`

This image, taken from an CSS-Tricks [article](https://css-tricks.com/almanac/properties/j/justify-content/) on `justify-content`, does a good job illustrating the difference between the values listed above:

![justify-content values](http://www.w3.org/TR/css3-flexbox/images/flex-pack.svg)

`align-items` - this affects the space perpendicular to `flex-direction`. You can think of this as the vertical alignment:
  - top -> `flex-start`
  - center -> `center` 
  - bottom -> `flex-end`

`flex-direction` - with the `row` value this will layout items in a row, and with the `column` value it will lay elements out in a column. These values can also have a `-reverse` added to them (`row-reverse` / `column-reverse` ) to reverse the ordering. When the flex direction is a column, `justify-content` changes to the vertical and `align-items` to the horizontal.

`order` - this property allows you to order items based on their position in the DOM. The order will start at 0, so anything lower will go higher and anything higher will go lower in the order.

`flex-basis` - The flex-basis CSS property specifies the flex basis which is the initial main size of a flex item. This property determines the size of the content-box.

`flex-grow` - The flex-grow CSS property specifies the flex grow factor of a flex item. It specifies what amount of space inside the flex container the item should take up.

`flex-shrink` - The flex-shrink CSS property specifies the flex shrink factor of a flex item. [https://developer.mozilla.org/en-US/docs/Web/CSS/flex-shrink](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-shrink)

`flex` - The flex CSS property is a shorthand property specifying the ability of a flex item to alter its dimensions to fill available space. Flex items can be stretched to use available space proportional to their flex grow factor or their flex shrink factor to prevent overflow. [https://developer.mozilla.org/en-US/docs/Web/CSS/flex](https://developer.mozilla.org/en-US/docs/Web/CSS/flex)

`flex-wrap` - The CSS flex-wrap property specifies whether flex items are forced into a single line or can be wrapped onto multiple lines. If wrapping is allowed, this property also enables you to control the direction in which lines are stacked. [https://developer.mozilla.org/en-US/docs/Web/CSS/flex-wrap](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-wrap)

### Exercises

- Finish the [CSS Exercises](https://github.com/rithmschool/prework_exercises/tree/master/css_exercises)
- Complete [Flexbox Defense](http://www.flexboxdefense.com/)
- Complete [Flexbox Froggy](http://flexboxfroggy.com/)
- Take one of the mocs you built from the CSS Exercises, and rebuild it using flexbox!

### Additional Resources

[https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes)

[https://philipwalton.github.io/solved-by-flexbox/](https://philipwalton.github.io/solved-by-flexbox/) - The "Better, Simpler Grid Systems" article is a good read before you get to the Twitter Bootstrap section.

#### [⇐ Previous](./04-css-part-1.md) | [Table of Contents](./readme.md) | [Next ⇒](./06-css-part-3.md)