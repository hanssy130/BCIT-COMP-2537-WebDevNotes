# Week4 — HTML5 Canvas

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
