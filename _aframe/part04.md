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