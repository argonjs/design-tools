---
layout: page
title: 'Lesson 2a: Asimple Argon-aframe experience with CSSObjects'
---

Explain how to create CSS Objects in addition to the WebGL objects - explain the difference. 

The `<ar-scene>` supports an optional CSS renderer, that has been designed to work with
Argon's stereo viewer mode.  The CSS content is positioned in front of the WebGL content 
(since the web browsers do not allow CSS and WebGL content to be rendered with a shared 
3D depth bufffer).

To add an HTML/CSS element to the 3D scene, the `css-object` component is used.  It takes
one or two CSS DOM references as it's properties, specifying the DOM elements to position in
in 3D.  If only one DOM element is provided, it will be `clone()`ed when Argon displays
the element in stereo (since one DOM element can only be displayed in one place.)  If a second
element is provided, it will be used for the right view in stereo mode.

The CSS elements are sized such at 1 units (1px in this example) is 1 meter, so the elements
will probably have to be scaled appropriately.  Since the web create the visual detail of a 
DOM element based on it's size, with a 100 unit element having ten times the resolution as
a 10 unit element, you should size and scale your DOM elements to balance detail vs rendering 
cost (higher resolution elements yield higher resolution textures and are slower to render).

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

{% highlight html %}
    <div hidden>
      <div id="mydiv" class="boxface">Argon<br>+<br>AFrame</div>
      <div id="mydiv2" class="boxface">WebGL<br>+<br>CSS</div>
    </div>
    <ar-scene>
      <a-entity id="helloworld" position="0 -1 -8">
        <a-box position="-1 0.5 1" rotation="0 45 0" width="1" 
               height="1" depth="1"  color="#4CC3D9" ></a-box>
        <a-entity position="0 3 0">
          <a-entity rotation="0 45 0">
                  <a-entity css-object="div: #mydiv" scale="0.01 0.01 0.01" rotation="0 0 0" position="0 0 0.5"></a-entity>
                  <a-entity css-object="div: #mydiv2" scale="0.01 0.01 0.01" rotation="0 -90 0" position="-0.5 0 0"></a-entity>
          </a-entity>
        </a-entity>
      </a-entity>
    </ar-scene>
{% endhighlight %}