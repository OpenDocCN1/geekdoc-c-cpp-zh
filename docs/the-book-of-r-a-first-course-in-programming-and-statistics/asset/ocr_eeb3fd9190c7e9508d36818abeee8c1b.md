R> quak.levs <- c(0.001,0.005,0.01,0.015)

Now, remember that by default, contour refreshes the graphics device and starts a new plot, but you want to avoid when adding contour to an existing plot. To do so, you need to explicitly specify add=TRUE. You have provided the four specified levels in quak.levs to levels and suppress labeling with drawlabels=FALSE. To control the appearance of contour lines at individual levels, you supply the sequence of integers 4:1 to lty, the first entry of which, 4, defines the line type of the contour at z = 0.001. The second entry, 3 specifies the line type of z = 0.005 contour, and so on. Lastly, all drawn contours to double-thickness with the single supplied value lwd=2. (You could supply a vector with four elements here too, if you want differing line thicknesses for the different contours. The element-wise contour extension extends to other aesthetics, such as color col.)

```
R> contour(quak.dens5,quak.dens2,add=TRUE,levels=quak.levs,drawlabels=FALSE,lty=4:1,lwd=2)
```

As a final touch, since the automatic labeling was suppressed in contour, a legend in the bottom-left corner of the plot region, referencing the values of the contours through the four different line types.

```
R> legend("bottomleft",legend=quak.levs,lty=4:1,lwd=2,title="Kernel estimate contours")
```

NOTE Many built-in and contributed base R plotting functions by default initialize, refresh or opens a new plot include an add argument as shown here. This allows you to use the graphics produced by these functions as additions to an already existing graphic. Look in the relevant help file to see whether this is for a given command.

# 25.4.2 Color-Filled Contours

For a straightforward variation on the contour plot, you can use color to fill the gaps between the levels that are drawn. Combined with a color legend, this removes the need to label the contour lines and in certain cases can make it easier to visually interpret fluctuations in the plotted-matrix surface.

The filled.contour function does this for you. You need to supply the increasing of grid coordinates in both the x-axis and y-axis directions, as well as the corresponding -matrix, to the x, y, and z in the same way as contour. The easiest way to specify the colors is to supply a color palette to the color.palette argument (which defaults to the built-in cm.colors palette; refer to Figure 25-2), and R does the rest.

Let’s use the mtcars response from Example 2 for a quick demonstration. If you don’t already have them in your current workspace, use