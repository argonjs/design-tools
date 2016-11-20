---
layout: page
title: 'Part 1: Getting Started with Argon-Aframe'
---

> Download [Argon4](http://argonjs.io/argon-app) and the [Tutorial Source Code](https://github.com/argonjs/docs/tree/gh-pages/code). <br> This tutorial uses the *1-geopose* and *resources* directories.<br> **[Live Demo](/code/1-geopose)**

In general, *argon.js* apps can be structured however you want. This tutorial
follows a [single-page app](https://en.wikipedia.org/wiki/Single-page_application)
structure, in which the entire app loads from one html page.

{% highlight html %}
<html>
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0" />
  <head>
    <title>My Awesome argon.js App</title>
    <script src="../resources/lib/three/three.min.js"></script>
    <script src="../resources/lib/argon.min.js"></script>
  </head>
  <body>
    <div id="argon"></div>
    <script src="./app.js"></script>   
  </body> 
</html>
{% endhighlight %}

>