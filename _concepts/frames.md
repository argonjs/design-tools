---
layout: page 
title: Frame  
permalink: /concepts/frame/
---

Frames of reference in aframe and Argon-aframe

Aframe is a three-dimensional graphics systems (based on three.js). You need to tell it where to place any object (box, sphere, plane or more complicated objects) that you create. 3D space is labelled by a triplet of numerical values: x - y - z.  Imagine you  are looking at a computer screen the x axis is the horizontal dimension of the screen; y is the vertical; z is the direction into and out of the screen. Assume that the three axes meet in the center and on the surface of your screen; that is the origin (0, 0, 0).  So if you created an aframe box at (2, 3, -3), it would appear in the upper right hand quadrant of the screen: 2 x-units over to the right and 3-units up. The z value of -3 means that the box should appear 3 z-units into or behind the screen. By convention, a -z value is away from you, and a +z value is coming out of the screen toward you.

<<<<<<< HEAD
DIAGRAM HERE123
=======
{% include sample1_diagram.html %}
>>>>>>> pr/2

Another way to visualize and refer to this coordinate system is East-Up-South (EUS). The terminology imagines that you are standing on the surface of a map: East is the positive x direction, Up (from the map) is the positive y direction, and South is the positive z direction. So South (+z) is behind your back and North (-z) is in front of you.

Aframe employs this coordinate system in its position component, which you use constantly when you create objects. For example, to place the box we mentioned above, we would write:

{% highlight html %}
<a-box position="2 3 -3"></a-box>
{% endhighlight %}

This tag would place the box in the virtual space at 2 meters to the right, 3 meters up, and -3 meters (in) from the origin. Aframe (and argon) uses meters as the default.

The virtual camera is an entity too. So in aframe you can the position component to position the camera anywhere in the space. Where you position the camera and its direction will determine what you see the scene is rendered. 

[digram of camera] 

Note that in Argon aframe the situation with the camera is more complicated. There is a special entity called `<ar-camera>`, and it contains the aframe camera along with a special frame of reference `ar-user`. This is position of the user, that is the phone the user is holding. The `ar-camera` always stays with the user because its perspective must be the same as the phone's actual videocamera. Otherwise the 3D objects drawn in the scene would not be in their proper positions when the user looks at them through the phone's video screen.

{% include camera_moving.html %}

Long-lat as a frame of reference 
So far we have been talking about the frame of reference within the virtual graphic space of AR. For geopositioning to work, we need a frame of reference that relates to the earth itself. 
