coordinate (note that the ready-to-use letters object in R allows you to generate letters of the alphabet quickly):

```
R z<- letters[1:24]
R cbind(xycoords,z)

x y z
1 1 a
2 21 b
3 3 c
4 4 d
```

```
--snip--

21 34 u
22 44 v
23 54 w
24 6 x
```

What this emphasizes is each unique x-y evaluation coordinate, expressible via expand.grid, will have a z value associated with it. All together, these z values define the resulting surface.

# 25.3.2 Constructing the z-Matrix

The 3D plots to visualize a bivariate function require the z values corresponding to the x-y evaluation grid in the form of an appropriately constructed matrix. The size of the z-matrix is determined directly by the resolution of the evaluation grid; the number of rows corresponds to the number of unique x grid values, and the number of columns corresponds to the number of unique grid values.

You therefore need to take a little care turning your calculated z values into a matrix. When your vector of z-axis values corresponds to the evaluation grid arranged in the standard expand.grid function (in other words, where coordinates are stacked by increasing x values and repeated y values), be sure that your resulting z-matrix is filled in the default column-wise fashion (Section 3.1.1), with the number of rows and columns being exactly representative of the number of values in each of the x- and yvalue sequences, respectively (xcoords and ycoords earlier). In the current example, you know that the resulting z-matrix needs to be of size 6 × 4 because there are six locations and four y locations.

The following is the correct matrix representation of the hypothetical function vector z:

```
R nx<- length(xcoords)
R ny<- length(ycoords)
R zmat<- matrix(z,nrow=nx,ncol=ny)
```