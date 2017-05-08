---
layout: page
title: 'Part 7: Using Vuforia in Twine'
---

> This lesson uses the third [example](https://github.com/blairmacintyre/oldfashioned/tree/master/examples/) from GitHub. <br> Import the text file into Twine to open the project.


## Adding the Vuforia Macros
In this tutorial you will learn how to utilize your Vuforia database within Twine to make AR experiences that can precisely track where images and objects are relative to the camera. We will begin by creating a new Twine project and adding the standard "passage-cleanup" code as well as the `append3d` and `replace3d` macros discussed in [part 3]({{ site.baseurl }}/_twinet/part3) of this tutorial.

There are three essential macros you will need to add to use Vuforia targets. The first two, `initVuforia` and `vuforiaDataset`, are used to initialize Vuforia using your encrypted license key and any Vuforia target datasets you will be using. The `initVuforia` macro will need one parameter, the url of the text file containing the encrypted Vuforia key. Argon will use this file to initialize Vuforia.

We call the collection of targets in a Vuforia database a **dataset**. Our second important macro, `vuforiaDataset`, will retrieve a dataset using the xml file that was automatically generated when we downloaded our Vuforia database in [part 6]({{ site.baseurl }}/_twinet/part6), granting us access to any target in that database. The macro will take in two parameters: a `datasetID`, which will act as a name for our dataset, and a `datasetURL`, which is the URL of the xml file associated with the database we want to use. The macros will look like this:

```javascript

/* <<initVuforia keyFileURL>> */
Macro.add(["initVuforia"], {
    handler () {
        if (this.args.length < 1) {
                return this.error('parameter missing: key file url');
        }

        var keyElem = document.createElement('a-asset-item');
        var $keyElem = jQuery(keyElem);
        $keyElem.attr({
           "id" : "vuforiakey",
         "src" : this.args[0]
        });

        keyElem.addEventListener('loaded', function(evt) {
            $('#argon-aframe').attr("vuforiakey", "#vuforiakey");
        });
    $('#argon-aframe').prepend($keyElem);
    }
});

/* <<vuforiaDataset datasetID datasetURL>> */
Macro.add(["vuforiaDataset"], {
    handler () {
        if (this.args.length < 2) {
                return this.error('parameters are {id, dataset url}');
        }
        console.log("dataset: " + this.args[1]);
        $('#argon-aframe').attr("vuforiadataset__" + this.args[0], "src:url(" + this.args[1] + ");");
    }
});


```

The final macro you will need is `createReferenceFrameEntity`. This macro will create an entity that relies on a specified frame of reference. We will use this macro in conjunction with the `append3d` macro to create an object that uses a specified frame of reference for positioning. `createReferenceFrameEntity` will take in three parameters: an `entityID`, which will be used to refer to this entity, a string that will determine whether the entity is a story or passage entity, and a `"parent frame"` which the entity will use as a point of reference. Add the code below and read through the comments.

```javascript

// <<createReferenceFrameEntity entityID story|passage "parent frame" * >>
Macro.add(['createReferenceFrameEntity'], {
    handler() {
        if (this.args.length < 3) {
            return this.error('need selector, name and parent frame name');
        }

        var targetId = this.args[0];

        /* Determines whether this is a story or passage entity */
        var $container;
        if (this.args[1] === "story") {
            $container = $("#story-entities");
        } else if (this.args[1] === "passage") {
            $container = $("#passage-entities");
        } else {
            return this.error('3D content type must be "story" or "passage": "' + this.args[1] + '" invalid');
        }

        /* If an entity with the same id has already been added, an error is thrown */
        var $targets = $container.find("#" + targetId);
        if ($targets.length > 0) {
            return this.error('passage "' + targetId + '" already exists.');
        }

      /* Adds the entity to the appropriate entity container (story or passage) */
        $targets = jQuery(document.createElement('ar-frame'));
        $targets.attr({
            "id": targetId,
            "parent": this.args[2]
        });

        for (var i = 3; i<this.args.length; i++) {
            setAttrFromArg($targets, this.args[i]);
        }

        $container.append($targets);
    }
});

```

With these three macros, we can now move onto the passages component.

## Making Entities that Rely on Specified Reference Frames
We will begin by naming the automatically generated passage `Start` and then creating a new `StoryInit` passage. In this passage we will need to set up Vuforia and the dataset that you intend to use for the AR experience. To do this you must use the `initVuforia` and `vuforiaDataset` macros that you defined in the JavaScript component. The code should look something like this:

```

<<initVuforia "http://pathToKey/key.txt">>
<<vuforiaDataset myDataset "http://pathToDataset/dataset.xml">>

```

With Vuforia and our dataset initialized, we can create an entity that uses one of our dataset's targets as a frame of reference. To do that, we use the `createReferenceFrameEntity` followed by the name of the entity we want to add, the type of entity we want it to be (story or passage), and the parent entity that we want to use as a frame of reference. For this example, we want to use a target that we added to our Vuforia database as the parent entity.

```

<<createReferenceFrameEntity boxOnTarget story vuforia.myDataset.target trackvisibility=true visible=false>>

<<append3d boxOnTarget story>>
<a-box position="0 0 0.025" width="0.05" depth="0.05" height="0.05" color="yellow" ></a-box>
<</append3d>>

```

This segment of code will create a 3D box called `boxOnTarget` that will remain hidden until the user points their camera towards a picture of the target inside `myDataset` called `target`. Because we made `boxOnTarget` a story entity, anytime the camera points to this picture, our `boxOnTarget` object will become visible and be positioned using the `target` as a frame of reference.

It is also important to note that we can use the user's camera (which we just refer to as the "user") as a frame of reference for entities. In fact, the user *is* the default frame of reference. Go to the Start passage and add the following code:

```

Any entity can act as a parent (frame of reference) for another Argon entity, a Vuforia target, a normal 3D object that we append to the screen, or even the user.

<<createReferenceFrameEntity sphere1 passage ar.user userotation=false>>

<<append3d sphere1>>
<a-sphere position="0, .5, 0" radius="1.25" color="darkgreen" ></a-sphere>
<</append3d>>

```

> **NOTE:** the most important concept to grasp from this lesson is that any Argon entity with *known* position can act as a frame of reference. However, Vuforia gives you the added ability of using custom images and 3D objects as frames of reference with high precision using computer vision.

You should spend some time practicing using reference frames and Vuforia targets as they are some of the most powerful tools that Argon has to offer and will greatly extend the power and flexibility of your augmented reality experiences!