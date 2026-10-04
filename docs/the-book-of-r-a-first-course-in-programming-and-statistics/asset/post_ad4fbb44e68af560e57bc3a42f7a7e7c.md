
```
R> xfromto <- rep(mtcars$hp,each=2)
R> yfromto <- rep(mtcars$wt,each=2)
R> zfromto <- rep(car$fitted.values,each=2)
R> zfromto <- seq(2,2+now(mtcars),2) <- mtcars$mpg
```

Here, the x and y-axis values don't change when moving from the "from" to the "to" location; these are simply double-replicates of each horsepower and weight entry of the original data frame. You need the z-axis "from" values to remain as the fitted values of the model (in other words, the actual vertical location of the response surface), and the "to" values are the raw z values. Then, a final call to segments3d draws on the residuals, as standard block line segments, for each text3d-labeled car.

```R
R> segments3d(x=xfromto,y=yfromto,z=zfromto)
```

Take a moment to interact with the final product, shown on the right of Figure 26-5.

## 26.2.3 Coloring by z Value

One advantage of pers3d plots is that you can color the surface according to the z values without needing to do anything. Recall that if you were using the base persp function, coloring by z value would require a minor workaround, because you'd need to calculate the relevant vertical position as the average of 4 adjacent z-matrix entries that make each facet (see Section 25.6.2).

Fortunately, this isn't necessary with pers3d. Continuing one last time the mtcars response surface, you can set up your desired color palette and assign colors to the entries of the z-matrix themselves without having to average out each 4 adjacent facet values.

```R
R> blues <- colorRPalette(c("cyan"
```

Then, using categorization to assign colors to a continuum, you just need to index blue200 by z.colors when specifying the col value in pers3d.

```R
R> persp3d(x=hp.seq,y=wt.seq,z=car.pred.mat,col=z.colors,
         alpha=0.6,xlab="Horsepower",ylab="Weight",zlab="mean MPG")
```

Figure 26-6 shows the result.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_737_0.png)

Figure 26-6: Showing a result of direct color assignment corresponding to the z-matrix value in persp3d mtcars response surface

## 26.2.4 Dealing with the Aspect Ratio

Taking a break from the mtcars model, you'll return to the bivariate kernel density estimate of the Chorley-Rible data, used in Sections 25.5 and 25.6. Load the spatstat package to access the chorley data and use the MASS package to access the kde2d function. Earlier for convenience, the following code calculates the KDE surface using kde2d, stored as the z component of the dens.WIN object:

```R
R> chorwin <- chorley$window
R> denswin <- kde2d(chorley$x,chorley$y,n=256,
      lim=c(chorwin$range,chorwin$range))
R> chorxy <- expand.grid(denswin$x,denswin$y)
R> choroutmat <- matrix(inside(chorxy[,1],y=chorxy[,2]),
      nrow=256,ncol=256)
R> denswin[choroutmat] <- NA
```

It also truncates the surface to fall within the polygon that represents the geographical region by setting all elements of the z-matrix outside that polygon to NA (studied in detail in Section 25.5.2). Then, executing the next few lines generates 200 colors from the built-in rainbow palette you've used previously for this KDE plot and categorizes the entries of the truncated z-matrix appropriately:

```R
R> zm <- denswin$z
R> bow <- rainbow(200,start=0,end=1)
R> breaks <- seq(min(zm,na.rm=TRUE),max(zm,na.rm=TRUE),length=200)
R> colors <- cut(zm,breaks=breaks,include.lowest=TRUE)
```

Again the difference is that you don't need to calculate facet averages as you did in Section 25.6.2. Before calling pers3d, it's worth remembering that you should consider the aspect ratio in the x- and y-coordinates. As you see in Section 26.1, the aspect argument in rgl functions a little differently than the asp argument in image or in persp. In rgl plots, including pers3d, aspect requests a numeric vector of length 3, which defines the relative scale of the x-, y-, and z-axes, in that order. To determine the appropriate relative scale for Chorley-Rible data, you need to calculate the total x-axis and y-axis widths that the study is defined upon and find their ratio.

```R
R> x <- chorwin$range[2]-chorwin$range[1]
R> x[1] 23
R> yd <- chorwin$range[2]-chorwin$range[1]
R> yd[1] 38
R> x/yd[1] 1.07572
```

This was done using the $xrange and $yrange components of the spatstat polygon, subtracting the lower limit from the upper in each case. The final ratio of x/yd reveals that you almost have a one-to-one scale, which technically means the region is physically wider in the x-axis, by a factor of around 1.076, than it is in the y-axis. Factoring that in, you can call persp3d to plot the KDE surface correctly.

```R
R> persp3d(denswin$x,denswin$y,denswin$z,
      col=colors,aspect=(x/yd,1,0.75),
      xlab="Eastings (km)",ylab="Northings (km)",zlab="Kernel")
```

You use aspect to stipulate that the x-axis should be scaled according to a factor of x/yd relative to the y-axis, that y is taken as the reference scale of 1, and the z-axis should be squashed by a factor of 0.75 relative to the y-axis. This is arbitrarily set so the graphic is similar to the original in Figure 25-21 on page 685. Let's finish the plot by adding a color legend. Ensure that the shape package loaded, resize your RGL device contains the result of the most recent call to persp3d, and execute the following command:

```
bgplot3d(plot.new());
colorlegend(col=colors,zlim=range(denswin$z,na.rm=TRUE),
      zval=seq(0,0.02,0.0025),main="KDE",digit=4,
      posx=c(0.87,0.9),posy=c(0.2,0.8)))
```

Remember that bgplot3d must be used to change the background of the current RGL device—refer to Section 26.1. You might want to experiment a little with posx and posy to find your preferred placement of the color legend. Figure 26-7 shows the result on your machine.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_739_0.png)

Figure 26-7: An interactive persp3d representation of the Chorley-Ribble kernel density estimate, colored according to z-axis values, with a static color legend

## Exercise 26.2

Return to the measurements in the built-in averiguar data frame. Create a copy of the data frame containing the variables temperature, wind speed, ozone level, and month; delete all with missing values. You're now going to experiment with rgl visualization of mean temperature.

- a. Refit the multiple linear model from Exercise 25.4 on page 676, which regressed temperature against main wind and ozone. Use expand.grid and predict to construct a z-matrix of the response surface; include 95 percent confidence interval for the fitted mean.
- b. Using the built-in topo.colors palette, replot the response surface, assigning the colors according to the z value and setting the opacity at 80 percent. 
- c. Enhance the plot from (b) as follows:
    - i. Generate exactly five colors from a custom palette that goes from "red4" to "pink" and add the wind, ozone, and temperature observations as points to the plot of the response surface. The points should be colored according to month (May through September) using these five colors in order. Set the size of the points to 10.
    - ii. Add vertical lines that denote the residuals of the fitted model to the plot; in other words, each observation should have a vertical line connecting it to the corresponding value of the response surface. These added lines should use the custom palette from earlier to match the color of each data point.
    - iii. Add the upper and lower 95 percent confidence limits stored as part of the model prediction in (a). The added surfaces should both be gray with 50 percent opacity.
    - iv. Add a legend to the top-right corner of the interactive plot referencing the five colors of points/lines according to month. Use a p value of 19 and a cex value of 2.
