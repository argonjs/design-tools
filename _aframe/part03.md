---
layout: page
title: 'Lesson 3: Creating a cursor'
---

In an html page, the user typically selects items by clicking on with with the cursor. You can also add a cursor to the 3D world of argon-aframe. You add the cursor to the camera, which means that it will appear in a shape you determine and at a place you specify relative to the center of the screen. This cursor shape will move as the user moves the phone. (If the user is wearing Google cardboard, then turning her head will move the cursor.) The cursor can be activated by a click user or simply by keeping it steady over an object for a length of time (the fuse time). Look at the example below:

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
 
At this point the cursor is defined, but it doesn't have any effect on the objects in the scene. In order to make the cursor have an effect, we need to add javascript that "listens" for the cursor when it selects an object. We do this by registering a new "component". You can learn more about components in Lesson 12. They are a key feature of working with aframe (and argon-aframe).  Here you can see how this particular component works. The new component is called `cursor-listener`. It is coded in a script tag and "registered with aframe. Then this component can be attached to the sphere, as you see in this line from the html above:  

{% highlight html %}

<a-sphere position="0 1.25 -1" cursor-listener radius="1.25" color="#EF2D5E" ></a-sphere>

{% endhighlight %}

 The sphere will react to the click-event, the mouseeneter-event, and the mouseleave-event. These events make the sphere reactive to the cursor. Here is the component that makes this possible: 

{% highlight html %}   

    <script>
      AFRAME.registerComponent('cursor-listener', {
        init: function () {
          this.el.addEventListener('click', function (evt) {
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

The function defined in the component is executed once when the component is initialized for a particular object. It adds three eventListeners (for eventListeners see Lesson 4). One event fires when the user clicks on the particular object. When that happens the program prints the message 'I was clicked at: ' together with the point where the cursor indicated contact with the object.  The other two events fire when the cursor starts hovering over the object or moves away from the object. Hovering over the object will cause it to become translucent (opacity = .5) Moving away will cause the object to return to its full opacity. 

Obviously you can put any javascript code you want into these events. You could make audio play when the user clicks on the sphere, or you can start the sphere rotating, or display a text on the screne. This is how you introduce interactivity into the scene. 