# 23.4.1 Graphical Parameters for Style and Suppression

If you want finer control over an R plot, you'll typically want to begin with a "clean slate". To do this, you need to be aware of the default settings of certain graphical parameters when calling a plotting function and how to suppress things such as boxes and axes. This is where you'll start.

For an example, let's plot MPG against horsepower (from the ready-to-use mtcars data set) and set each plotted point to be sized proportionally to the weight of each car. For convenience, create the following:

```
R hp <- mtcars$hp
R mpg <- mtcars$mpg
R wtcex <- mtcars$wt/mean(mtcars$wt)
```

The last object is the car weight scaled by its sample mean. This creates a vertex where cars less than the average weight have a value < 1 and cars more than the average weight have a value > 1, making it ideal for the cex parameter to scale the size of the plotted points (refer to Chapter 7).

Let's start by focusing on some more graphical parameters usually used in the first instance of a call to plot, paving the way for using the box and axis commands. Executing the following line gives you the default appearance of the plot and its box, axes, and labeling: this is shown as the leftmost image in Figure 23-8.

```
R plot(hp,mpg,cex=wtcex)
```

There are two axes "styles," controlled by the graphical parameters x and y axes. Their sole purpose is to decide whether to impose the small amount of additional horizontal and vertical buffer space that's present at the ends of each axis to prevent points being chopped off at the end of the plotting region. The default, xaxs="r" and yaxis="r", is to include that space. The alternative, setting one or both of these to "i", instructs the plot to be strictly defined by the upper and lower limits of the data (or by those supplied to xlim and/ ylim), that is, with no additional padding space.

For example, the following line produces the middle plot in Figure 23-8.

```
R plot(hp,mpg,cex=wtcex,xaxs="i",yaxis="i")
```

This is almost the same as the default, but now no padding space at the end of the axis; the most extreme data points sit right on the axis. Generally, the axis style "i" is fine, but on occasions where you need finer control over the axes' scales and the that additional buffer space can be problematic. In those occasions, you'll often see ylim/ylim being used in conjunction with xaxis="i"/yaxis="i".