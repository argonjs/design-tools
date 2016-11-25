---
layout: page
title: 'Lesson 9: Panoramas'
---

A simplified panorama example with one panorama. Introducing the concept of an different reality

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



