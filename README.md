Best Buy 3D WebGL POC 
=====================

Description
-----------

Best Buy 3D WebGL POC is a modern project of web retail application that provides the 3D display that is implemented against Best Buy website pages. The 3D display of the product lets the user to see the detail of the product in 3D dimension. The functionality provided also lets the user to interact with the product interactively. It uses [three.js](https://github.com/mrdoob/three.js/) as the WebGL framework and [Collada](https://collada.org/) file as the model.

Quick Start
-----------

### At the very basic, include these libraries in your HTML file :###
* three.min.js : Three.js library.  
* ColladaLoader.js : It is used to load the collada model.
* OrbitControls.js : It is used for mouse control.

### ThreeJSObject.js ###

This class is created to provide the abstraction for three.js object initialization. 

* This code creates the new instance/object of the ThreeJSObject.  
```javascript
var threeJSObject = new ThreeJSObject();
``` 

* Create the scene.
```javascript
this.createScene = function() {
	this.scene = new THREE.Scene();
}
```

* Create a renderer and set its size.
```javascript
this.createRenderer = function() {
	this.renderer = new THREE.WebGLRenderer({
		antialias : true
	});
	this.renderer.setSize(SCREEN_WIDTH, SCREEN_HEIGHT);
}
```  

* Create a camera, zoom it out from the model a bit, and add it to the scene.
```javascript
this.createCamera = function() {
	this.camera = new THREE.PerspectiveCamera(CAMERA_FOV, CAMERA_ASPECT, CAMERA_NEAR, CAMERA_FAR);
	this.camera.position.set(0, 0, 3);
	this.scene.add(this.camera);
}
```

  


