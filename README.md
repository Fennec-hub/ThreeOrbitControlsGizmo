# Three Orbit Controls Gizmo

This library is the continuation of **[jrj2211](https://github.com/jrj2211/three-orientation-gizmo)**'s work, a lightweight **Blender** like orientation **gizmo** for **Three.js** using an internal HTML5 Canvas, adapted here to work in tandem with a slightly modified version of **`THREE.OrbitControls`**, it follow the orbit controls changes and you can now change the camera angle by dragging the gizmo or select an axis by clicking on it.

**[Live Demo](https://fennec-hub.github.io/ThreeOrbitControlsGizmo/)**
<p align="center">
  <a href="https://fennec-hub.github.io/ThreeOrbitControlsGizmo/">
  <img src="https://raw.githubusercontent.com/fennec-hub/ThreeOrbitControlsGizmo/master/demo/ThreeObitControlsGizmo.gif" />
  </a>
</p>

### `THREE.OrbitControls` modifications :
In order to programmatically change the `OrbitControls` camera sphere angles (`spherical.theta` , `spherical.phi`) I had to access these two methods (`rotateLeft`, `rotateUp`), since they are internal functions I simply exposed them by adding these two lines :

```javascript
// These two lines are the only modifications done to THREE.OrbitControls
this.rotateLeft = rotateLeft;
this.rotateUp = rotateUp;
```

### Usage

```javascript
import { OrbitControls } from  "ThreeOrbitControlsGizmo/OrbitControls.js";
import { OrbitControlsGizmo } from  "ThreeOrbitControlsGizmo/OrbitControlsGizmo.js";

// Add the Orbit Controls
const controls = new  OrbitControls( camera, renderer.domElement );

// Add the Obit Controls Gizmo
const controlsGizmo = new  OrbitControlsGizmo(controls, { size:  100, padding:  8 });

// Add the Gizmo domElement to the dom 
document.body.appendChild(controlsGizmo.domElement);
```

#### Direct integration - Add by [GitHubDragonFly](https://github.com/GitHubDragonFly)

This non-module version of the OrbitControlsGizmo can be used directly in the `HTML` with either of below:
 - `<script src="OrbitControlsGizmo.js"></script>` - if no path is required
 - `<script src="../static/js/OrbitControlsGizmo.js"></script>` - with some path added

It has been used as such in Three.js viewers found on the [webpage](https://githubdragonfly.github.io/).

### Options
| Property | Default | description |
|--|--|--|
| size | 90 | Size of the gizmo `domElement` (`canvas`) |
| padding | 8 | Adds padding around the gizmo (makes it look nicer when using a circular background) |
| bubbleSizePrimary | 8 | Size of the circle for the positive axes (X,Y,Z) |
| bubbleSizeSecondary | 6 | Size of the circle for the negative axes (-x,-Y,-Z) |
| lineWidth | 2 | Size of the stroke to use for connecting the bubble to the center point |
| fontSize | 2 | Primary axes label font size |
| fontFamily | "arial" | Primary axes label font family |
| fontWeight | "bold" | Primary axes label font weight |
| fontColor | "#222222" | Primary axes label font color |
| className | "obit-controls-gizmo" | the `domElement` class name |
| colors | `{ x: ["#f73c3c", "#942424"], y: ["#6ccb26", "#417a17"], z: ["#178cf0", "#0e5490"] }` | Each axis [foreground, background] colors |

### Properties
- `.lock` Boolean : Lock all axes
- `.lockX` Boolean : Lock `X` axis
- `.lockY` Boolean : Lock `Y` axis

### Methods
- `.update()` : Update the gizmo orientation
- `.dispose()` : Dispose of the gizmo, remove the canvas from the dom, remove all event listeners

### Styling 
To get a **Blender** like  orientation gizmo style and effects add this to your css :

```css
.obit-controls-gizmo {
    position: absolute;
    top: 2em;
    right: 2em;
    z-index: 1000;
    background-color: #FFF0;
    border-radius: 100%;
    transition: background-color .15s  linear;
    cursor: pointer;
}

.obit-controls-gizmo.dragging, 
.obit-controls-gizmo:hover {
    background-color: #FFF3;
}

.obit-controls-gizmo.inactive {
    pointer-events: none;
    background-color: #FFF0  !important;
}
```
  
