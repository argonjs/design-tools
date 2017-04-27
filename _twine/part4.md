---
layout: page
title: 'Part 4: CSS Styling in Twine'
---

> This lesson uses the first [example](https://github.com/blairmacintyre/oldfashioned/tree/master/examples/) from github. <br> Import the text file into Twine to open the project.


## Utilizing CSS Styling
You can utilize CSS for styling an Argon experience's layout, font, and presentation. We will be adding some CSS styling to the Twine expererience we created in the last lesson.

To create storywide styling, you must reference the story's id: `story`. We can style our story in a multitude of different ways. For example, we can specify "pointer events", which allow you to control when a graphic element becomes the target of mouse elements. "Auto" applies to all events. Other possible styling we can do includes choosing our font families, specifying background color, positioning our CSS elements, etc..

```css

#story {
  pointer-events: auto;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  padding: 10px;
  background-color:rgba(255,255,255,0.7);
  -webkit-backdrop-filter: blur(5px);
  position:absolute;
  bottom: 0px;
}

```

Using CSS styling, we can also influence how Argon treats obejcts that are in focus and those that are out of focus. To style elements that are in focus, simply style the `argon-focus` class, and for those that are out of focus, use the `argon-no-focus` class.

Add the code below and notice how in this example we make objects that are not focused notably more transparent.

```css

.argon-focus #story {
  transition: opacity 0.8s;
  visibility: visible;
  opacity: 1;
}

.argon-no-focus #story {
  transition: visibility 0s linear 0.8s, opacity 0.8s;
  visibility: visible;
  opacity: 0;

```

In the next lesson you will learn how to utilize panoramas in your AR experiences!