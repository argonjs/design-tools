---
layout: page
title: 'Lesson 5: Adding an Eventlistener'
---
> Download [Argon4](http://argonjs.io/argon-app) and the [Tutorial Source Code](https://github.com/argonjs/design-aids/tree/gh-pages/code). <br> This tutorial uses the *event* and *resources* directories.<br> **[Demo in Argon4](https://github.com/argonjs/design-aids/tree/gh-pages/code/event/)**


In lesson 4, we saw an example of an eventListener added to a component. Here in Lesson 5, we describe eventListeners in more detail. 

eventListeners go far beyond A-Frame. In conventional web programming, you can add eventListeners to handle many different kinds of events from objects and actions in the DOM. For example, you can listen for an event when the HTML file has been fully loaded; or an event when the user clicks on a button; or when the user releases the mouse button; and so on. In Javascript, this is the structure:

{% highlight html %}
element.addEventListener(event, function);
{% endhighlight %}

addEventListener adds the event to some element in the DOM that you specify, such as a button or an image. The event name is one of a long list known to the DOM system: "click", "mouseup", "mousedown", and so on. In this case, "function" is the name of the function that is called when that event occurs. This is explained in more detail in the [W3 documentation](http://www.w3schools.com/js/js_htmldom_eventlistener.asp)

For Argon-aframe in particular, there are two ways that you can attach eventListeners to your objects: either directly to a single object or through a component (which can be used for multiple objects). 

Let's look again at the code for the sphere from Lesson 4.

{% highlight html %}

<a-sphere position="0 1.25 -1" cursor-listener radius="1.25" color="#EF2D5E" ></a-sphere>

{% endhighlight %}

cursor-listener is the component that contains the three events. The advantage of defining a component is that we can attach the same component to many objects. Each object will then respond when clicked or when the cursor passes over it. But we could also attach the event directly to the sphere itself. 

First, we would remove the component and instead give the sphere an id:

{% highlight html %}
<a-sphere id="mysphere" position="0 1.25 -1" radius="1.25" color="#EF2D5E" ></a-sphere>
{% endhighlight %}

Then in our Javascript code, we would identify the sphere object and add the event directly:

{% highlight html %}
<script>
var theSphere = document.querySelector("#mysphere"); 
theSphere.addEventListener("click",myReportingFunction); 
function myReportingFunction(){
	console.log("sphere was clicked on"); 
}
</script>
{% endhighlight %}

You could do this individually for each object and each event that you want to attach. This is sometimes useful, but, as noted, it is often better to create a component (see Lesson 12). 



