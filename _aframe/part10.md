---
layout: page
title: 'Lesson 10: Image-tracking'
---
> Download [Argon4](http://argonjs.io/argon-app) and the [Tutorial Source Code](https://github.com/argonjs/design-aids/tree/gh-pages/code). <br> This tutorial uses the *vuforia* and *resources* directories.<br> **[Demo in Argon4](https://github.com/argonjs/design-aids/tree/gh-pages/code/vuforia/)**

{% include lesson10vid.html %}

Geolocation using GPS and other positioning information is one way to locate objects in the world (see Lessons 6 and 7). But geolocation is inaccurate and therefore useful only for the large-scale placement of digital objects and information. That is, if you want the user to see a 3D model of a building located on the site where it is going to be constructed, then geolocation will work fairly well. If the user is standing some distance from the site, it doesn't matter much whether the model is misplaced every by 10 or more meters. However, if you want to create a table-top AR game where virtual zombies run across the player's desk, then GPS is far too inaccurate. When you want precise registration, you need to use image-tracking. For such purposes, Argon uses the [Vuforia](http://www.vuforia.com) image-tracking system. 

Vuforia keeps a database of images for your application. When the phone camera shows one of the images, Vuforia recognizes it and computes the position and orientation of the phone relative to the image. This allows Argon to position 3D objects with precision (usually in the space above or in front of the image). You can see how this works by running this example. First, you need to print out this generic image of [stones](https://developer.vuforia.com/sites/default/files/sample-apps/targets/stones.pdf). (You can also bring up the stones image on a desktop computer screen without printing it out.) Then, load this application into Argon. Now when you point the phone's camera at the stones image, you will see a bronze head appear right above the image. 

Here is the code to make this happen. Start with the usual scripts in the header. (Note that we also have splash.css and app.css files to create an animated splash screen.)

{% highlight html %}

<html>
  <head>
    <title>Vuforia, with Argon + A-Frame</title>
    <meta name="description" content="Vuforia, with Argon + A-Frame">
    <link rel="stylesheet" type="text/css" href="../resources/splash.css">
    <link rel="stylesheet" type="text/css" href="app.css">
    <script src="../resources/js/aframe.min.js"></script>
    <script src="../resources/js/argon.min.js"></script>
    <script src="../build.js"></script>
    <script src="../resources/js/CSS3DArgonRenderer.js"></script>
    <script src="../resources/js/CSS3DArgonHUD.js"></script>
    <script src="../resources/js/aframe-look-at-component.js"></script>
  </head>
  {% endhighlight %}
  
Then in the body of the page, we create some divs. The first set instructs the user to point the phone at the stones target. This will appear at the bottom of the screen. The other divs are for creating an animated splash screen while the image database is being initialized. 
  
  {% highlight html %}

  <body>
    <div hidden>
      <div id="lookattarget" class="bottomScreen">Look at the "stones" target ...</div>
    </div>  
    <div id="loader-wrapper">
      <div class="splashtext">
        <h1>AFrame + Argon + Vuforia</h1>
        <h2 id="status">loading scripts...</h2>
      </div>

      <div id="loader"></div>
      <div class="loader-section section-left"></div>
      <div class="loader-section section-right"></div>
    </div>
{% endhighlight %}

  Here are the most important lines. The `<ar-scene>` tag here has two components: one gives the vuforia key; the other tells the system what image data set is being used. 
  
  {% highlight html %}
    <ar-scene vuforiakey="#vuforiakey"
              vuforiadataset__stonesandchips="src:url(../resources/datasets/StonesAndChips.xml);">
      <a-assets>
        <a-asset-item id="vuforiakey" src="key.txt"></a-asset-item>
      </a-assets>
      <!-- attach to stones target. x/y in the plane, z up -->
      <ar-frame id="frame" trackvisibility="true" visible="false" parent="vuforia.stonesandchips.stones" position="0 0 0" rotation="0 0 0">
       <a-entity scale="0.1 0.1 0.1">
      <a-sphere position="0 1.25 -1" radius="1.25" color="#EF2D5E"></a-sphere>
       </a-entity>
      </ar-frame>      
    </ar-scene>
    <script src="app.js"></script>
  </body>

{% endhighlight %}

