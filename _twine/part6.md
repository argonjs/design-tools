---
layout: page
title: 'Part 6: Creating an Image Database for Twine Experiences'
---


## Vision-based Tracking and Vuforia
The Argon browser includes a computer-vision tracking system called [Vuforia](http://www.vuforia.com). Vuforia is a platform-native SDK that can find and precisely track where images and objects are relative to the camera. argon.js can represent these tracked *targets* as frames of reference expressed relative to the camera on the device (which is what we also use as the location of the user).  This means that anything tracked by Vuforia can have its position computed relative to any other frame of reference Argon knows about, and attaching content to objects tracked by Vuforia is done in exactly the same way that content was attached to the world in the first parts of this tutorial.

## Obtaining a Vuforia License Key
To begin using Vuforia with your Twine story, you will need to obtain a Vuforia license key. First, you must [register](https://developer.vuforia.com) for a Vuforia developer account. After creating an account, you can generate a license key. Navigate to the "Develop" page and add a licencse key (you can choose the "Development" type for this example). Your license key will look something like this:
<pre>
AYVDMl7/////AAAAGUNYbWe+HkCjrn65cBM7Lm0Z6OHGozSF6sPHjCvjp3LhFIlirezFjpIqp0Xtg0ObkDmyTdJj1Yqb8VB9zeFu29cUBWe1fEBAHT//B74Urf2vcDCjyk7l92MUcwCq1xMRruzTVyXkIiQO8XrPTfjGA0KCCJjeBMj9HLvsH+POXBuKPOpnAEkptjZ/qNa4lEpSmZnr43Vg8wJZsQtzFBL8KDT8RGxzSZbuIh800dLzWmJOOjUDlac2qmnBWia7F7QymO1ig5WXgbDGb3CoOsFAZOgUsqXqk2ycrmV9BnebjesdVWmYKazrreiH021fq4rT1EmW5zgo4jR5pfLnjlXhofobPnCsq3zJZda6N13zpabc
</pre>

> **Warning:** you should not share your key with others because you are only allotted so many "recos" before you are charged. A "reco" occurs when your app recognizes an image in a cloud database.

To use Vuforia, the native library must be initialized with a valid license key. The Argon browser requires each web app to provide this key in an encrypted format, so that programmers are not making their license key visible to others. This also means that only the users of your applications can access Vuforia functionality that is tied to your key, especially services that cost money to use.

To obtain this encrypted version of your license key, navigate to the [Vuforia PGP Encryptor]({{ site.baseurl }}/start/vuforia-pgp-encryptor) page. The first box is for your Vuforia license key, which you should paste in exactly as it appears on the Vuforia website without adding any extra spaces or line breaks.

In the second box, you should enter a list of domains and URL patterns specifying what URLs this license key and corresponding tracking database can be used from. Make sure to read the instructions thoroughly because the domains you enter must be correctly formatted. Now enter the URL patterns into the first box below "Allowed Origins". It should look something like this:

```
?(*.)example.com/**, www.myothersite.com/demo/**

```

Copy the new encrypted key from the "License Data (encrypted)" box. The entire output is the encrypted version of the license key. Store this key in a text file.

> If you are using a public computer, you should empty the browser cache after using the Vuforia-PGP-encryptor page, to ensure your license key is not available after you are done.

> **NOTE: You are responsible for complying with the Vuforia Terms of Service**. Vuforia requires each separate application to have its own key, and distributed applications cannot use a developer key. The free developer key cannot be used for commercial, published applications.

## Adding Vuforia Targets

With your new Vuforia key, you are now ready to create a Vuforia database and add targets to that database. Navigate to the Vuforia Target Manager page and add a database. After the database has been created, you can begin adding targets, which can be 2D images or 3D objects. For the sake of simplicity, we will be using 2D images as our targets for this example, which you can download from [here](#). Alternatively, you can use your own jpg or png images.

> When adding targets, pay attention to the sizes you enter, as argonjs will use these sizes as if they are expressed in meters.

After adding your target(s), download the database, selecting whichever SDK option you prefer. You should receive two files with the name of the database, one with a `.dat` extension and the other with a `.xml` extension.

When creating AR experiences that utilize this database, make sure to keep the `xml` and `dat` files in the same directory. In the next lesson we will teach you how to incorporate your new image database into your Twine AR experiences.