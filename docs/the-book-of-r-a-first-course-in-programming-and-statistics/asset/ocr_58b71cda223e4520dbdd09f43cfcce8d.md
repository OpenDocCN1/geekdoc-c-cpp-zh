# 26.3 Trivariate Surfaces

So far you've looked at bivariate functions of the form $z = f(x,y)$, where your evaluation grid is two-dimensional. In other words, you evaluate the function $f$ from an x value and a y value; the x and y values are plotted on the first two axes, and the values of $f$ are used to plot a third dimension. Next'll plot trivariate functions, which can be thought of as $w = f(x,y,z)$. That is, the evaluation grid is three-dimensional, and $f$ gives you a fourth value, $w$, to use for plotting the surface.

# 26.3.1 Evaluation Coordinates in 3D

When dealing with a trivariate mathematical function, you need an x, y, and z value to evaluate the result. Rather than a flat evaluation grid, you'll have an evaluation lattice that sits in a cube or some other 3D prism.
As perfect first example of a trivariate function, you'll create a "color cube" of RGB colors, where each point is the result of three values in red, green, and blue—refer to Section 25.1.1 for details. You'll use the physical axes to evaluate the evaluation lattice in the red, green, and blue values, and the result will be a point plotted with that color in position in the 3D space.
The following code sets the evaluation lattice in the three coordinate directions:

```
R> reds <- seq(0,255,25)
R> reds
[1] 0 25 50 75 100 125 175 200 225 250
R> greens <- seq(0,255,25)
R> blues <- seq(0,255,25)
R> full.rgb <- expand.grid(reds,greens,blues)
R> nrow(full.rgb)
[1] 1331
```

The first four lines generate equally spaced increasing sequences in the three colors spanning the standard to 0 to 255 RGB integer range. Then you use the built-in expand.grid function to generate the data frame of all color triplets according to these three sequences, resulting in an evaluation lattice of exactly $11^3 = 1331$ coordinates. Note that expand.grid works in the same way for higher-dimensional evaluation grids as it does for bivariate x-y grids (refer to Section 25.3.1).

Finally, a call to plot3d spheres at each 3D evaluation coordinate (recall the use of rgb command from Section 25.1.1):

```
R> plot3d(x=full.rgb[,1],y=full.rgb[,2],z=full.rgb[,3],
     col=rgb(full.rgb,maxValue=255,type="s",
     size=1.5,xlab="Red",ylab="Green",zlab="Blue")
```