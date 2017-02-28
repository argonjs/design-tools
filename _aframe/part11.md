---
layout: page
title: 'Lesson 11: Creating and using your own image database'
---
> Download [Argon4](http://argonjs.io/argon-app) and the [Tutorial Source Code](https://github.com/argonjs/design-aids/tree/gh-pages/code). <br> This tutorial uses the *vuforia2* and *resources* directories.<br> **[Demo in Argon4](https://github.com/argonjs/design-aids/tree/gh-pages/code/vuforia2/)**

## Vision-based Tracking and Vuforia
The Argon browser includes a computer-vision tracking system called [Vuforia](http://www.vuforia.com). Vuforia is a platform-native SDK that can find and precisely track where images and objects are relative to the camera. argon.js can represent these tracked *targets* as frames of reference expressed relative to the camera on the device (which is what we also use as the location of the user).  This means that anything tracked by Vuforia can have its position computed relative to any other frame of reference Argon knows about, and attaching content to objects tracked by Vuforia is done in exactly the same way that content was attached to the world in the first parts of this tutorial.

To use Vuforia with Argon, you must create an account on the [Vuforia Developer Portal](https://developer.vuforia.com) and use the tools there to get a license key and create target datasets. (Currently, argon.js does not support all of the features of the Vuforia Native SDK, such as cloud recognition and VuMarks, but we hope to soon.)

In the Vuforia Portal's *License Manager*, you should obtain a copy of your license key.  It will look something like this:
<pre>
AYVDMl7/////AAAAGUNYbWe+HkCjrn65cBM7Lm0Z6OHGozSF6sPHjCvjp3LhFIlirezFjpIqp0Xtg0ObkDmyTdJj1Yqb8VB9zeFu29cUBWe1fEBAHT//B74Urf2vcDCjyk7l92MUcwCq1xMRruzTVyXkIiQO8XrPTfjGA0KCCJjeBMj9HLvsH+POXBuKPOpnAEkptjZ/qNa4lEpSmZnr43Vg8wJZsQtzFBL8KDT8RGxzSZbuIh800dLzWmJOOjUDlac2qmnBWia7F7QymO1ig5WXgbDGb3CoOsFAZOgUsqXqk2ycrmV9BnebjesdVWmYKazrreiH021fq4rT1EmW5zgo4jR5pfLnjlXhofobPnCsq3zJZda6N13zpabc
</pre>

In the Vuforia Portal's *Target Manager*, you should create and download a target database. 

> Please pay attention to the sizes you enter for the various targets: argon.js will use these sizes as if they are expressed in meters. 

Select the SDK option when asked, and you should receive two files with the same name, one with a `.dat` extension and one with a `.xml` extension.  

In the remainder of this part of the tutorial, you will learn how to use this key and target database to do vision-based tracking with Argon.

## The Vuforia License Data File
To use Vuforia, the native library must be initialized with a valid license key. The Argon browser requires each web app to provide this key in an encrypted format, so that programmers are not making their license key visible to others. This also means that only the users of your applications can access Vuforia functionality that is tied to your key, especially services that cost money to use. 

To create an encrypted license key file, you need to use [PGP](https://en.wikipedia.org/wiki/Pretty_Good_Privacy) to encrypt an JSON file with the Argon browser's public key (available in the public PGP key store as `secure@argonjs.io`).  To simplify the process and ensure a valid JSON file is encrypted, you should use the [Vuforia PGP Encryptor]({{ site.baseurl }}/start/vuforia-pgp-encryptor) page on this site.

The JSON file contains two things, which you enter in the first two boxes on the web page. The first box is for your Vuforia license key, which you should paste in exactly as it appears on the Vuforia web site. Do not add extra spaces or line breaks. 

> If you are using a public computer, you should empty the browser cache after using the Vuforia-PGP-encryptor page, to ensure your license key is not available after you are done.

> **IMPORTANT: You are responsible for complying with the Vuforia Terms of Service**. Vuforia requires each separate application to have its own key, and distributed applications cannot use a developer key. The free developer key cannot be used for commercial, published applications. 

In the second box, you should enter a list of domains and URL patterns specifying what URLs this license key and corresponding tracking database can be used from. The website shows you documentation on how to specify these patterns. The encrypted key used with the samples includes these patterns (among others):
<pre>
?(*.)argonjs.io/**
?(*.)argon.gatech.edu/**
?(*.)ael.gatech.edu/**
</pre>
You will notice that if you try to run the code for this example from your own computer or any website aside from those, Vuforia will not work.

The website runs entirely in the web client. No information you enter is sent out of your browser, and the JSON file and encrypted license data are generated as you type and appear in the remaining two text boxes on the web page. You do not need to do anything with the *License Data (JSON)* box; it is shown so you can see what the JSON file looks like.  

When you are done, copy the contents of the *License Data (encrypted)* box.  You will need to add that to the web application so it can be passed to Argon to initialize Vuforia for your web page.


## Making your Argon image-tracking application


## Vuforia Key

The `vuforiakey` component can be added to the `<ar-scene>` entity to specify the Vuforia 
license key, if Vuforia is needed. The property of the component is a reference to a DOM element
that is either an `<a-asset-item>` or some other DOM element.  If it's an asset item, the 
key will be stored in a separate file on the server and the path specified as a property of the 
asset item. If the element is a DOM element, the key will be stored directly in the HTML file.

{% highlight html %}
<ar-scene vuforiakey="#vuforiakey">
      <a-assets>
        <a-asset-item id="vuforiakey" src="key.txt"></a-asset-item>
      </a-assets>
</ar-scene>
{% endhighlight %}
Specifying a key causes Vuforia to be immediately initialized with that key.

### Properties

The `vuforiakey` component takes one property.

| Description                                                                                                                     | Default Value |
|------------|---------------------------------------------------------------------------------------------------------------------------------|---------------|
| The DOM element specifying the key. | A DOM element reference |


