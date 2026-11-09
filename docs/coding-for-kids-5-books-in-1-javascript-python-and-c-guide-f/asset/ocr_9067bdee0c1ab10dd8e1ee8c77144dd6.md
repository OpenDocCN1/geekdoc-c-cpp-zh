```
```javascript
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
```

# Output #1: Move Down
Position 1

![](bbox=[0.129, 0.501, 0.481, 0.785])

# Position 2