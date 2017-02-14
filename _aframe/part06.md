---
layout: page
title: 'Lesson 6: Adding video and audio'
---
> Download [Argon4](http://argonjs.io/argon-app) and the [Tutorial Source Code](https://github.com/argonjs/design-aids/tree/gh-pages/code). <br> This tutorial uses the *video* and *resources* directories.<br> **[Demo in Argon4](https://github.com/argonjs/design-aids/tree/gh-pages/code/video/)**


A-Frame itself has a [video primitive](https://aframe.io/docs/0.3.0/primitives/a-video.html) that you can use to add video to a scene. To use it, you load the video as an asset and then position the video primitive into the scene. This same tag will work in Argon-aframe. It will play a video on a plane positioned in space. 

Try this in Argon:
{% highlight html %}
<ar-scene>
  <a-assets>
    <video id="myvideo" autoplay loop="true" src="xxx.mp4">
  </a-assets>
  <!-- Using the asset management system. -->
  <a-video src="#myvideo" width="16" height="9" position="0 0 -20"></a-video>
</ar-scene>
{% endhighlight %}

For audio, A-Frame has a sound component that you can attach to entities. See the [aframe documentation](https://aframe.io/docs/0.3.0/components/sound.html). This component should work on Argon-aframe just as it does in A-Frame. 

If these entities and components don't give you the capabilities that you need, you can also create your own component (see lesson 12) that can use the HTML audio and video tags to have more control over the presentation and interaction with the media. 

There are limitations to playing a video on iOS devices. See how A-Frame handles those limitations [here](https://aframe.io/docs/0.4.0/primitives/a-video.html).
