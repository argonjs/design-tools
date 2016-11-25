---
layout: page
title: 'Lesson 10: Image-tracking'
---

Uses the Vuforia Stones database to place the bronze head or other simple object. 

## Vuforia Key

The `vuforiakey` component can be added to the `<ar-scene>` entity to specify the Vuforia 
license key, if vuforia is needed.  The property of the component is a reference to a DOM element
that is either a `<a-asset-item>` or some other DOM element.  If it's an asset item, the 
key will be stored in a separate file on the server and the path specified as a property of the 
asset item.  The element is a DOM element, the key will be stored directly in the HTML file.

```html
<ar-scene vuforiakey="#vuforiakey">
      <a-assets>
        <a-asset-item id="vuforiakey" src="key.txt"></a-asset-item>
      </a-assets>
</ar-scene>
```
Specifying a key causes vuforia to be immediately initialized with that key.

### Properties

The `vuforiakey` component takes one property.

| Description                                                                                                                     | Default Value |
|------------|---------------------------------------------------------------------------------------------------------------------------------|---------------|
| The DOM element specifying the key. | A DOM element reference |

