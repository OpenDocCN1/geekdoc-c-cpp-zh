This obtains four levels—the quantiles above which the 80 percent, 60 percent, 40 percent, and 20 percent most densely clustered observations are identified. Then set up a couple of vectors to control the color and opacity of each increasing level of denseness accordingly.

```
R> qcols <- c("yellow","orange","red","red4")
R> qalpha <- c(0.2,0.3,0.4,0.5)
```

The range of colors and alpha levels means the isosurface will darken in color and become more opaque as the density increases.

One final time, replot the raw quak data using plot3d as earlier. Then it’s simply a matter of supplying your vectors of length 4 to each appropriate argument in contour3d.

```
R> contour3d(x=x.latt,y=y.latt,z=z.latt,f=quak.dens3d$estimate,
    color=qcols,level=qlevels,add=TRUE,alpha=qalpha)
```

Figure 26-15 shows the results. You can see that the tightest grouping of earthquakes occurs quite deep and toward the eastern edge of the 3D spatial prism (the visible “three-chamber” density blob is a well-known feature of these particular data).

# 26.4 Handling Parametric Equations

In most of the examples in the chapter so far, the surfaces are directly defined by the coordinates of a regular evaluation grid or lattice, but there are situations where the final axis you want to visualize is not a function of some evaluation grid. This occurs quite naturally when you simply want to draw familiar geometric shapes but also extends to more complicated situations in mathematics.

In this section, you’ll plot from a collection of parametric equations, which together define the shape or surface of interest. This section will assume you’re familiar with the fundamental trigonometric functions sine and cosine, as well as the conversion of angles from degrees to radians, since by default R deals exclusively with the latter. That said, I’ll walk you through the relevant calculations and R code as needed.

# 26.4.1 Simple Loci

Using mathematical terminology, a locus (plural loci) is a set of points that satisfy, and are defined by, a particular set of parametric equations. In R, these equations govern how individual numeric elements of the resulting objects are calculated, which you can then easily plot using familiar functions.

> NOTE
When discussing loci, any reference to 2D or 3D space refers to Euclidian space, which is the standard way in which you’ve dealt with coordinates in the x-, y-, and z-axes so far.