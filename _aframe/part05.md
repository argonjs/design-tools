---
layout: page
title: 'Lesson 5: Adding video and audio'
---

Aframe itself has a [video primtiive}(https://aframe.io/docs/0.3.0/primitives/a-video.html) that you can use to add video to a scene. To use it you load the video as an asset and then position the video primitive itself into the scene. This same tag will work in argon-aframe. It will play a video on a plane positioned in space. 

TRY THIS in argon
{% highlight html %}
<ar-scene>
  <a-assets>
    <video id="myvideo" autoplay loop="true" src="xxx.mp4">
  </a-assets>
  <!-- Using the asset management system. -->
  <a-video src="#myvideo" width="16" height="9" position="0 0 -20"></a-video>
</ar-scene>
{% endhighlight %}



For audio, aframe has a sound component that you can attach to entities. See the [aframe documentation](https://aframe.io/docs/0.3.0/components/sound.html). This component should work on argon-aframe just as it does in aframe. 

If these entities and components don't give you the capabilities that you need, you can also create your own component that can use the html audio and video tags to have more control over the presentation and interaction with the media. 
