# Week4 — HTML5 Canvas

### Overview
- 2D drawing platform
- uses only JavaScript & HTML, no plugins
- Extensible through JS API
- Created by Apple for dashboard widgets
- openly developed as a W3C spec

### Bitmap vs Vector
Canvas is a bitmap system
- Everything is a single, flat, picture
- If changes (adding a line), then whole picture is redrawn
SVG is a vector system
- Elements are drawn as separate DOM objects
- Can be manipulated individually

## The `<canvas` tag
- Similar to `<div>`
e.g.
```
<div> </div>
<canvas> </canvas>
```
- Area of `<canvas>` is used for drawing & animation

### Attributes
- ID
- width
- height
- either made with HTML, or created with JS/JQuery
- starts x,y coordinates from top left

```
<canvas id="myCanvas" width="600" height="400"> </canvas>
```

### HTML
```
<canvas id="myCanvas" width="600" height="400">
<p> Some default content if it doesn't support canvas </p>
</canvas>
```
Everything else needs JavaScript.

### .js
- HTML must load first, then run JS
- use `window.onload` in .js file, or jQuery's equivalent
- wrap all code for canvas to wait until page has loaded.

```
window.onload = draw;

function draw() {
  const canvas = document.getElementByID('myCanvas');
  if (canvas.getContext)
    let ctx = canvas.getContext('2d');
}

or 

window.onload = function() {
}
```

### ctx
- 2D rendering context
```
ctx.fillStyle = 'rgb(255, 0, 0)';
ctx.strokeStyle = 'rgba(0, 255, 0, 0.5)';
```
- use RGBA for alpha transparency
- `fillStyle()` and `strokeStyle()` define the style of shapes to be drawn
- `fillRect(x, y, w, h)` - Draws a rectangle using current fill style
- `strokeRect(x, y, w, h)` - Draws the outline of a rectangle using the current stroke style
- `clearRect(x, y, w, h)` - Clears all pixels within the given rectangle

### Complex Shapes & Paths
- Paths are a list of subpaths
- Subpaths are one or more points connected by straight or curved lines
- Renering context always has a current plan
- A new path should be created for each individual shape

- `begin Path()` - Resets the current path
- `closePath()` - Closes the current subpath and starts a new one
- `moveTo(x,y)` - Creates a new subpath at the given point
- `fill()` - Filsl the subpaths with the current fill style
- `stroke()` - Outlines the subpaths with the current stroke style


```
  <div>
    <input type="file" id="file" />  
  </div>
  <div id="image-container">
    <canvas width="500" height="500"></canvas>
    <div>
      <span>Top Line:</span><br/>
      <input id="topLineText" type="text"><br/>
      <span>Bottom Line:</span><br/>
      <input id="bottomLineText" type="text"><br/>
    </div>
  </div>
```

```
<script>
    function textChangeListener (evt) {
      let id = evt.target.id;
      let text = evt.target.value;
      
      if (id == "topLineText") {
        window.topLineText = text;
      } else {
        window.bottomLineText = text;
      }
      
      redrawMeme(window.imageObject, window.topLineText, window.bottomLineText);
    }
    
    function redrawMeme(image, topLine, bottomLine) {
      // Get Canvas2DContext
      let canvas = document.querySelector('canvas');
      let ctx = canvas.getContext("2d");
      if (image != null)
        ctx.drawImage(image, 0, 0, canvas.width, canvas.height);
      
      // Text attributes
      ctx.font = '30pt Impact';
      ctx.textAlign = 'center';
      ctx.strokeStyle = 'black';
      ctx.lineWidth = 3;
      ctx.fillStyle = 'white';
      
      if (topLine != null) {
        ctx.fillText(topLine, canvas.width / 2, 40);
        ctx.strokeText(topLine, canvas.width / 2, 40);
      }
      
      if (bottomLine != null) {
        ctx.fillText(bottomLine, canvas.width / 2, canvas.height - 20);
        ctx.strokeText(bottomLine, canvas.width / 2, canvas.height - 20);
      }
    }
        

    function handleFileSelect(evt) {
      debugger;
      let file = evt.target.files[0];
      
      let reader = new FileReader();
      reader.onload = function(fileObject) {
        let data = fileObject.target.result;
        
        // Create an image object
        let image = new Image();
        image.onload = function() {
          
          window.imageObject = this;
          redrawMeme(window.imageObject, null, null);
        }
        
        // Set image data to background image.
        image.src = data;
        console.log(fileObject.target.result);
      };
      reader.readAsDataURL(file)
    }
    
    window.topLineText = "";
    window.bottomLineText = "";
    let input1 = document.getElementById('topLineText');
    let input2 = document.getElementById('bottomLineText');
    input1.oninput = textChangeListener;
    input2.oninput = textChangeListener;
    document.getElementById('file').addEventListener('change', handleFileSelect);
  </script>
  ```
