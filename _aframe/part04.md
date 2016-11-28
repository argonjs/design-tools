---
layout: page
title: 'Lesson 4: Adding an Eventlistener'
---

In lesson 3 we saw an example of an eventlistener added to a component.  Here in Lesson 4 we describe eventlisteners in more detail, because event listeners are very useful in a variety of places in argon-aframe code, not just for the cursor. 

Eventlisteners are an essential part of Javascript and the html DOM (basically everthing attached to the web page) system; they go beyond aframe. In conventional web programming you can add eventlisteners to handle many different kinds of events from objects and actions in the DOM. For example, you can listen for an event when the html file has been fully loaded; or an event when the user clicks on a button; or when the user releases the mouse button; and so on. In Javascript, this is the structure:

{% highlight html %}

element.addEventListener(event, function);

{% endhighlight %}

addEventListner adds the event to some element in the DOM that you specify, such as a button or an image. The event name is one of a long list of such events known to the DOM system: "click", "mousedup", "mousedown", and so on. And function is name of the function that is called when that event occurs.  This is explained in detail in the [W3 documentation](http://www.w3schools.com/js/js_htmldom_eventlistener.asp)

As we have said, eventlisteners can be used in web programming in general. For Argon-aframe in particular, there are two ways that you can attach eventlisteners to your objects: either directly to a single object or through a component (which can be used for multiple objects). 

Let's look again at the code for the sphere from Lesson 3.

{% highlight html %}

<a-sphere position="0 1.25 -1" cursor-listener radius="1.25" color="#EF2D5E" ></a-sphere>

{% endhighlight %}

cursor-listener is the component that contains the three events. The advantage of a component is that we can attach it to many objects. Each object will then respond when clicked or when the cursor passes over it. 

But we could also attach the event directly to the sphere itself. First we would remove the event listener and instead give the sphere an id:

{% highlight html %}

<a-sphere id="mysphere" position="0 1.25 -1" radius="1.25" color="#EF2D5E" ></a-sphere>

{% endhighlight %}

Then in our javascript code we would add find that object and add the event directly:


{% highlight html %}
<script>
var theSphere = document.querySelector("#mysphere"); 
theSphere.addEventListener("click",myReportingFunction); 
function myReportingFunction(){
	console.log("sphere was clicked on"); 
}
</script>
{% endhighlight %}

You could do this individually for each object and each event that you want to attach. This is sometimes useful, but it is often better to create a component (see Lesson 12). 



