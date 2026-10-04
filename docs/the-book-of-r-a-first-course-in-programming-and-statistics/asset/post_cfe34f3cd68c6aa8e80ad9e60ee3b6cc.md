
Then, after loading ggplot, execute the following to produce the image on the left of Figure 24-1.

```
R> ggplot(surv, aes(x=Wr.Hnd,y=Height)) +
 geom_point(aes(col=Sex,shape=Sex)) + geom_smooth(method="loess")
```

The call to ggplot initializes the object and sets the default mapping of Wr.Hnd on the x-axis and height on the y-axis. The addition of geom_point adds the points, using color and point type to differentiate between males and females. The addition of geom_smooth superimposes the LOESS smoother. By default, a 95 percent confidence interval for the estimated trend is marked off by a transparent gray-shaded area.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_645_0.png)

Figure 24-1: Showcasing ggplot2 (left) and base R graphics (right) for display of nonparametric estimated trends using LOESS

Now I'll demonstrate how to produce a similar result using base graphics. Although there are base R functions, such as scatter.smooth, that can produce a scatterplot with the smoothed trend relatively quickly, to be able to do things with such shade in the confidence interval region, is helpful to be able to build the plot up by piece. The relative ease of the ggplot2 approach with this base R code, produces the image on the right of Figure 24-1:

```
R> plot(surv,Wr.Hnd,survHeight,col=survSex,pch=c(16,17),survSex)
R> smoother <- loess(Height~Wr.Hnd,data=surv)
R> handseq <- seq(min(surv$Wr.Hnd),max(surv$Wr.Hnd),length=100)
R> sm <- predict(smoother,newdata=data.frame(Wr.Hnd=handseq),se=TRUE)
R> lines(handseq,sm$fit)
R> polygon(x=c(handseq,rev(handseq)),
 y=c(sm$fit+2*sm$se,rev(sm$fit-2*sm$se)),
 col=adjustcolor("gray",alpha=0.5), border=NA)
```

The first line draws the data, and the syntax uses the built-in loess function to produce the smoothed trend—and the syntax is identical to that of lm. Just as with linear models fitted by lm, for drawing to begin, you need

set up a fine sequence of values of the x-axis variable at which to obtain the point estimates and their standard errors; this is achieved with seq in the third line, followed by predict in the fourth line with the se argument set to TRUE. This results in the object sm, a list with components $fit and $se as usual.

The smoothed trend is then drawn, using smooth in a call to lines. Finally, a rough 95 percent confidence interval is calculated for the predicted values minus twice the corresponding standard errors in se. This is done directly in the call to polygon, which draws the gray band by the vertices formed by the confidence interval; the color is given to the grey-filled shape to be transparent with a call to the ready-to-use adjustcolor, the argument alpha takes a value from 0, which is fully transparent; alpha=0.5 sets 50 percent opacity of the specified "gray"

All, and a legend hasn't been put yet! This example exposes the base R version of the image, requires not in terms of length of the script but also for the whole process of thinking its construction; for example, putting together the vertices of a polygon for the confidence region appropriately and remembering to adjust the offset of the filled shape to prevent preplotted covered. This becomes more apparent the moment you become a little more ambitious with such features. Suppose you wanted to superimpose smoothers for each sex separately; this would require separate estimation of the LOESS functions and a rethink of the plotting strategy. However, this addition is simple in ggplot terms, requiring a change in the aesthetic mapping of the relevant geom. The following code produces

Figure 24-2:

```
R> ggplot(surv, aes(x=Wr.Hnd, y=Height, col=Sex, shape=Sex)) + 
  geom_point() + geom_smooth(method="loess")
```

All that's needed is that the aesthetic mapping for color and point type (col=Sex and shape=Sex, respectively) has shifted so that instead of being specific to the plotted points only, it's part of the default mapping declared in the initialization call to ggplot. Any layer added after that doesn't assign the mapping will follow this default, as is the case for geom_point and geom_smooth.

NOTE The implementation of LOESS and other trend smoothers depends on you specifying the amount of smoothing you want; this is controlled by the proportion of data to use each localized weighted subset, for each step/location in the estimation procedure. A larger proportion leads to a smoother, less variable trend than a smaller proportion. This value, referred to as the span, can be set by the optional argument span in either loess or geom_smooth; however, for quick data exploration, the default value of 0.75 is usually adequate. You can try experimenting with this on the example plots in this section to see the effects on the respective.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_647_0.png)

## 24.2.2 Constructing Smooth Density Estimates

The idea of smoothing isn't limited to scatterplot trends. Kernel density estimation (KDE) is a method for producing a smooth estimate of a probability density function, based on observed data. Briefly, KDE involves a scaled probability function (the kernel) to each observation in a data set and summing them all to give an impression of the distribution of the data set as a whole. It's basically a sophisticated version of a histogram. For theoretical details, the text by Wand and Jones (1995) is a good reference.

To illustrate this method, consider the built-in airquality data frame; enter ?airquality at the prompt to open the documentation, which tells you it contains a number of measurements taken of the air in New York over several months. A basic plot of the kernel estimate of the density of the temperature measurements is provided with the following line and shown on the Figure of 24-3:

```
R> ggplot(data=airquality,aes(x=Temp)) + geom_density()
```

Such plot is relatively easy to create with R graphics as well, using the built-in command to implement KDE for a given data vector. However, ggplot2 lets you dress the plot using aesthetic mappings with relative ease—a big draw for ggplot2. For example, suppose you want to visualize the density estimates for temperature separately according to the month of observation. First, execute the following code:

```
R> air <- airquality
R> air$Month <- factor(air$Month, labels=c("May", "June", "July", "August", "September"))
```

![](img/b2cfc85cbb129f60fe595a2bae074fe4_648_0.png)

**Figure 24-3:** *Visualizing temperature distributions in the airquality data frame via KDE, using ggplot2 functionality*

This has created a copy of the airquality data frame in your workspace and recoded the originally numeric Month vector as a factor vector (as required for ggplot mappings), labeling the entries appropriately. Using air, the following code produces the right-hand plot in Figure 24-3:

```
R> ggplot(data=air,aes(x=Temp, fill=Month)) + geom_density(alpha=0.4) + ggtitle("Monthly temperature probability densities") + labs(x="Temp (F)",y="Kernel estimate")
```

The different densities are clearly identified by different colors, using fill=Month in aes in the plot initialization mapped out by ggplot. You additionally supplied alpha=0.4 to geom_density to set 40 percent opacity so you can see all five curves. The remaining calls to ggtitle and labs simply tidy up the main and axis titles. The features of the distributions of these measurements are as you might expect—temperatures for July, the hottest month, are centered over a far higher range of values than, say, for May.

> just like LOESS techniques, the precise appearance of kernel-estimated probability density function is dependent on the amount of smoothing enabled. Like binwidth in the histogram, the quantity of interest in KDE is referred to as the bandwidth or smoothing parameter—a larger bandwidth imposes smoother smoothing over the range of the data. By default, the bandwidth is automatically chosen using a data-driven technique in these examples. This default level of smoothing is generally acceptable for simple exploration of your data.
