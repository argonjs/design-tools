---
layout: page
title: 'Part 1: Getting Started with Argon-Aframe'
---

This part will introduce the developer to the basic structure of an argon-aframe application: the html file and the needed code resources and asset files. 

Writing an argon-aframe experience means inserting the appropriate regular and custom tags into an html file.


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
  <body>
	tags go here. 
  </body> 
</html>
{% endhighlight %}

>