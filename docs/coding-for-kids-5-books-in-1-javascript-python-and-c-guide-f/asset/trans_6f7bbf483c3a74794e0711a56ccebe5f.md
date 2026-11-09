
### 输出

![](img/443990a0ec620659ce8be783c0758bc6_378_0.png)

圆形

![](img/443990a0ec620659ce8be783c0758bc6_378_1.png)

圆形

## 绘图（圆形）

![](img/443990a0ec620659ce8be783c0758bc6_379_0.png)

## 不断增长的径向圆

径向圆与普通圆非常相似。径向圆控制圆形的颜色、背景色，还可以为圆形与背景之间的边框添加额外颜色。在下面的示例中，我们创建一个颜色为红色、背景为蓝色的径向圆。并且这个红色球体有一个黄色边框，起到圆环的作用。

在下面的示例中，使用 **createRadialGradient()** 来创建圆形。其工作原理如下。

**createRadialGradient(a,b,c,d,e,f)** 创建一个内圆，其 **中心 (a,b)** 的半径为 **c**。第二个圆创建一个 **中心 (d,e)**、半径为 **f** 的圆。如果我们想要一个环形圆，就应让它们位于同一中心，即 **(a,b) = (d,e)**。

在下面的示例中，我们在画布中心 **(250,250)** 处有一个内圆和一个外圆。外圆的半径始终比内圆大 **20** 像素。

内圆颜色使用 **addColorStop(0,"red")** 设置为红色，背景使用 **addColorStop(1,"blue")** 设置为蓝色。最后，外圆颜色使用 **addColorStop(0.5,"yellow")** 设置为黄色。

径向圆每 50 毫秒（0.05 秒）增大 5 像素。如果圆形的大小超出画布，则将其重置为 10 像素。

```html
<html>
<head><title>Growing Circle</title>
</head>
<body>
<canvas id="mCanvas" width="500" height="500" style="border:2px solid"></canvas><br>
<button class="btn" onclick="growingcircle()">Circle</button>
<script>
function growingcircle()
{
var c = document.getElementById("mCanvas");
var c2x = c.getContext("2d");
setInterval(frame, 50);
size=10;
function frame()
{
//circle
if (size>350)
{
size=10;
}
c2x.beginPath();
var grd = c2x.createRadialGradient(250, 250, size, 250, 250, size+20);
grd.addColorStop(0, "red");
grd.addColorStop(0.5, "yellow");
grd.addColorStop(1, "blue");

// Fill with gradient
c2x.fillStyle = grd;
c2x.fillRect(0, 0, 500, 500);
c2x.stroke();
c2x.fill();
size+=5;
}
}
</script>
</body>
</html>
```

### 输出

![](img/443990a0ec620659ce8be783c0758bc6_381_0.png)

![](img/443990a0ec620659ce8be783c0758bc6_381_1.png)

![](img/443990a0ec620659ce8be783c0758bc6_382_0.png)

## 沿不同方向移动的球

在下面的示例中，我们使用计时器和球函数，通过 4 个按钮让球沿 4 个不同方向移动。每个按钮都会运行将球沿特定方向移动的函数。

例如，如果我们按下向下按钮，它会使用 **MoveDown()** 函数让球向下移动。一旦球到达画布底部，它就会再次从顶部重新开始。

在每个函数中，我们设置一个位置变量来指示球的起点。在 MoveUp() 和 MoveDown() 中，我们分别将 y 位置设置为 500 和 0。使用 setInterval 函数，我们每 50 毫秒（0.05 秒）将位置变量增加/减少 5 像素，从而移动球。并且，我们使用 IF 函数检查球是否已到达画布边缘，并将其重置回初始状态。

```html
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

function MoveUp()
{
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
setInterval(frame, 50);
locY=500;
function frame()
{
//Circle
if (locY<0)
{
locY=500;
}
ctx.beginPath();
ctx.clearRect(0, 0, 500, 500);
ctx.arc(250,locY,30,0,2*Math.PI);
ctx.fillStyle = "blue";
ctx.stroke();
ctx.fill();
locY=locY-5;
}
}

function MoveRight()
{
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
setInterval(frame, 50);
locX=10;
function frame()
{
//Circle
if (locX>500)
{
locX=10;
}
ctx.beginPath();
ctx.clearRect(0, 0, 500, 500);
ctx.arc(locX,250,30,0,2*Math.PI);
ctx.fillStyle = "blue";
ctx.stroke();
ctx.fill();
locX=locX+5;
}
}

function MoveLeft()
{
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
setInterval(frame, 50);
locx=500;
function frame()
{
//Circle
if (locx<0)
{
locx=500;
}
ctx.beginPath();
ctx.clearRect(0, 0, 500, 500);
ctx.arc(locx,250,30,0,2*Math.PI);
ctx.fillStyle = "blue";
ctx.stroke();
ctx.fill();
locx=locx-5;
}
}
</script>
</body>
</html>
```

### 输出 #1：向下移动

### 位置 1

![](img/443990a0ec620659ce8be783c0758bc6_385_0.png)

### 位置 2

![](img/443990a0ec620659ce8be783c0758bc6_386_0.png)

### 输出 #2：向左移动

### 位置 1

![](img/443990a0ec620659ce8be783c0758bc6_386_1.png)

### 位置 2

![](img/443990a0ec620659ce8be783c0758bc6_387_0.png)

### 绘图（向下移动）

如下所示，loc 从 10 开始并不断增大，使其在动画中向下移动。

![](img/443990a0ec620659ce8be783c0758bc6_387_1.png)

## 弹跳球

在此示例中，我们将球移向画布边缘，当球碰到画布时会反弹回来。

这是通过修改决定球 x 位置和 y 位置的等式来实现的。

首先，在这种情况下，我们同时让球沿 x 和 y 位置移动。因此，我们有两个独立的变量，**locationx** 和 **locationy**。还有另外 2 个变量决定球移动的方向；**snx** 和 **sny**。如果 snx 为正，则向右移动。如果 snx 为负，则向左移动。因此，locationx 和 locationy 的等式为：

```text
locationx=locationx+snx*5
locationy=locationy+sny*5
```

因此，我们让球沿 x 方向移动 5 像素（向左或向右），并沿 y 方向移动 5 像素（向上或向下）。

如果球到达画布侧边（**locationx=500** 或 **locationx=0**），则改变 x 方向运动的方向（`snx=snx*-1`）。

并且，如果球到达画布上/下边缘（**locationy=500** 或 **locationy=0**），则改变 y 方向运动的方向（`sny=sny*-1`）。

这种方向变化产生了我们在屏幕上看到的反弹效果。

```html
<html>
<head><title>Bouncing Ball</title>
</head>
<body>
<canvas id="myCanvas" width="500" height="500" style="border:2px solid"></canvas><br>
<button class="btn" onclick="bouncingball()">Bounce Ball</button>
<script>
function bouncingball()
{
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
var snx=1;
var sny=1;
setInterval(function ()
locationx=Math.random()*350;
locationy=Math.random()*350;
function frame()
{
//Circle
ctx.beginPath();
ctx.clearRect(0, 0, 500, 500);
ctx.arc(locationx,locationy,20,0,2*Math.PI);
ctx.fillStyle = "red";
ctx.stroke();
ctx.fill();
if (locationx>=500)
{
        snx=snx*-1;
}
if (locationx<=0)
{
        snx=snx*-1;
}
if (locationy>=500)
{
        sny=sny*-1;
}
if (locationy<=0)
{
        sny=sny*-1;
}
locationx=locationx+snx*5;
locationy=locationy+sny*5;
}
}
</script>
</body>
</html>
```

### 输出

![](img/443990a0ec620659ce8be783c0758bc6_390_0.png)

弹跳球

![](img/443990a0ec620659ce8be783c0758bc6_390_1.png)

弹跳球

### 绘图（底部墙壁反弹）

![](img/443990a0ec620659ce8be783c0758bc6_391_0.png)

### 绘图（右侧墙壁反弹）

![](img/443990a0ec620659ce8be783c0758bc6_391_1.png)

