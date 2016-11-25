---
layout: page
title: 'Lesson 8: Triggers'
---

A common need in AR and VR is to know when the viewer is within a certain distance of some location in the world. The `trigger` component can be attached to an entity, and when the camera is within a certain distance (specified by the `radius` attribute) the component will emit an event (specified by the `event` attribute).

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

Multiple triggers can be attached to an entity.  If `trigger__name` is attached, the event emitted will name `name` in the event detail `name` property.

### Properties

| Property | Description                                                                                                                     | Default Value |
|-----------|----------------------------------------------------------------------------------------------------------------------|---------------|
|raduis|The distance of the trigger point from the entity to the camera. | 1 |
|event| The name of the event to emit.| "trigger" |

### Events

When a trigger is fired, it will emit the following event.

| Name         | Description                         |
|--------------|-------------------------------------|
| `eventname`  | A trigger event containing event detail {name: string, inside: boolean, distanceSquared: number} | 

