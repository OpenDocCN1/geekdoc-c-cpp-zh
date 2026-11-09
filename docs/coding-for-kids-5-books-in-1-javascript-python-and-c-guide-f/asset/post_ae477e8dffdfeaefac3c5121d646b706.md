
**Output:**
![](img/443990a0ec620659ce8be783c0758bc6_364_0.png)

**Drawing (Measurements):**
Here’s Circle 2 (blue circle) measuring using the canvas co-ordinates, just to show an example.
![](img/443990a0ec620659ce8be783c0758bc6_364_1.png)
Circle #2

## Creating a Rectangle on the Canvas

The drawing of a rectangle begins the same way as a circle; with the canvas and 2D context variables. Again, we use **beginPath()** and **clearRect()** to start the process. Then we use a function known as **fillRect()** which is shown below:

**fillRect(a,b,c,d)** means that the top left corner of the rectangle starts at an x-coordinate of **a** and a y-coordinate of **b**; it has a width of **c** and a height of **d**. So, we start at **(a,b)**, and clear a canvas of width c and height d.

In the example below, we start at **(0,0)**, and create a rectangle of width 50 pixels and height 100 pixels. It is a red rectangle (since fillRect is red).

There is also a second **fillRect()** which creates a square of width 75 pixels (as both width and height are set to the same value of 75). The top left corner of the square starts at **(150,150)**.

In both cases, fillRect() automatically draws and fills the rectangle with the assigned color.

```html
<html>
<head><title>Sample Canvas</title>
</head>
<body>
<canvas id="aCanvas" width="500" height="500" style="border:2px solid"></canvas><br>
<button class="btn a" onclick="drawSquare()">Draw Square</button>

<script>
function drawSquare()
{
var i = document.getElementById("aCanvas");
var c2x = i.getContext("2d");

//Rectangle 1
c2x.beginPath();
c2x.fillStyle = "red";
c2x.clearRect(0, 0, 500, 500);
c2x.fillRect(0, 0, 50, 100);

//Square 1
c2x.beginPath();
c2x.fillStyle = "blue";
c2x.fillRect(150, 150, 75, 75);
}
</script>
</body>
</html>
```

**Output:**
![](img/443990a0ec620659ce8be783c0758bc6_366_0.png)

**Drawing (Rectangle 2):**
![](img/443990a0ec620659ce8be783c0758bc6_366_1.png)

## Creating a Smiley Face

In the below example, we use our knowledge of circles and semi-circles to create a smiley face.

First, we do a yellow circle of 75 pixel radius in the center of the screen, which is the face. We then draw 2 small black circles of 10 pixels each which serve as the eyes.

And finally, we do a semi-circle filled with black color of radius 30 pixels. This is the smile.

Pretty cute, huh? You can get creative and make any face you want.

```html
<html>
<head><title>Smiley Face</title>
</head>
<body>
<canvas id="accanvas" width="500" height="500" style="border:2px solid"></canvas><br>
<button class="btn" onclick="drawsquare()">Draw Square</button>
<script>
function drawsquare()
{
var i = document.getElementById("accanvas");
var c2x = i.getContext("2d");

//Yellow Face
c2x.beginPath();
c2x.clearRect(0, 0, 500, 500);
c2x.arc(250,250,75,0,2*Math.PI);
c2x.fillStyle = "yellow";
c2x.stroke();
c2x.fill();

//Black Eyes
c2x.beginPath();
c2x.arc(225,225,10,0,2*Math.PI);
c2x.fillStyle = "black";
c2x.stroke();
c2x.fill();

c2x.beginPath();
c2x.arc(275,225,10,0,2*Math.PI);
c2x.fillStyle = "black";
c2x.stroke();
c2x.fill();

//Black Smile

c2x.beginPath();
c2x.arc(250,275,30,0,1*Math.PI);
c2x.fillStyle = "black";
c2x.stroke();
c2x.fill();
}
</script>
</body>
</html>
```

**Output:**
![](img/443990a0ec620659ce8be783c0758bc6_368_0.png)
Draw Square

## Timer and Animations

### What is a Timer?

A timer in JavaScript is used to time JavaScript code. It allows the user to execute different portions of the code at different time intervals. **setTimeout()** and **setInterval()** functions are used to set the timer. **setTimeout()** allows a fixed break before executing a code; **setInterval()** allows the code to be executed multiple times with a fixed interval between each execution. For example: **setTimeout(a, 1000)** executes the function **a** after **1000 ms (1 second)**. **setInterval(a, 1000)** keeps executing the function with a break of **1000 ms (1 second)** between runs. These functions are the key to running JavaScript animations.

### Timer Example

In our code, we only use the **setInterval()** function. In the example below, we have two buttons that run two separate functions. The first function **writename()** prints the name “Bob” on the screen every 2500 ms (or 2.5 seconds). The function **fname()** is run using **setInterval(fname, 2500)** and write the name “Bob”. The second function runs the function **setcount()** prints numbers starting from 1 and increments it by 1 each time with a break of 500 ms (0.5 seconds). So, it prints 1,2,3,4 and so on with a break of 0.5 seconds between each print.

```html
<html>
<head><title>Counting Timer</title>
</head>
<body>
<link rel="stylesheet" href="samplestyle.css" />
<button class="btn a" onclick="setcount()">Count</button>
<button class="btn a" onclick="writename()">Write Name</button>

<script>
function writename()
{
var name="Bob";
setInterval(fname, 2500);
function fname()
{
document.write('<link rel="stylesheet" type="text/css" href="samplestyle.css" />');
document.write(name);
document.write('<br>');
}
}

function setcount()
{
count=0;
setInterval(timeUp, 500);
function timeUp()
{
document.write('<link rel="stylesheet" type="text/css" href="samplestyle.css" />');
count=count+1;
document.write(count);
document.write('<br>');
}
}
</script>
</body>
</html>
```

**Output 1:**
![](img/443990a0ec620659ce8be783c0758bc6_371_0.png)

On clicking **Count**,
![](img/443990a0ec620659ce8be783c0758bc6_372_0.png)

**Output #2**
![](img/443990a0ec620659ce8be783c0758bc6_372_1.png)

On clicking **Count**
![](img/443990a0ec620659ce8be783c0758bc6_373_0.png)

## Growing Square

We use the **setInterval** and **fillRect** functions to write a program that expands a square. A button when clicked runs the growing square function. In the growing square function, we do a **setInterval** where we run the function **frame()** every 10 ms (0.01 seconds). We declare a variable size to 10 pixels. **Size** contains the length of the square.

In the function frame, we first clear the entire canvas using **clearRect()**. Then we draw a rectangle starting at (0,0) of length ‘**size**’. **Size** is increased by 5 every time the function is executed. Once size is greater than 500, it is set back to 10. This ensures that once the square is larger than the canvas, it restarts growing from a small size.

```html
<html>
<head><title>Growing Square</title>
</head>
<body>
<canvas id="myCanvas" width="500" height="500" style="border:2px solid"></canvas><br>
<button class="btn a" onclick="growingsquare()">Square</button>
<script>
function growingsquare()
{
var i = document.getElementById("myCanvas");
var c2x = i.getContext("2d");
setInterval(frame, 10);
size=0;
function frame()
{
if (size>500)
{
size=0;
}
c2x.clearRect(0, 0, 500, 500);
c2x.fillRect(0, 0, size, size);
size=size+5;
}
}
</script>
</body>
</html>
```

**Output:**
![](img/443990a0ec620659ce8be783c0758bc6_375_0.png)
Square

**Drawing (Square grows)**
![](img/443990a0ec620659ce8be783c0758bc6_376_0.png)

## Growing Circle

We use the **setInterval** and **arc** functions to write a program that expands a circle. A button when clicked runs the **growing circle** function. In the growing circle function, we do a **setInterval** where we run the function **frame()** every 50 ms (0.05 seconds). We declare a variable size to 10 pixels. **Size** contains the radius of the circle.

In the function frame, we first clear the entire canvas using **clearRect()**. Then we draw a circle starting at the center of (250,250) of radius ‘**size**’. **Size** is increased by 5 every time the loop is executed. Once size is greater than 350, it is set back to 10. This ensures that once the circle is larger than the canvas, it restarts growing from a small size.

```html
<html>
<head><title>Growing Circle</title>
</head>
<body>
<canvas id="myCanvas" width="500" height="500" style="border:2px solid"></canvas><br>
<button class="btn a" onclick="growingcircle()">Circle</button>
<script>
function growingcircle()
{
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
setInterval(frame, 50);
size=10;
function frame ()
{
//Circle
if (size>350)
{
size=10;
}
ctx.beginPath();
ctx.clearRect(0, 0, 500, 500);
ctx.arc(250,250,size,0,2*Math.PI);
ctx.fillStyle = "blue";
ctx.stroke();
ctx.fill();
size=size+5;
}
}
</script>
</body>
</html>
```
