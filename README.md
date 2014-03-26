Best Buy 3D WebGL POC 
=====================

Description
-----------

Best Buy 3D WebGL POC is a modern project of web retail application that provides the 3D display that is implemented against Best Buy website pages. The 3D display of the product lets the user to see the detail of the product in 3D dimension. The functionality provided also lets the user to interact with the product interactively. It uses [three.js](https://github.com/mrdoob/three.js/) as the WebGL framework and [Collada](https://collada.org/) file as the model asset.

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
##### 1. Set up for the scene, renderer, camera, light, and directional light.

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

* Create a light, set its position, and add it to the scene.
```javascript
this.createCamera = function() {
	this.camera = new THREE.PerspectiveCamera(CAMERA_FOV, CAMERA_ASPECT, CAMERA_NEAR, CAMERA_FAR);
	this.camera.position.set(0, 0, 3);
	this.scene.add(this.camera);
}
```
  
* Create a directional light, set its position, and add it to the scene.
```javascript
this.createDirectionalLight = function() {
	var directionalLight = new THREE.DirectionalLight(0xeeeeee);
	....
	this.scene.add(directionalLight);
}
```

* Set up for the scene, renderer, camera, light, and directional light.
```javascript
this.initialize = function(){
	this.createScene();
	this.createRenderer();
	this.createCamera();
	this.onResizeRenderer();
	this.createLight();
	this.createDirectionalLight();
	this.createOrbitControl();
	this.camera.position.set(-2, 2, 3);
}
```

##### 2. Set up the mouse controL. 

* Create the OrbitControls so that we can pan around with the mouse.
```javascript
this.createOrbitControl = function() {
	this.controls = new THREE.OrbitControls(this.camera, this.renderer.domElement);
	....
}
```

##### 3. Render the scene set up and update the created mouse control.
* Render scene and update orbit control.
```javascript
this.renderScene = function() {
	this.renderer.render(this.scene, this.camera);
	this.controls.update();
	requestAnimationFrame($.proxy(this.renderScene, this));
}
```

##### 4. Provide the functions to interact with the 3d model.

* Zoom in/out the model.
```javascript
this.zoomModel = function(scale, callbackFunction) {
	....
		// things to do zooming the model.
}
```

* Rotate against Y axis.
```javascript
this.rotateAgainstYAxis = function(degree) {
	....
		// things to do rotation of the model.
}
```

* Translate the 3d model in Y axis.
```javascript
this.translateY = function(distanceTranslation) {
	....
		// things to do translation of the model.
}
```

##### 5. Handle the animation. Keyframe animation is used in this project.

### Collada Loader and Collada Model ###

* This code is used to load the collada model and add it to the scene.
```javascript
function loadColladaModel(modelUrl, initialLoadScale, initialLoadPosition) {
	var colladaLoader = new THREE.ColladaLoader();
	colladaLoader.load(modelUrl, function colladaReady(colladaGeometry) {
		....
		threeJSObject.scene.add(model);
	});
}
```


