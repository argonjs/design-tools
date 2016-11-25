---
layout: page
title: 'Lesson 5: Adding video and audio'
---

Show how to add video and audio

{% highlight html %}
<a-scene>
  <a-assets>
    <video id="myvideo" autoplay loop="true" src="xxx.mp4">
  </a-assets>
  <!-- Using the asset management system. -->
  <a-video src="#myvideo" width="16" height="9" position="0 0 -20"></a-video>
</a-scene>
{% endhighlight %}

can do this in ar-scene as well?