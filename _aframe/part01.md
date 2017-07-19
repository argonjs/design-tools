---
layout: page
title: 'Lesson 1: Getting Started with Argon-Aframe'
---

An Argon-aframe application consists of an html file and auxiliary files. The html file contains the tags that display the objects and the media, as we will describe in the following lessons. In addition to the tags in the `<body>` of your html file, you also need to insert script tags in the `<head>`. These script tags will refer to resources that the application needs, such as the aframe.js and argon.js code and other javascript files. In the examples, we use a folder called resources to store these code files (in a subfolder called js). There are other assets you may need for your application, such as style sheets and various media assets - jpg images, audio and video files - depending on the purpose of your application. You can organize these in folders as you prefer. Here is the bare minimum structure of your html file:

{% highlight html %}
<html>
  <head>
    <title>Hello, World! Argon + A-Frame</title>
    <meta name="description" content="Hello, World! Argon + A-Frame">
    <script src="../resources/js/aframe.js"></script>
    <script src="../resources/js/argon.min.js"></script>
    <script src="../build.js"></script>
  </head>
  <body>
	ARGON AFRAME TAGS GO HERE 
  </body> 
</html>
{% endhighlight %}

Argon-aframe works like any web application. You place your html and other resource files on your server and serve them to your users through the http protocol: 

![Lesson 1_picture1](http://argonjs.io/design-tools/public/Lesson1_picture1.png){:class="img-responsive"}

We assume that you understand how to store html files on a server and serve them. If this is not the case, you can contact a web developer/programmer to proceed.

The client is the Argon browser, which you can download from the App Store [here](https://itunes.apple.com/us/app/argon4/id1089308600?mt=8). Many of Argon's features will work in other browsers on mobile devices (including Android phones and tablets) or laptops. For example, if you want to make an experience that uses only panoramas (see [lesson 9](http://argonjs.io/design-tools/aframe/part09/)), then you would not have to use the Argon browser itself. However, at this time, only the Argon browser running on an iPhone or iPad will be able to show the live video feed of the device camera and also do image-trackings (as explained in lessons [10](http://argonjs.io/design-tools/aframe/part10/) and [11](http://argonjs.io/design-tools/aframe/part11/)).
