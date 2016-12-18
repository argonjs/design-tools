---
layout: page
title: 'Lesson 7: Geolocation'
---
> Download [Argon4](http://argonjs.io/argon-app) and the [Tutorial Source Code](https://github.com/argonjs/design-aids/tree/gh-pages/code). <br> This tutorial uses the *geolocation* and *resources* directories.<br> **[Demo in Argon4](https://github.com/argonjs/design-aids/tree/gh-pages/code/geolocation/)**


Key features of Augmented Reality include 1. the ability of associating data objects with places in the world and 2. displaying those objects at those places. 

The `<ar-geopose>` primitive is argon-aframe's way of locating objects in physical space (of the planet). The `<ar-geopose>` primitive creates an entity with a `referenceframe` component. This component defines the position and/or rotation of the entity by an LLA (longitude, latitude, altitude). So you can locate your object anywhere on the earth relatively accurately by using this tag. 

You can find the longitude and latitude through google maps or through a variety of apps on a smart phone. Some apps will also give your the altitude of a location. 

{% highlight html %}
<ar-scene>
    <ar-geopose id="GT" lla=" -84.398881 33.778463"> 
    </ar-geopose>
</ar-scene>
{% endhighlight %}

`geopose` here defines a place. It has an id of GT for "Georgia Tech" and its position is the Georgia Tech campus. The longitude is -84.398881, because GT is almost 90 degrees west of Greenwich, England, which is the 0 origin for longitude. Its latitude is 33.778463 degrees north of the equator. No altitude is omitted. If given, it should be in meters. Atlanta is relatively high up for a major city, so GT's altitude would be about 300 (meters). 

The `userotation` and `useposition` properties can be set to true (the default) to have this entity set its rotation and/or position from the referenceframe.  Often, the position is used but the rotation may be left to be specified in the local coordinates. So you might want to set rotation to false. 

So far we have a geoposition as an entity, but it is empty. If we nest objects inside the geopose entity, all those objects inherit the geopose's location. So we can put a sphere at this location on the GT campus: 

{% highlight html %}
<ar-scene>
    <ar-geopose id="GT" lla=" -84.398881 33.778463" userotation="false"> 
 	<a-sphere position="0 2 -1" radius="1.25" color="#EF2D5E"></a-sphere>
    </ar-geopose>
</ar-scene>
{% endhighlight %}

This creates a sphere of a radius of 1.25 meters and the indicated RGB color. What is the position of the sphere? Remember that aframe assumes a reference frame x-y-z, where x is right and left, y is up and down, and z is toward or away from the user. The position of the sphere is at the origin in terms of left and right, two meter up, and one meter away from 0 in the z direction (which is into the screen). What would the position "0 0 0" mean? That origin is sited at the longitude and latitude specified in the `geopose`. The sphere inherits the `geopose` location as the origin of its frame of reference.  

So if we wanted to make a "poster" and set it in space at this location, we could write the following:

{% highlight html %}
<body>
<div id="mydiv"> Welcome to Georgia Tech! </div>
<ar-scene>
    <ar-geopose id="GT" lla=" -84.398881 33.778463" userotation="false"> 
        <a-entity billboard>
        <a-entity css-object="div: #mydiv" scale="0.02 0.02 0.02" position="0 0 0"></a-entity>
        </a-entity>
    </ar-geopose>
</ar-scene>
</body>

{% endhighlight %}

In Lesson 2a we saw how to turn html divs into CSSObjects.  This is what we do here. The div whose id is "mydiv" is converted to a CSSObject, scaled and positioned at the origin (0 0 0) of the geopose entity GT. The billboard entity wrapped around mydiv makes sure that the this entity and everything nested inside will always turn to face the camera (so the user can read it). That effect is called "billboarding." 