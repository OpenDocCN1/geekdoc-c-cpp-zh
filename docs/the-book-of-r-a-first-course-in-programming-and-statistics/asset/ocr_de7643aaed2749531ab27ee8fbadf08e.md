As you progress to plot some actual surfaces of interest, you should keep the concept of the z-matrix as illustrated in Figure 25-9 in mind. The $6 \times 4$ grid used in this hypothetical example is coarse. In practice, you would usually use finer grids in terms of the resolution of the $x$ and $y$-sequences to improve the visual appearance of the surface.

# 25.4 Contour Plots

One of the most common plots used to display a surface based on evaluation of a function over a grid of bivariate coordinates is the *contour plot*. Contour plots are perhaps most easily explained as a series of lines—the contours—drawn over the 2D evaluation, with each contour marking a specific level of the surface of interest.

# 25.4.1 Drawing Contour Lines

Based on a numeric z-matrix, the $R$ function contour is what's used to produce the contours connecting $x$-$y$ coordinates that share the same $z$ value.

# Example 1: Topographical Map

For example, you will use another ready-to-use data set—the volcano object. This data set is simply a matrix containing measurements of elevation above sea level (in meters) of a dormant volcano over a rectangular area in the Auckland region of New Zealand; see the documentation for details. To view the topography, you need the volcano object (which is your z-matrix) and the relevant $x$-$y$ sequences. In this case, use integers corresponding to the size of the volcano matrix (row and column numbers can be obtained with a simple call to `dim`;; see Section 3.1.3).

```
R> dim(volcano)
[1] 87 61
R> contour(x=1:row(volcano),y=1:ncol(volcano),z=volcano,asp=1)
```

The $x$ and $y$-sequences are provided to $x$ and $y$, respectively, and the $z$-matrix to $z$. The optional argument $asp=1$, referring to the aspect ratio of the plot, forces a 1-to-1 unit treatment of the coordinate axes (as is when the units have a physical size interpretation, like plots of geographical regions—as is the case here).

Figure 25-1 shows the result of this example. By default, $R$ automatically chooses the levels of $z$ at which to draw the contours for an aesthetically pleasing result. Contours are also selectively labeled with their corresponding $z value. Looking at the topography, you can see the highest peak is a rim on the left, marked by an oblong contour with a depression (at around 160 m) falling immediately to the right.