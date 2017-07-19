---
layout: page
title: 'Lesson 9: Panoramas'
---
> Download [Argon4](http://argonjs.io/argon-app) and the [Tutorial Source Code](https://github.com/argonjs/design-aids/tree/gh-pages/code). <br> This tutorial uses the *panorama* and *resources* directories.<br> **[Demo in Argon4: Simple panorama:](https://rawgit.com/argonjs/design-tools/gh-pages/code/panorama/simple.html)****[Panorama with 3D objects](https://rawgit.com/argonjs/design-tools/gh-pages/code/panorama/simple-objects.html)****[Demo in Argon4: Multiple panoramas](https://rawgit.com/argonjs/design-tools/gh-pages/code/panorama/multiple.html)**

{% include lesson9vid.html %}

The default background for Argon is the view offered by the live video camera on the phone or tablet. Instead of the video, you can substitute a 360-degree panoramic image as the background. Panoramas offer a number of compelling design options. If the user cannot get to a specific location, such as a museum or historic site, the panorama can convey what the site looks like. The AR experience can play over the panorama. 

To display a panoramic backgroud, Argon needs an image in a special format called an 'equirectangular projection." You can make such a photo yourself using a relatively inexpensive panoramic camera such as the [Ricoh Theta S](https://theta360.com/en/about/theta/s.html). You can also take multiple images with a DLSR camera and stitch them into an equirectangular projection using a stitcher program such as [PTGui](https://www.ptgui.com). The resulting image should have an aspect ratio (width to height) of 2-1. 5000x2500 pixels is a good size. If the image is too large, it may fail to load. 

Once you have the equirectangular image as a .jpg or .png file, then you can create the panorama in Argon:

{% highlight html %}
<html>
  <head>
    <title>Hello, World! Argon + A-Frame</title>
    <meta name="description" content="Panorama Argon + A-Frame">
    <script src="https://aframe.io/releases/0.5.0/aframe.min.js"></script>
    <script src="https://rawgit.com/argonjs/argon/develop/dist/argon.js"></script>
    <script src="https://rawgit.com/argonjs/argon-aframe/master/dist/argon-aframe.js"></script>
  </head>
  <body>
    <ar-scene desiredreality="src:url(../resources/reality/panorama/index.html);" panorama="src:url(panoramas/cent.jpg);lla:'-84.3931 33.7608 309';initial:true;">

    </ar-scene>
  </body>
</html>
{% endhighlight %}

You attach two components to the `<ar-scene>`:  `desiredreality` and `panorama`. Let's take the second component first. `panorama` has three attributes. The source is the image file (Centennial Olympic Park in Atlanta, Georgia, USA). The lla specifies the geoposition where the panorama was taken (you can find this on Google Maps and elsewhere). Right now, the geoposition information (long and lat) is just stored, but it could be useful in an application later. The `initial` attribute indicates that this panorama is to be displayed in the background when the application starts up. Since it is the only panorama in this example, there is no other choice. However, you can declare multiple panoramas in this component and switch among them (see below). In that case, the `initial` attribute becomes useful.


## Putting A-Frame objects in the panoramic reality  

This example is empty so far: we  have the panoramic background, but nothing in the 3D space itself. But the panorama reality is just like the live video background. We can put any of the other A-Frame entities in the scene as well. For example, the geometric objects in our basic example:


{% highlight html %}
<html>
  <head>
    <title>Hello, World! Argon + A-Frame</title>
    <meta name="description" content="Panorama Argon + A-Frame">
    <script src="../resources/js/aframe.js"></script>
    <script src="../resources/js/argon.min.js"></script>
    <script src="../build.js"></script>
  </head>
  <body>
    <ar-scene desiredreality="src:url(../resources/reality/panorama/index.html);" panorama="src:url(panoramas/cent.jpg);lla:'-84.3931 33.7608 309';initial:true;">
      <a-entity id="helloworld" position="0 -1 -8">
      <a-sphere position="0 1.25 -1" radius="1.25" color="#EF2D5E"></a-sphere>
      <a-box position="-1 0.5 1" rotation="0 45 0" width="1" height="1" depth="1"  color="#4CC3D9"></a-box>
      <a-cylinder position="1 0.75 1" radius="0.5" height="1.5" color="#FFC65D"></a-cylinder>
      <a-plane rotation="-90 0 0" width="4" height="4" color="#7BC8A4"></a-plane>
      </a-entity>
    </ar-scene>
  </body>
</html>
{% endhighlight %}

Now the sphere, box, cylinder, and plane will all appear inside the space with the panorama of Centennial Olympic Park in the background. 


## Switching among multiple panoramas  

Here is a more complex example that features four different panoramas. The user switches between them by pressing a button at the bottom of the screen.

Here are the links to various scripts as usual:
{% highlight html %}
<html>
  <head>
    <title>Hello, World! Argon + A-Frame</title>
    <meta name="description" content="Hello, World! Argon + A-Frame">
    <script src="../resources/js/aframe.js"></script>
    <script src="../resources/js/argon.min.js"></script>
    <script src="../build.js"></script>
    <script src="../resources/js/CSS3DArgonRenderer.js"></script>
    <script src="../resources/js/CSS3DArgonHUD.js"></script>
    <script src="../resources/js/aframe-look-at-component.js"></script>
	  <link rel="stylesheet" type="text/css" href="../resources/style.css">
  </head>

{% endhighlight %}

The body begins with a menu and the `<ar-scene>` tag.

{% highlight html %}  
  <body>
    <div id="menu" class="menu"></div>
    <ar-scene desiredreality="src:url(../resources/reality/panorama/index.html);" panorama__aqui="src:url(panoramas/aqui.jpg);lla:-84.3951 33.7634 206;initial:true;" panorama__cent="src:url(panoramas/cent.jpg);lla:'-84.3931 33.7608 309';" panorama__high="src:url(panoramas/high.jpg);lla:'-84.38584 33.79035 289';" panorama__pied="src: url(panoramas/pied.jpg);lla:'-84.37427 33.78577 271';">
    </ar-scene>
{% endhighlight %}    

In the `<ar-scene>` tag above, the `desiredreality` component points again to the panorama reality file. In this case, however, there are four panorama components instead of one. The name extension (after the `__`) becomes the identifier for that panorama. (aqui is the Georgia Aquarium; cent is Centennial Olympic Park; high is the High Museum; pied is Piedmont Park – all in Atlanta, Georgia.)

The following section of the code creates the menu that switches between the four panoramas and associates a click event handler with each of the four panoramas:

{% highlight html %}    
    
    <script>
      var arScene = document.querySelector('ar-scene');
      var content = document.querySelector('#helloworld');

      // the ar-camera has an argon reference frame attached, so when it gets it's first value,
      // we'll get this event 
      arScene.addEventListener("referenceframe-statuschanged", function () {
        var camera = document.querySelector('ar-camera');
        var vec = camera.object3D.getWorldDirection();
        vec.multiplyScalar(-10);
        vec.y -= 1;
        content.setAttribute("position", {x: vec.x, y: vec.y, z: vec.z});
      });

      var panoramas = [
        { text: 'Georgia Aquarium', name: 'aqui' },
        { text: 'Centennial Park', name: 'cent' },
        { text: 'High Museum', name: 'high' },
        { text: 'Piedmont Park', name: 'pied'}
      ];

      var currentPanorama;
      // get the menu element
      var menu = document.getElementById('menu');
      // add buttons to the menu for each panorama
      panoramas.forEach(function (p) {
          var button = document.createElement('button');
          button.textContent = p.text;
          menu.appendChild(button);
          // when a button is tapped, have the reality fade in the corresponding panorama
          button.addEventListener('click', function () {
              arScene.sceneEl.emit('showpanorama', { name: p.name });     
          });
      });
      
      arScene.addEventListener('argon-initialized', function(evt) {
        arScene.sceneEl.hud.appendChild(menu);
        arScene.sceneEl.argonApp.focusEvent.addEventListener(function () {
            document.getElementById('menu').style.display = 'block';
        });
        arScene.sceneEl.argonApp.blurEvent.addEventListener(function () {
            document.getElementById('menu').style.display = 'none';
        });      
      });
    </script>
  </body>
</html>
{% endhighlight %}


In the code above, note the `arScene.addEventListener`. You need to make sure that argon is initialized before you begin any further actions, such as appending the menu to the scene. 

## The Panorama Reality

The Panorama Reality is one of three realities (backgrounds) that are currently available. The other two are the standard video reality (provided by the phone's camera) and the Google Streetview, which is a panorama provided by accessing Google Streetview for a particular location (long and lat).  





