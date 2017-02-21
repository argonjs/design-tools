---
layout: page
title: 'Lesson 8: Triggers'
---
> Download [Argon4](http://argonjs.io/argon-app) and the [Tutorial Source Code](https://github.com/argonjs/design-aids/tree/gh-pages/code). <br> This tutorial uses the *trigger* and *resources* directories.<br> **[Demo in Argon4](https://github.com/argonjs/design-aids/tree/gh-pages/code/trigger/)**

A common need in AR and VR is to know when the viewer is within a certain distance of some location in the world. The `trigger` component can be attached to an entity, and when the camera is within a certain distance (specified by the `radius` attribute), the component will emit an event (specified by the `event` attribute).

{% highlight html %}
    <ar-scene>
      <ar-geopose id="GT" lla=" -84.398881 33.778463" userotation="false" trigger="radius:100;event:nearGT"> 
         <a-entity billboard fixedsize="20">
           <a-plane rotation="0 90 0" width="2.9" height="4" src="#buzzpin" transparent="true"></a-plane>
           <a-entity css-object="div: #mydiv" scale="0.02 0.02 0.02" position="0 4 0"></a-entity>
        </a-entity>
      </ar-geopose>
    </ar-scene>
{% endhighlight %}

In this example, when the user (camera) is within 100 meters of the specified LLA, the event will be emitted.  Similarly, when the user (camera) moves further than 100 meters away, the event will be emitted again.  The event detail can be used to decide if it was an enter or exit event.

So, in general, the `radius` property is the distance from the entity to the camera in meters. The `event` property gives the name of the event. (The default name is "trigger".) When the trigger is fired, it will emit an event with that name. The trigger event will have the following details: name: string, inside: boolean, distanceSquared: number.

Multiple triggers can be attached to an entity.  If `trigger__name` is attached, the event emitted will have `name` in the event detail `name` property.

