---
layout: page
title: 'Part 6: Incorporating Vuforia in Your Twine Experience'
---


## Vision-based Tracking and Vuforia
The Argon browser includes a computer-vision tracking system called [Vuforia](http://www.vuforia.com). Vuforia is a platform-native SDK that can find and precisely track where images and objects are relative to the camera. argon.js can represent these tracked *targets* as frames of reference expressed relative to the camera on the device (which is what we also use as the location of the user).  This means that anything tracked by Vuforia can have its position computed relative to any other frame of reference Argon knows about, and attaching content to objects tracked by Vuforia is done in exactly the same way that content was attached to the world in the first parts of this tutorial.

## Obtaining a Vuforia License Key
To begin using Vuforia with your Twine story, you should have access to hosting on an online server. For more information on how to do that, click [here](http://www.webhostingsecretrevealed.net/web-hosting-beginner-guide/).

The next step is to obtain a Vuforia license key. First, you must [register](https://developer.vuforia.com) for a Vuforia developer account. After creating an account, you can generate a license key. Navigate to the "Develop" page and add a licence key (you can choose the "Development" type for this example). Your license key will look something like this:
<pre>
AYVDMl7/////AAAAGUNYbWe+HkCjrn65cBM7Lm0Z6OHGozSF6sPHjCvjp3LhFIlirezFjpIqp0Xtg0ObkDmyTdJj1Yqb8VB9zeFu29cUBWe1fEBAHT//B74Urf2vcDCjyk7l92MUcwCq1xMRruzTVyXkIiQO8XrPTfjGA0KCCJjeBMj9HLvsH+POXBuKPOpnAEkptjZ/qNa4lEpSmZnr43Vg8wJZsQtzFBL8KDT8RGxzSZbuIh800dLzWmJOOjUDlac2qmnBWia7F7QymO1ig5WXgbDGb3CoOsFAZOgUsqXqk2ycrmV9BnebjesdVWmYKazrreiH021fq4rT1EmW5zgo4jR5pfLnjlXhofobPnCsq3zJZda6N13zpabc
</pre>

**Warning:** you should not share your key with others because you are only alloted so many "recos" before you are charged. A "reco" occurs when your app recognizes an image in a cloud database.

To use Vuforia, the native library must be initialized with a valid license key. The Argon browser requires each web app to provide this key in an encrypted format, so that programmers are not making their license key visible to others. This also means that only the users of your applications can access Vuforia functionality that is tied to your key, especially services that cost money to use.

To obtain this encrypted version of your license key, navigate to the [Vuforia PGP Encryptor](http://docs.argonjs.io/start/vuforia-pgp-encryptor/) page. Paste your key in the box titled "Vuforia Key." Read the instructions below, and then type in your server address with this format: "?(*.)yourwebsitehere.com**". Copy the new encrypted key under the "License Data (encrypted)" box. The entire output is the encrypted version of the license key.

> If you are using a public computer, you should empty the browser cache after using the Vuforia-PGP-encryptor page, to ensure your license key is not available after you are done.

> **NOTE: You are responsible for complying with the Vuforia Terms of Service**. Vuforia requires each separate application to have its own key, and distributed applications cannot use a developer key. The free developer key cannot be used for commercial, published applications.

## Adding Vuforia Targets

