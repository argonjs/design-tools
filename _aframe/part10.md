---
layout: page
title: 'Lesson 10: Image-tracking'
---

Geolocation using GPS and other positioning information is one way to locate objects in the world (see Lessons 6 and 7). But geolocaiton is inaccurate and therefore useful only for the large-scale placement of digital objects and information. That is, if you want the user to see a 3D model of a building located on the site where it is going to be constructed, then geolocaiton will work fairly well. If the user is standing some distance from the site, it doesn't matter much whether the model is misplaced every by 10 or more meters. However, if you want to create a table-top AR game where virtual zombies run across the player's desk, then GPS is far too inaccurate. When you want precise registration, you need to use image-tracking. For such purposes, Argon uses the [Vuforia](http://www.vuforia.com) image-tracking system. 

Vuforia keeps a database of images for your application. When the phone videocamera shows one of the images, Vuforia recognizes it and computes the position and orientation of the phone relative to the image. This allows Argon to position 3D objects with precision (usually in the space above or in front of the image). You can see how this works by running this example. First you need to print out this generic image of stones XXXX (you can also bring up the stones image on a desktop computer screen without printing it out). Then load this application into Argon XXXX.  Now when you point the phone's camera at the stones iamges, you will see a bronze head appear right above the image. 

Here is the code to make this happen:

Start with the usual scripts in the header. Note that we have a special splash.css file to create a splash screen while assets are loading the image database is initialized. 

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
  
  Then in the body of the page create the `ar-scene` with the special components for the image database
  
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

    <ar-scene vuforiakey="#vuforiakey"
              vuforiadataset__stonesandchips="src:url(../resources/datasets/StonesAndChips.xml);">
 
 {% endhighlight %}
  
  Then in the body of the page create the `ar-scene` with the special components for the image database
  
  {% highlight html %}
 
      <a-assets>
        <a-asset-item id="vuforiakey" src="key.txt"></a-asset-item>
        <a-mixin id="light" geometry="primitive: sphere; radius: 1.5"
                 material="color: #FFF; shader: flat"
                 light="color: #DDDDFF; distance: 120; intensity: 2; type: point">
        </a-mixin>
        <a-mixin id="torus-knot" geometry="primitive: torusKnot"
                 material="color: red"></a-mixin>
      </a-assets>

      <!-- attach to stones target. x/y in the plane, z up -->
      <ar-frame id="frame" trackvisibility="true" visible="false" parent="vuforia.stonesandchips.stones" position="0 0 0" rotation="0 0 0">
       <a-entity scale="0.003 0.003 0.003">
        <a-entity id="stuff"></a-entity>

        <!-- Lights. -->
        <a-entity position="0 0 25">
          <a-animation attribute="rotation" to="0 0 360"
                      repeat="indefinite" easing="linear" dur="4096">
          </a-animation>
          <a-entity mixin="light" position="15 0 0"></a-entity>
        </a-entity>

        <a-entity position="0 0 25">
          <a-animation attribute="rotation" to="360 0 0"
                      repeat="indefinite" easing="linear" dur="4096">
          </a-animation>
          <a-entity mixin="light" position="0 0 25"></a-entity>
        </a-entity>
       </a-entity>
      </ar-frame>      
    </ar-scene>
    <script src="app.js"></script>
  </body>
</html>


{% endhighlight %}

