---
layout: page
title: 'Part 5: Panoramas'
---

> This lesson uses the second [example](https://GitHub.com/blairmacintyre/oldfashioned/tree/master/examples/) from github. <br> Import the text file into Twine to open the project.


## Argon Panoramas
The default background for Argon is the view offered by the live video camera on the phone or tablet. Instead of the video, you can substitute a 360-degree panoramic image as the background. Panoramas offer a number of compelling design options. If the user cannot get to a specific location, such as a museum or historic site, the panorama can convey what the site looks like. The AR experience can play over the panorama.

To display a panoramic background, Argon needs an image in a special format called an ‘equirectangular projection.” You can make such a photo yourself using a relatively inexpensive panoramic camera such as the [Ricoh Theta S](https://theta360.com/en/about/theta/s.html). You can also take multiple images with a DLSR camera and stitch them into an equirectangular projection using a "stitcher" program such as [PTGui](https://www.ptgui.com). The resulting image should have an aspect ratio (width to height) of 2-1. 5000x2500 pixels is a good size. If the image is too large, it may fail to load. Once you have the equirectangular image as a .jpg or .png file, then you can create the panorama in Argon.

## Adding the Panorama Macros
Let's begin by creating a new Twine story and entering the JavaScript editor. Remember that the first code you must add to any AR Twine experience is the "passage-cleanup". For this experience, the same code as the previous example will suffice.

We now need to add three important macros to give our AR experience panorama functionality.

The first macro we must define is `createPanorama`.
This macro will be called in the `StoryInit` passage and be used to initialize panoramas that we may later use in our Twine passages.
It takes in three arguments, a name, a dataset url, and a string containing the latitude, longitude, and altitude, of the location of the panorama.

We will also be creating a short helper function for our `createPanorama` macro. Add the code below.

```javascript

/* A helper function for createPanorama that gets information from the arguments passed into it. */
function getComponentAttrFromArg(arg) {
    var eq = arg.indexOf("=");
    if (eq == -1) {
        return(arg);
    } else if (eq == 0 || eq == arg.length-1) {
        return "";
    } else {
        return arg.slice(0,eq) + ":" + arg.slice(eq+1) + ";";
    }
}

/* LLA stands for latitude, longitude, altitude */
Macro.add(['createPanorama'], {
    handler() {
        if (this.args.length < 3) {
                return this.error('required parameters are {name, dataset url, LLA}, plus other optional additional parameters');
        }
        console.log("new panorama '" + this.args[0] + "', url: " + this.args[1]);
        var argValue = "src:url(" + this.args[1] + ");lla:" + this.args[2] + ";";

        /* Manipulates the argument to get the necessary information. Above the 'createPanorama' macro, you can find the helper function that this loop utilizes. */
        for (var i = 3; i<this.args.length; i++) {
            argValue += getComponentAttrFromArg(this.args[i]);
        }

        /* Adds the panorama into Argon */
        $('#argon-aframe').attr("panorama__" + this.args[0], argValue);
    }
});

```

The second macro we will define is `requestPanoramaReality`, which can be used in our story passages to retrieve a panorama reality that we will need to place our panorama in. The macro will take in two arguments, the name of the panorama reality we want to create and the url of the panoramaReality.

Finally, we will add a last, simple macro called `showPanorama` that will display the panorama of our choosing. The only parameter we need is the name of the panorama.

```javascript

var panoramaRealityURL = "http://argonjs.io/argon-aframe/resources/reality/panorama/index.html"
Macro.add(['requestPanoramaReality'], {
    handler() {
        if (this.args.length < 2) {
            return this.error('required parameters are name and url');
        }
        console.log("new reality '" + this.args[0] + "', url: " + this.args[1]);
        $('#argon-aframe').attr("desiredreality", "name:'" + this.args[0] + "';src:url(" + this.args[1] + ");");
    }
});


Macro.add(['showPanorama'], {
    handler() {
        if (this.args.length < 1) {
            return this.error('parameter is panorama name');
        }
        console.log("show panorama '" + this.args[0]);
        $('#argon-aframe')[0].emit("showpanorama", { name: this.args[0] });
    }
});

```

## Incorporating Panoramas into Passages
Now, onto the fun part! Leave the JavaScript editor, open the auto-generated empty passage, and name it `Start`. Remember that the first passage must always be the `Start` passage.

We will now create our `StoryInit` passage. Click the add passage button and navigate to its editor. Let's initialize a few panoramas, keeping in mind the three arguments that `createPanorama` requires. Add the following code to the passage.

```html

<<createPanorama aquarium http://bmaci.com/a4/twine/panoramas/aqui.jpg "-84.3951 33.7634 206" initial=true>>
<<createPanorama skyline http://bmaci.com/a4/twine/panoramas/cent.jpg "-84.3931 33.7608 309">>
<<createPanorama museum http://bmaci.com/a4/twine/panoramas/high.jpg "-84.38584 33.79035 289">>
<<createPanorama park http://bmaci.com/a4/twine/panoramas/pied.jpg "-84.37427 33.78577 271">>

```

Notice that the first `createPanorama` has an extra parameter. That parameter simply lets Argon know that you plan to use that panorama first.

Now that we've initialized the panoramas, we can move on to the `Start` passage. For `Start` and subsequent passages, we will now need the other two macros we added: `requestPanoramaReality` and `showPanorama`.

Add this code to your passages:

```html

Here we see our first panorama, take a look around! Notice how the resolution of the panorama is diminished, a result of expanding the picture to a 360 degree view.

Click [[next|second]] to see how 3D objects look when placed on a panorama.

<<requestPanoramaReality "Panorama Reality" "http://bmaci.com/a4/twine/panoramaReality/index.html">>
<<showPanorama aquarium>>

```

Note that `aquarium` should be replaced with the name corresponding to the panorama image you wish to show in the scene.

## Overlaying 3D Objects onto Panoramas
With our next passage, let's try to overlay our panorama with some 3D objects. Think back to [part 3]({{ site.baseurl }}/_twinet/part3). How did we add 3D objects to a scene?

Remember, we have to first add the append3d (and optionally the replace3d) macro into the JavaScript component before we can begin placing 3D objects into our scene. Go ahead and add those in. After that's done, we can start adding 3D objects, and your second passage can look something like this:

```html
Here is our second panorama, and as you can see (you might have to look around), we have added some 3D objects to it! Click [[here|Start]] to go back to the 'Start' scene.

<<requestPanoramaReality "Panorama Reality" "http://bmaci.com/a4/twine/panoramaReality/index.html">>
<<showPanorama skyline>>

<<append3d story sphere-and-box>>
<a-sphere position="0 1.25 -5" radius="1.25" color="pink" ></a-sphere><a-box id="bluebox" position="5 0.5 -5" rotation="0 45 0" width="1" height="1" depth="1"  color="blue"></a-box>
<</append3d>>

```

Now that we have shown you the basic process for adding panoramas to your AR experiences, you should go ahead and play around, practicing what you've learned.

Feel free to implement passages for the last two panoramas!

When you are ready, continue onto the next tutorial, which will teach you how to implement Vuforia into your AR experiences and the benefits of doing so.