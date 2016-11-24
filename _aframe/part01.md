---
layout: page
title: 'Lesson 1: Getting Started with Argon-Aframe'
---

An Argon-aframe application consists of an html file and auxiliary files. The html file contains the tags that display the objects and the media, as we will describe in the following lessons. In addition to the tags in the `<body>` of your html file, you also need to insert script tags in the `<head>`. These script tags will refer to resources that you need, such as the aframe.js and argon.js code and other javascript files. 




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
	ARGON AFRAME TAGS GO HERE 
  </body> 
</html>
{% endhighlight %}

>