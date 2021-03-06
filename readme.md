# Virtual Stick
A virtual joystick for touch devices.

[View Repo](https://github.com/l-brett/virtual-stick)

[Demo(for touch devices)](https://l-brett.github.io/virtual-stick/example.html)
## Usage

Install via npm or yarn
```
yarn add virtual-stick
```

```
npm add virtual-stick
```

Include the library in your project

node:
```js
const VirtualStick = require('VirtualStick.js').VirtualStick;
```
es6:

```js
import VirtualStick from 'VirtualStick';
```

 Basic Usage:
```js
let controller = new VirtualStick(options);
```

Getting data from the controller
```js
// in your update method
let data = controller.getAxis();
```

This provides the following data:
```js
{
    x: 0.4, //position on x-axis (between -1 - 1)
    y: 0.4, //position on y-axis (between -1 - 1)
    dx: 1, // dpad x-axis (1,-1 or 0) 
    dy: 1, //dpad y-axis (1,-1 or 0)
}
```

which could be used with something like:
```js
let axis = controller.getAxis();
player.x+=axis.x;
player.y+=axis.y;
```

drawing it:
```js
function gameLoop() {
    doOtherStuff();
    controller.draw();
}
```

Releasing touch events if the controller is no longer required
```js
controller.unbind();
```

This is the full list of configurable options:
```js
{
    'container': document.body, // The element to hook onto(any html element)
    'left':0, // Touch Capture Area left offset as percentage
    'top':0, // Touch Capture Area top offset as percentage
    'width':100, // Touch Capture Area width as percentage
    'height':100, // Touch Capture Area Height as percentage
    'track-size':150, // The size of the area to move the button in
    'button-size': 80, // The size of the thumbstick
    'button-color':'#FFFFFF99', //the background color of the thumbstick
    'button-stroke-color':'#FFFFFF', //the stroke color of the thumbstick
    'button-stroke-size':2, //thumbstick stroke width
    'track-color':'#00000099', //controller track area background color
    'track-stroke-color':'#FFFFFF', //controller track area stroke color
    'track-stroke-size':2, //controller track area stroke size
    'touch-handler': null // (Not required) can be used to attach multiple controllers to the same touch handler
}
```


Creating a 50/50 twin stick controller:
```js

import VirtualStick from 'VirtualStick';

let leftControl = new VirtualStick({
    width:50,
    'track-stroke-color':'#FF0000',
    'button-stroke-color':'#FF0000',
    'button-color':null
});

let rightControl = new VirtualStick({
    width:50,
    left:50,
    'track-stroke-color':'#0000FF',
    'button-stroke-color':'#0000FF',
    'button-color':null
});
```