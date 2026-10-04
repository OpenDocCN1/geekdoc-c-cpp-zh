
R> quak.dens - kde2d(x=quakes$long,y=quakes$lat,n=50)

Then you use persprot just as you'd used persp, without needing to specify either theta or phi.

R> persprot(x=quak.dens$,y=quak.dens$,z=quak.dens$,border="red3",shade=0.4, ticktype="detailed",xlab="Longitude",ylab="Latitude", zlab="Kernel estimate")

Figure 25-22 shows a series of screenshots of the rotating plot.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_720_0.png)

Figure 25-22: A rotating perspective plot of a KDE surface for the spatial earthquake locations, after a call to the custom persprot function

## Exercise 25.5

In Exercise 25.3 (a), you revisited the nuclear data set from the boot package and fitted two multiple linear regression models to model mean construction cost by permit date and plant capacity—one with main effects only and the other including an interaction term between the two continuous predictors.

- a. Refit the two versions of the model and produce perspective plots of the response surfaces based again on a 50 × 50 evaluation grid, taking the following into account:

- Use nrow in a call to par to display the two perspective plots next to each other. In the same call to par, override the default figure margins to have only one line of space on each side (par is explored in this role in Chapter 23).
- Use ylim to ensure both plots are displayed on the same scale of vertical axis, spin each one horizontally 25 degrees, and ensure detailed axis markings and tidy titles.
- Is there any visual indication that the presence of the interaction term has any meaningful impact on modeling the response?

- b. Start a fresh plot. To get a better idea of the difference between the two surfaces, produce a perspective plot of the z-matrix obtained as the elementwise difference between the individual z-matrices for the two fitted models in (a). What, in general, is the effect of including the interaction term?

Turn your attention back to the topographical information on the Auckland volcano, as the built-in R object volcano: an 87 × 61 matrix of elevation values (meters). You first looked at this in Section 25.4.1 as a contour plot.

- c. Produce the most basic, default perspective plot of the volcano, using simple integer sequences for the $x$- and $y$-coordinates.

- d. The plot in (c) is decidedly unappealing for a number of reasons. Produce a more realistic depiction of the volcano as per the following:
- Use a new graphics device with the margin widths reset to one, one, and four lines on the bottom, left, top, and respectively.
- The help file ?volcano reveals the $x$- and $y$-coordinates to which the volcano z-matrix corresponds is in 10-meter units. Using scale and altering expand, replot the surface with the correct aspect ratio in all three axes.
- Suppress all axis tick marks and notation using axes.
- The facets should be colored according to 50 colors generated from the built-in terrain.colors palette, and the facet border lines should be suppressed.

- Find your choice of visually appealing viewing angle.
- Use colorlegend from the shape package to place a color legend referencing elevation in meters in the space to the right of the plot. Experiment with the arguments to find appropriate placement and tick mark labels.

Here's my version of the improved plot:

![](img/b2cfc85cbb129f60fe595a2bae074fe4_722_0.png)

In Exercise 25.4, you looked at the spatial distribution of intentional fires in a region of Spain. Ensure the spatstat package is loaded, and then rerun the following lines to obtain the relevant objects:

```
R> fire <- split(climfires)$intentional
R> firewin <- climfires$window
```

- Borrow the code from Exercise 25.4 (d) and (e) to reproduce the kernel density estimate of this dispersion of observations, based on a 256 × 256 evaluation grid, truncated to the study region. Then, display it as a perspective plot according to the built-in:
- Just as with the pixel image, use 50 colors from the built-in heat,colors palette to color the facets by z value. Note the truncated z-matrix contains NA values.
- Border lines on the surface should be suppressed, and you should find your preferred choice of viewing angle.
- Use scale to ensure the correct spatial aspect ratio. In doing, you'll also need to adjust the z-axis expansion by a factor of around 5,000,000 for the density surface to be visible along the vertical, given the natural scaling of the density estimate on the specified evaluation grid.
- Employ detailed axis labeling and simply entitle the axes "X", "y", and "z" as appropriate.

# My product is given here.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_723_0.png)

f. Use the persprot function defined in Section 25.6.3 to view the surface from (e), setting skip=10.

## Important Code in This Chapter

| Function/operator | Brief description | First occurrence |
| :--- | :--- | :--- |
| col2d | RGB to color | Section 25.1 |
| rgb | RGB to hex | Section 25.1 |
| colorRamp | Custom palette | Section 25.1 |
| colorlegend | Legend | Section 25.2 |
| terrain.colors | Built-in | Section 25.1 |
| heat.colors | Built-in | Section 25.1 |
| gray.colors | Built-in | Section 25.1 |
| rainbow.colors | Built-in | Section 25.1 |
| palette | Built-in | Section 25.1 |
| scatterplot3d | 3D scatterplot | Section 25.2 |
| letters | Characters | Section 25.1 |
| contour | Contour plot | Section 25.1 |
| kde2d | Kernel estimate | Section 25.1 |
| image | Pixel images | Section 25.1 |
| inside | Inside region | Section 25.2 |
| persp | Perspective plot | Section 25.1 |
| grid | Evaluation | Section 25.1 |
| filled.contour | Filled contour | Section 25.1 |
| spatstat | spatstat | Section 25.2 |
| volcano | volcano | Section 25.4 |
| scale | scale | Section 25.1 |
| ylim | ylim | Section 25.1 |
| par | par | Section 25.1 |
| nrow | nrow | Section 25.1 |
| persprot | persprot | Section 25.1 |

# INTERACTIVE 3D PLOTS

![](img/b2cfc85cbb129f60fe595a2bae074fe4_724_0.png)

When it comes to 3D plots, it's important to be able to view them from different angles. The rgl package by Adler et al. (2015) offers some fantastic, simple-to-use functions that allow you to rotate. Under the hood, rgl utilizes OpenGL—a standard programming interface—to render the graphics on your screen. Install rgl (for example, by calling install.packages("rgl") at the prompt) and then library("rgl") to load it.

## 26.1 Point Clouds

Let's begin with the most basic of 3D plots—point clouds. In statistics, this tool is typically used to provide scatterplots of three continuous variables, as you saw when you created static 3Dplots.

### 26.1.1 Basic 3D Cloud

Return to the built-in iris data, composed of four measurements taken on three species. Create the following vectors in your workspace, as you did in Section 25.2.1:

```R
R pwid <- iris$Petal.Width
R plen <- iris$alal.Length
R swid <- iris$Sepal.Width
R slen <- iris$Sepal.Length
```

You use the plot3d function to display an interactive 3D cloud of points. It's called in the way familiar for scatterplots—by supplying the x, y, and z-coordinates to the x, y, and z arguments, respectively. The following opens an RGL device and produces a scatterplot of petal width, length, and sepal width:

```R
R plot3d(x=pwid,y=plen,z=swid)
```

You'll probably want to increase the size of the device with your mouse to see the data better. By left-clicking the plot and holding the button down, you can move the mouse to rotate the plot in any direction you like. If you right-click the plot and hold, you control the zoom. Specifically, right-clicking and holding moving the mouse upward will zoom out, right-clicking and holding while moving the mouse downward will zoom in. The axis tick marks and labels automatically appear on different sides on your viewing angle.
