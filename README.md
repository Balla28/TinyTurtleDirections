# Unit 8 Project 1 || Tiny Turtle Directions
![Imgur](http://i.imgur.com/Nh1qdMJm.jpg)

Tiny Turtle is a fun Computer Science activity created by a ScriptEd volunteer that teaches students how to use JavaScript functions. The original documentation can be found [here](https://github.com/toolness/tiny-turtle).


#Directions for Set Up
**Step 1: New Repo**      
Create a new GitHub repo called **TinyTurtle**.

<br>
**Step 2: Clone**   
Clone your new repo into a Cloud 9 workspace with a similar name.

<br>
**Step 3: New Files**   
Create four new files in this workspace. Name these new files...

* index.html
* style.css
* script.js
* tinyTurtle.js

<br>
**Step 4: index.html**  
Copy and paste the code below into your index.html file

```
<!DOCTYPE html>
<html>
<head>
  
  <title>Tiny Turtle</title>
  <link rel="stylesheet" type="text/css" href="style.css">
  
</head>
<body>
    <h1>Tiny Turtle</h1>
  <canvas></canvas>
  
  <script src="tinyTurtle.js"></script>
  <script src="script.js"></script>
</body>
</html>
```

<br>

**Step 5: tinyTurtle.js**  
Copy and paste the code below into your tinyTurtle.js file

```
// tiny-turtle.js
// 2013-10-11
// Public Domain.
// For more information, see http://github.com/toolness/tiny-turtle.

function TinyTurtle(canvas) {
  canvas = canvas || document.querySelector('canvas');

  var self = this;
  var rotation = 90;
  var position = {
    // See http://diveintohtml5.info/canvas.html#pixel-madness for
    // details on why we're offsetting by 0.5.
    x: canvas.width / 2 + 0.5,
    y: canvas.height / 2 + 0.5
  };
  var isPenDown = true;
  var radians = function(r) {return 2 * Math.PI * (r / 360) };
  var triangle = function(ctx, base, height) {
    ctx.beginPath(); ctx.moveTo(0, -base / 2); ctx.lineTo(height, 0);
    ctx.lineTo(0, base / 2); ctx.closePath();
  };
  var rotate = function(deg) {
    rotation = (rotation + deg) % 360;
    if (rotation < 0) rotation += 360;
  };

  self.penStyle = 'black';
  self.penWidth = 1;
  self.penUp = function() { isPenDown = false; return self; };
  self.penDown = function() { isPenDown = true; return self; };
  self.forward = self.fd = function(distance) {
    var origX = position.x, origY = position.y;
    position.x += Math.cos(radians(rotation)) * distance;
    position.y -= Math.sin(radians(rotation)) * distance;
    if (!isPenDown) return;
    var ctx = canvas.getContext('2d');
    ctx.strokeStyle = self.penStyle;
    ctx.lineWidth = self.penWidth;
    ctx.beginPath();
    ctx.moveTo(origX, origY);
    ctx.lineTo(position.x, position.y);
    ctx.stroke();
    return self;
  };
  self.stamp = function(size) {
    var ctx = canvas.getContext('2d');
    ctx.save();
    ctx.strokeStyle = ctx.fillStyle = self.penStyle;
    ctx.lineWidth = self.penWidth;
    ctx.translate(position.x, position.y);
    ctx.rotate(-radians(rotation));
    triangle(ctx, size || 10, (size || 10) * 1.5);
    isPenDown ? ctx.fill() : ctx.stroke();
    ctx.restore();
    return self;
  };
  self.left = self.lt = function(deg) { rotate(deg); return self; };
  self.right = self.rt = function(deg) { rotate(-deg); return self; };

  Object.defineProperties(self, {
    canvas: {get: function() { return canvas; }},
    rotation: {get: function() { return rotation; }},
    position: {get: function() { return {x: position.x, y: position.y}; }},
    pen: {get: function() { return isPenDown ? 'down' : 'up'; }}
  });

  return self;
}
```
**Step 6: Canvas CSS**  
You will notice a new HTML tag is being used. This tag is called `canvas`
In the `style.css` page give your canvas tag the following attributes

* a width of 400px
* a height of 400px
* a border (any style)

<br>
**Step 7: JavaScript Set Up**  
In the `script.js` page paste the code below on line 1


```
	TinyTurtle.apply(window); 
``` 

**Step 8: Play Turtle**  
Tiny Turtle understands the following commands:

* forward();
* right();
* left();
* stamp(); <------ This shows which direction the turtle is pointing.  

Use the commands above to make Tiny Turtle travel in a Square.

**Step 9: House**  
For the final piece of this project create a house (square with a triangle ontop)

