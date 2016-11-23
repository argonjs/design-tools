---
title: Panoramic Narratives for Argon
layout: page
---
This is a drag-and-drop web interface to generate panoramic narratives with 360-degree panoramic images and optional audio. No programming is required. 

By "panoramic narratives", we mean a combination of 360 panoramic images, each with its own (optional) audio. A row of buttons appears centered at the bottom of the screen, which permits the user to choose in what order to visit the panos. You can use this structure to create a tour of rooms in a building, a college campus, a city neighborhood, historic site, etc. You could also create a fictional narrative with audio that tells a story in several locations. There are many possible practical and creative applications for this simple combination of word and image.

Here is a simple example: a tour of four tourist locations in Atlanta, GA:...

These narratives should work in any standard browser (such Safari or Chrome) on a desktop or laptop, on an iOS or Android device. They will work best in the Argon4 browser running in Safari on an iOS device or in Chrome running on an Android device. 

In order to use the panoramic narrative, you first must create the panoramas and record the audio. There are a number of cameras and editing tools to make panoramic images [such the Ricoh Theta S]. The panoramas must be in a particular format: an equirectangular projection with an aspect ratio of 2 to 1 (width to height). While the application should handle images of varying sizes, a good limit would be 5000 by 2500 or 6000 by 3000, especially if you are going to create a narrative with more than 5 panoramas. The audio should be in mp3 format. 

Once you have your image and audio assets in appropriate files, you go to the web site: http://panorama.lmc.gatech.edu:8000

![The panomaker start screen]({{ site.baseurl }}/public/pano1.png)

Fill in the fields (name and email are optional). 

Once you fill in the field indicating the number of panos, the page will expand to give you dialogue boxes for each of the pano and audio combinations:

![Filling out the screen]({{ site.baseurl }}/public/pano2.png)

Fill in the file names, or drag and drop the files. You can also add the latitude, longitude, and altitude of the panos, if you know that information. It isn't used in the current implementation, but the information will be added to the code (in case you want to modify the code, as described below)

When you press create, the system will upload and process your files. You will get a final screen that gives you a link to our server. If you click this link in the browser or in Argon4, you will get your experience. You can use our server link for testing. However, please be aware that we will clean out our directories from time to time. If you want to keep your resulting experience, you should download files and store them on your own server. 

You can do this by clicking on the download button. You will receive a zipped file contining a folder. Upzip and please this folder on your server. You can also open the files and modify or add to the code to create a more elaborate experience (e..g to change the buttons, add 3D graphics). TO do this, you will probably need to look at the documentation for [Argon](http://argonjs.io).