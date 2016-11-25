---
layout: page
title: 'Lesson 6: Geolocation'
---

Determining the user's location and placing a object in a geolocation near the user.


The `<ar-geopose>` primitive creates an entity with a `referenceframe` component that 
defines the position and/or rotation of the entity by an LLA (longitude, lattitude, altitude).  
The `userotation` and `useposition` properties can be set to true (the default) to have
this entity set it's rotation and/or position from the referenceframe.  Often, the position
is used but the rotation may be left to be specified in the local coordinates.


{% highlight html %}
<ar-scene>
    <ar-geopose id="GT" lla=" -84.398881 33.778463" userotation="false"> 
        <a-entity billboard fixedsize="20">
        <a-plane rotation="0 90 0" width="2.9" height="4" src="#buzzpin" transparent="true"></a-plane>
        <a-entity css-object="div: #mydiv" scale="0.02 0.02 0.02" position="0 4 0"></a-entity>
        </a-entity>
    </ar-geopose>
</ar-scene>
{% endhighlight %}
