---
layout: page
title: 'Lesson 2: Writing a simple Argon-aframe experience'
---

Argon-aframe is built on top of aframe and allows you to make use of much of the exisitng aframe code. We will not go through aframe itself. For an explanation of the aframe entities, please consult the [aframe documentation](https://aframe.io/docs/0.3.0/introduction/). Instead, we will start by showing you how easy it is to "wrap" argon-aframe around aframe itself.  

Here is the code for the Hello World example in aframe:

{% highlight html %}
<html>
  <head>
    <meta charset="utf-8">
    <title>Hello, World! • A-Frame</title>
    <meta name="description" content="Hello, World! • A-Frame">
    <script src="../../../dist/aframe.js"></script>
  </head>
  <body>
    <a-scene>

      <a-sphere position="0 1.25 -1" radius="1.25" color="#EF2D5E"></a-sphere>
      <a-box position="-1 0.5 1" rotation="0 45 0" width="1" height="1" depth="1"  color="#4CC3D9"></a-box>
      <a-cylinder position="1 0.75 1" radius="0.5" height="1.5" color="#FFC65D"></a-cylinder>
      <a-plane rotation="-90 0 0" width="4" height="4" color="#7BC8A4"></a-plane>

      <a-sky color="#ECECEC"></a-sky>
      <a-entity position="0 0 3.8">
        <a-camera></a-camera>
      </a-entity>
    </a-scene>
  </body>
</html>
{% endhighlight %}

Aframe creates an `<a-scene>` in the body of the html page. Inside the `<a-scene>` there are four 3D entities: a sphere, a box, a cylinder, and a plane. (There is also a color for the sky and a positioning of the 3D camera. But for the Argon version, we don't need sky because Argon will use the device's own videocamera to provide the physical world as the background. Also, we don't need to specify the 3D camera for this example.) 

For the Argon version, we just group the 3D entities under another `<a-entity>` with the id "helloworld" and a position. Then we replace the `<a-scene>` tag with the `<ar-scene>` tag. 
    
Here is the code:

{% highlight html %}
<html>
  <head>
    <title>Hello, World! Argon + A-Frame</title>
    <meta name="description" content="Hello, World! Argon + A-Frame">
    <script src="../resources/js/aframe.min.js"></script>
    <script src="../resources/js/argon.min.js"></script>
   <script src="../build.js"></script>
  </head>
  <body>
    <body>
    <ar-scene>
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

In addition, you see in the `<head>` that we need two additional scripts for the argon javascript.To view this example, you need the Argon browser running on iOS device. If you view it in a regular browser, you will simply see a white background, because the background videoreality can only be provided by Argon. 