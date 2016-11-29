---
layout: page
title: 'Lesson 5: Adding video and audio'
---

Aframe itself has a video tag that you can use to add video or audio to a scene. 

{% highlight html %}
<a-scene>
  <a-assets>
    <video id="myvideo" autoplay loop="true" src="xxx.mp4">
  </a-assets>
  <!-- Using the asset management system. -->
  <a-video src="#myvideo" width="16" height="9" position="0 0 -20"></a-video>
</a-scene>
{% endhighlight %}

This same tag will work in argon-aframe. It will play a video on a plane positioned in space. 

You can also create your own component that can use the html audio and video tags to have more control over the presentation and interaction with the media. 