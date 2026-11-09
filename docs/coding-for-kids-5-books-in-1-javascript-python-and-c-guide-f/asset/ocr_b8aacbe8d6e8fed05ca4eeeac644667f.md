```
```javascript
function press(event)
{
  if (keyc[event.keyCode]=="up")
  {
    moveup();
  }

  if (keyc[event.keyCode]=="down")
  {
    movedown();
  }
}
function frame()
{
  //Circle
  cx.beginPath();
  cx.clearRect(20,0,800,600);
  cx.arc(locationx,locationy,20,0,2*Math.PI);
  cx.fillStyle = "red";
  cx.stroke();
  cx.fill();
  dist=Math.sqrt((locationx-10)**2+(locationy-yrect)**2);
  //document.write(dist);
  if (locationx>=800)
  {
    snx=snx*-1;
  }
  if (dist<75)
  {
    snx=snx*-1;
    locationx=locationx+snx*20;
  }
  if (locationy>=600)
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
</script>
</body>
</html>
```
```