---
layout: page
title: 'Part 3: Writing a simple Argon-Twine experience'
---

> This lesson uses the first [example](https://github.com/blairmacintyre/oldfashioned/tree/master/examples/) from github. <br> Import the text file into Twine to open the project.


## Creating a Story in Twine
To begin creating a new Argon-Twine experience, open Twine and select the '+Story' button. You may then choose a name for your project. The name can be changed at any point later on.

After creating a new project, you will be directed to the Twine editing page. At this point, if you have not done so, you should familiarize yourself with the fundamentals of Twine by playing around with the interface or reading the [Twine wiki](http://twinery.org/wiki/) or [forum](http://twinery.org/forum/).

It is important to note that an Argon-Twine project is separated into three different components, the passages (written in the OldFashioned format), a story CSS stylesheet, and a JavaScript component.

## Writing the JavaScript Component
Let's begin by opening up the JavaScript component for editing. In any Argon-Twine project, you should begin by doing a "passage-cleanup", which removes any passage entities. For simple projects the following code will suffice.

```javascript

predisplay['#argon-passage-cleanup'] = function (task) {
    $('#passage-entities').empty();
};

```

The next important Twine topic to discuss is adding macros. Macros are commands that can be defined in the JavaScript component and then used within the passages. For this example, you will need to add two macros, `append3d` and `replace3d`, which will allow you to add and replace 3D entities. There are two types of entities: story-entities and passage-entities. Story-entities are initialized in the `StoryInit` passage, which will be discussed later in this tutorial, and remain static as you traverse through the passages. In contrast, passage-entities are instantiated in individual passages and have scopes limited to their respective passage. One last note, the `append3d` and `replace3d` macros will take in two arguments. The first argument will define whether you are dealing with story-entities or passage-entities and the following argument will define the entities you are adding or replacing. Now, read through this code snippet to get a better understanding of how to implement the `append3d` and `replace3d` macros. Then add the following code below the "passage-cleanup".

```javascript

Macro.add(['append3d', 'replace3d'], {
        tags : null,


        handler() {

            /* A 3D entity must be provided as an argument */
            if (this.args.length === 0) {
                return this.error('no selector specified');
            }

            /* The 'targetId' variable holds the 3D entity you are adding. The '$container' variable will be assigned 'passage-entities' if the first argument is 'passage' or 'story-entities' if the first argument is 'story'.  */
            var targetId;
            var $container;
            if (this.args.length === 1) {
                targetId = this.args[0];
                //default to passage for the type
                $container = $("#passage-entities");
            } else {
                if (this.args[0] === "story") {
                    $container = $("#story-entities");
                } else if (this.args[0] === "passage") {
                    $container = $("#passage-entities");
                } else {
                    return this.error('3D content type must be "story" or "passage": "' + this.args[0] + '" invalid');
                }
                targetId = this.args[1];
            }

            /* The container may already hold the target that was passed in as an argument. If it does, '$targets' will be assigned that value and this macro's function will change from adding a new 3d entity to replacing an old 3d entity. */
            var $targets = $container.find("#" + targetId);
            if ($targets.length === 0) {
                $targets = jQuery(document.createElement('a-entity'));
                $targets.attr("id", targetId);
                console.log("creating new 3D element: " + targetId);
            $container.append($targets);
            } else if (this.name === 'replace3d') {
                $targets.empty();
            }

            if (this.payload[0].contents !== '') {
                var frag = document.createDocumentFragment();
                new Wikifier(frag, this.payload[0].contents);
                var div = document.createElement('div');
                div.appendChild(frag);
                var text = div.innerText;

                console.log("storing content in 3D element: " + text);
                $targets.append(text);
            }
        }
});

```

## The "Start" and "StoryInit" passages
Now we move to the simpler part: the passages component. Navigate to the grid view of the project. You should see an untitled passage. Open the editor for the passage and name it `Start`. This passage will be the beginning of any AR experience you create with Twine.

**NOTE:** The first passage we create must be the `Start` passage.

But before we begin editing this passage, let's create a new passage and name it `StoryInit`. `StoryInit` is a special passage that is used to make any preparations that must be done before beginning the AR experience. Among other actions, it can be used to initialize story entities. In the passage editor for `StoryInit`, we will add a story-entity consisting of two 3D objects, a box and a sphere. We will call this entity, quite simply, `box-and-sphere`. Add the following code to the `StoryInit` passage.

```html

<<append3d story box-and-sphere>>
<a-sphere position="0 1.25 -10" radius="1.25" color="pink" ></a-sphere><a-box id="bluebox" position="-1 0.5 -10" rotation="0 45 0" width="1" height="1" depth="1"  color="blue"></a-box>
<</append3d>>

```

Notice that the attributes of these 3D objects are readily customizable. Another important point is that attributes like `radius`, `width`, `height`, and `depth` are in units of meters.

## Adding Passage Entities
Now we can finally get into the core of the creation process. We will open up the editor for the `Start` passage again and add some basic text that will be overlayed onto the screen when we run the project. We will also add a passage-entity consisting of a simple green sphere. Add the following code to the `Start` passage.

```html

This is a simple AR scene. [[Click|second]] to go to the second scene.
<<append3d sphere1>>
<a-sphere position="1 1.25 -5" radius="1.25" color="darkgreen" ></a-sphere>
<</append3d>>

```

Note that `[[Click|second]]` will display the word "Click", which acts as a link to a passage named `second`. Because there is no current passage called `second`, one will automatically be generated.

Remember that when a user leaves the first scene and enters the second scene, the green sphere will be terminated because it is a passage-entity and we have left its scope. Now, open the editor for the `second` passage and add the following code.

```html

This is a second AR scene. This scene has more text, because we'd like to see how that lay's out. [[Click|third]] to go to the third scene, or click [[here|Start]] to return to the first scene.
<<append3d passage sphere2>>
<a-sphere position="-1 -1.25 -5" radius="1.25" color="orange" ></a-sphere>
<</append3d>>

```

In this final, third scene, we will use the replace3d macro to replace the 3D objects in the box-and-sphere story-entity with new 3D objects. Add this last bit of code to the `third` passage.

```html

This is a third AR scene. Click [[second|second]] to go to the second scene, or click [[here|Start]] to return to the first one.
<<append3d sphere3>>
<a-sphere position="-1 1.25 -5" radius="1.25" color="orange" ></a-sphere>
<</append3d>><<replace3d story box-and-sphere>>
<a-sphere position="0 -1.25 -10" radius="1.25" color="#EF2D5E" ></a-sphere><a-box id="bluebox" position="-1 -2.5 -10" rotation="0 45 0" width="1" height="1" depth="1"  color="#4CC3D9"></a-box>
<</replace3d>>

```

## Exporting the Project
Now let's export and use our experience! From the Twine dashboard, click the cog icon in the upper right corner of your AR project and click the "Publish to File" button, which will create an html file that will hold your AR experience. To view this example, you need to serve it to the Argon browser running on an iOS device. If you view it in a regular browser, you will simply see a white background, because the background video reality can only be provided by Argon.Simply find a way to store this file on the Internet, for example, through GitHub pages, and then navigate to the file using the Argon4 application.

Congratulations, you now have the tools to create simple AR experiences with Twine! Next, we will take a look at CSS styling in Twine.