![](bbox=[0.156, 0.086, 0.723, 0.396])

Figure 5.6 The view of a world where the screen resolution is 1024×768 and there's a 1:1 ratio between a pixel and a unit in world space

With this view of the world, it's not too difficult to convert from world space into clip space. Simply divide the x-coordinate by width / 2 and divide the y-coordinate by height / 2. In matrix form, assuming 2D homogeneous coordinates, this simple view projection matrix is as follows:

```
SimpleViewProjection = [
  2 / width   0         0
  0         2 / height  0
  0         0           1
]
```

```
SimpleView Projection
= [
  2 / width   0         0
  0         2 / height  0
  0         0           1
]
```