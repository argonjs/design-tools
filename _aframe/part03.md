---
layout: page
title: 'Lesson 3: CSSObjects'
---
> Download [Argon4](http://argonjs.io/argon-app) and the [Tutorial Source Code](https://github.com/argonjs/design-aids/tree/gh-pages/code). <br> This tutorial uses the *cssobject* and *resources* directories.<br> **[Demo in Argon4](https://rawgit.com/argonjs/design-tools/gh-pages/code/cssobject/index.html)**


In Lesson 2 we saw how to place boxes and other geometric objects in the scene. But what if you want to put text and images in the scene as well: that is, the materials you are used to creating and manipulating on a web page using html and css? Suppose you want to place a label reading "Argon + Aframe" above a box in the space. We can do this by using CSSObjects. 

Displaying graphic objects on a computer screen is called "rendering," In order to render objects, you need (not surprisingly) a renderer, and there are different kinds. For Argon-aframe there are currently two available renderers: the WebGL renderer and a CSS renderer. The names WebGL and CSS refer to different graphic systems, and each is preferred for certain kinds of objects. In Argon, you can combine 3D objects using the WebGL renderer with 3D CSSobjects (of text or 2D image) using the CSS renderer. 

The previous Lesson 2 showed you how to create simple 3D content for the WebGL renderer such as `a-box`. Now we create the label as a CSSObject. 

First, here is the css that defines the class `boxface`. It can go in the `<head>` of the html file (along with the script tags we have in lesson 2). 
 
{% highlight html %}
.boxface {
    opacity: 0.5;
    width: 90px;
    height: 90px;
    font-size: 25px;
    text-align: center;
    color: black;
    background: rgba(127,255,255,0.85);
    outline: 5px solid rgba(12,25,25,1.0);
    border: 0px;
    margin-bottom: 0px;
    padding: 0px 0px;
    
}
{% endhighlight %}
 
Now in the `<body>` of the html file, we put:  
{% highlight html %}
    <div hidden>
      <div id="mydiv" class="boxface">Argon<br>+<br>AFrame</div>
    </div>
    <ar-scene>
      <a-entity id="helloworld" position="0 -1 -8">
        <a-box position="-1 0.5 1" rotation="0 45 0" width="1" 
               height="1" depth="1"  color="#4CC3D9" ></a-box>
        <a-entity position="0 3 0" rotation="0 45 0">
            <a-entity css-object="div: #mydiv" scale="0.01 0.01 0.01" rotation="0 0 0" position="0 0 0.5">
            </a-entity>
        </a-entity>
      </a-entity>
    </ar-scene>
{% endhighlight %}

Most of these tags are familiar from Lesson 2. You will recognize `<ar-scene>` to define the whole scene as well as the first `<a-entity>` and the `<a-box>`.  Below that you will see nested entity tags. `<a-entity position="0 3 0">` positions the whole nested group at x = 0;y=3;z=0. This will put the label 3 meters above origin (because y indicates up and down) and so above the box; it also rotates the label by 45 degrees along the y axis (so that the text will face the camera). 

The next entity is the one that actually defines the CSSObject:

{% highlight html %}
   <a-entity css-object="div: #mydiv" scale="0.01 0.01 0.01" rotation="0 0 0" position="0 0 0.5"></a-entity>
{% endhighlight %}

Notice that the `css-object` component takes a div as its parameter. You see the div id is `#mydiv`.  `mydiv` is defined as the id of the div shown in the code above: it is the div that holds the text `Argon<br>+<br>+Aframe`. The effect of this component is that the div that will be transformed into a 3D CSSObject, which means that it will be rendered in the 3D space with the scale, rotation, and relative positions indicated by the other components in the tag.  

A note about size: The CSS elements are sized such that 1 unit (1px in this example) is 1 meter, so conventionally sized CSS elements will be huge. The CSS class `boxface` above is 90 pixels by 90 pixels, which would translate to 90 meters by 90 meters. The CSSObject has therefore been scaled to .01 in all dimensions, which brings the box down to .9 meters in height and width.'
