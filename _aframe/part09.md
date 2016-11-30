---
layout: page
title: 'Lesson 9: Panoramas'
---

The default background for Argon is the view offered by the live video camera on the phone or tablet. Instead of the video, you can substitute a 360-degree panoramic image as the background. Panoramas offer a number of compelling design options. If the user cannot get to a specific location, such as a museum or historic site, the panorama can convey what the site looks like. The AR experience can play over the panorama. 

To display a panoramic backgroud, Argon needs an image in a special format called an 'equirectangular projection." You can make such a photo yourself using a relatively inexpensive panoramic camera such as the [Ricoh Theta S](https://theta360.com/en/about/theta/s.html). You can also take multiple images with a DLSR camera and stitch them into an equirectangular projection using a stitcher program such as [PTGui](https://www.ptgui.com). The resulting image should have an aspect ratio (width to height) of 2-1. 5000x2500 pixels is a good size. If the image is too large, it may fail to load. 



## Panorama Reality

The `panorama` component is added to the `<ar-scene>` entity to specify a geopositioned panoramic image for the custom
panorama reality (the panorama reality implements the "ael.gatech.panorama" reality protocol). 

Multiple components can be specified with the multiple component syntax 
(`panorama__` plus a name).  The name extension (after the `__`) becomes the identity
of that panorama, and is used to show the panorama by emitting a "showpanorama" event on 
the `<ar-scene>`.  For example, in this example:

{% highlight html %}
<ar-scene desiredreality="src:url(../resources/reality/panorama/index.html);"
      panorama__aqui="src:url(/panorama/panoramas/aqui.jpg);lla:-84.3951 33.7634 206;initial:true;">
</ar-scene>
{% endhighlight %}

The panorama has the identity `aqui`, and so it can be shown in the panoramic reality by emiting an event:


{% highlight html %}
var arScene = document.querySelector('ar-scene');
var menu = document.getElementById('menu');

var button = document.createElement('button');
button.textContent = "Aquarium";
menu.appendChild(button);
// when a button is tapped, have the reality fade in the corresponding panorama
button.addEventListener('click', function () {
    arScene.sceneEl.emit('showpanorama', { name: "aqui" });     
});
{% endhighlight %}

If the `initial` property is true, argon.js will attempt to load the panorama when the 
panorama reality is activated.





Then the second example with four, as in the current sample. 



