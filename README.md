aframe-button-controls
===

An [A-Frame](https://aframe.io) [WebVR](https://webvr.info/) component that supports the controller functionality
available everywhere - buttons.  Especially useful for apps designed to be usable with Google Cardboard V2, Gear VR
without a separate Controller, mobile and desktop.

Fires a **buttondown** event when *any* button on *any* controller is pressed, including the virtual controller in
Chrome in VR mode. Also fires when a pointerdown/touchstart/mousedown event is fired on the scene element and 
not handled by another element,
so it's uniform across browsers for Cardboard, and usable in flat mode, 
on mobile and on desktop.

Likewise fires a **buttonup** event.

Button events, in the **detail** property, have a **controllerId** property for the controller 
and an **index** property to distinguish which button on the controller was pressed.
You should only use indexes greater than 0 for optional commands, as Cardboard, mobile, and desktop have only one button.

Not appropriate as the base for object selection within a scene - for that you probably want 
[laser-controls](https://aframe.io/docs/0.8.0/components/laser-controls.html#sidebar).
 
Cannot detect the button on Cardboard V1, as the magnetic sensor is not exposed to browsers.

Basic use:
```html
	<script src="https://unpkg.com/aframe-button-controls@^1.0.1/aframe-button-controls.js"></script>
	
	<script>
		AFRAME.registerComponent('mystuff', {
			init: function () {
				let controlsEl = document.querySelector('[button-controls]');
				controlsEl.addEventListener('buttondown', function (evt) {
					// ...
				});
				controlsEl.addEventListener('buttonup', function (evt) {
					// ...
				});
			}
		});
	</script>

</head>
<body>
	<a-scene mystuff></a-scene>

		<a-entity button-controls></a-entity>
```

If using [aframe-state-component](https://www.npmjs.com/package/aframe-state-component),
you can create **buttondown** and **buttonup** handlers, instead of calling addEventListener yourself.
