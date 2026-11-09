```
<html>
<head><title>Growing Circle</title>
</head>
<body>
<canvas id="myCanvas" width="500" height="500" style="border:2px solid"></canvas><br>
<button class="btn a" onclick="moveDown()">Down</button>
<button class="btn a" onclick="moveUp()">Up</button>
<button class="btn a" onclick="moveRight()">Right</button>
<button class="btn a" onclick="moveLeft()">Left</button>

<script>
function MoveDown()
{
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
setInterval(frame, 50);
var loc=10;
function frame()
{
if (loc>500)
{
loc=10;
}
ctx.beginPath();
ctx.clearRect(0, 0, 500, 500);
ctx.arc(250,loc,30,0,2*Math.PI);
ctx.fillStyle = "blue";
ctx.stroke();
ctx.fill();
loc=loc+5;
}
}
</script>
```