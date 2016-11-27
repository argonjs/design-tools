---
layout: page
title: 'Lesson 3: Creating a cursor'
---

In an html page, the user typically selects items by clicking on with with the cursor. You can also add a cursor to the 3D world of argon-aframe. You add the cursor to the camera, which means that it will appear in a shape you determine and at a place you specify relative to the center of the screen. This cursor shape will move as the user moves the phone. (If the user is wearing Google cardboard, then turning her head will move the cursor.) The cursor can be activated by a click user or simply by keeping it steady over an object for a length of time (the fuse time).

	Look at the example below:

{% highlight html %}
  <body>
    <ar-scene>
      <a-entity id="helloworld" position="0 -1 -8">
        <a-sphere position="0 1.25 -1" cursor-listener radius="1.25" color="#EF2D5E" ></a-sphere>
      </a-entity>
      <ar-camera>
        <a-entity id="myCursor" cursor="fuse:true; fuse-timeout: 1000"
                    position="0 0 -0.1"
                    geometry="primitive:ring; radiusInner: 0.001; radiusOuter: 0.0015"
                    material="color: #2E3A87; opacity:0.3;">          
        </a-entity>
      </ar-camera>
    </ar-scene>
 {% endhighlight %}   
 
 This simple `<ar-scene>` consists of two things: a sphere and the ar-camera. The camera has a cursor entity attached to it. The cursor entity is to set "fuse," which means that it will function to select an object by just keeping the cursor over the object, in this case for 1000 miliseconds = 1 sec. The other components of the cursor entity define how it looks: a ring of a certain color and 30% opacity.  (You can define the shape and color of your own cursor, if you don't like the ring.)
 
At this point the cursor is defined, but it doesn't do anything when the user holds it over an object. In order to make the cursor act, we need to add javascript. This javascript code creates and registers a new component. You can learn about components in Lesson 12. Here you can just examine the code to see what it does. Note that the new component is called `cursor-listener`. It is defined in the javascript, and it is attached to the sphere in the code above. This means that cursor-listener will attach events to the sphere The sphere will react to the click-event, the mouseeneter-event, and the mouseleave-event. These events make the sphere reactive to the cursor.

{% highlight html %}   
    <script>
      AFRAME.registerComponent('cursor-listener', {
        init: function () {
          this.el.addEventListener('click', function (evt) {
            this.setAttribute('material', 'color', getRandColor());
            console.log('I was clicked at: ', evt.detail.intersection.point);
          });
          this.el.addEventListener('mouseenter', function (evt) {
            this.setAttribute('material', 'opacity', 0.5);
          });
          this.el.addEventListener('mouseleave', function (evt) {
            this.setAttribute('material', 'opacity', 1.0);
          });
        }
      });

{% endhighlight %}

