---
layout: page
title: 'Lesson 13: Loading 3D models'
---
> Download [Argon4](http://argonjs.io/argon-app) and the [Tutorial Source Code](https://github.com/argonjs/design-aids/tree/gh-pages/code).



AR-Frame loads 3D models and materials by importing .OBJ, .MTL and Collada (.DAE) files.

#Method 1
The `obj-model` component loads a 3D model and material using a [Wavefront](https://en.wikipedia.org/wiki/Wavefront) (.OBJ) file and a .MTL file. We can load an .OBJ model by pointing to assets that specify the path to an .OBJ and .MTL file:

```
<ar-scene>
  <a-assets>
    <a-asset-item id="tree-obj" src="/path/to/tree.obj"></a-asset-item>
    <a-asset-item id="tree-mtl" src="/path/to/tree.mtl"></a-asset-item>
  </a-assets>
  <a-entity obj-model="obj: #tree-obj; mtl: #tree-mtl"></a-entity>
</ar-scene>
```

#Method 2
The `collada-model` component loads a 3D model using a COLLADA (.DAE) file:

```
<ar-scene>
  <a-assets>
    <a-asset-item id="tree" src="/path/to/tree.dae"></a-asset-item>
  </a-assets>
  <a-entity collada-model="#tree"></a-entity>
</ar-scene>
```

We can also load assets of an OBJ or Collada model by specifying the path directly within url(). Note that this is less performant than going through the asset management system.

```
<a-entity obj-model="obj: url(/path/to/tree.obj); mtl: url(/path/to/tree.mtl)"></a-entity>
<a-entity collada-model="url(/path/to/tree.dae)"></a-entity>
```

##Troubleshooting:
If you don’t see your model, try scaling it down. OBJ model vertices commonly have large unit scales in comparison to A-Frame, which uses a unit scale of meters.
If you don’t see textures on your model, try placing all .jpg images in the same directory. When an OBJ model uses multiple materials (.jpg images), make sure it defines object groups for the sub-objects that use each of those materials, so that Three.js' OBJLoader can associate the materials correctly. 
A-Frame’s loader component is not perfect, and you may find it difficult to load OBJ files; Collada files are often easier to work with.

##Additional resources:
You can find and download models on the web to drop into our scenes:
* [Sketchup’s 3D Warehouse](https://3dwarehouse.sketchup.com/) - Repository of models.
* [Clara.io](https://3dwarehouse.sketchup.com/) - Repository of models.
* [Blender](https://www.blender.org/) - A free open-source 3D modeling program with plenty of existing learning resources to create models.
