
![](img/b2cfc85cbb129f60fe595a2bae074fe4_611_0.png)

Figure 23-1: My two visible graphics devices, Device 2 (left) and Device 3 (right), showing the final results of producing and manipulating two plots of the quakes data

## 23.1.3 Closing Device

To close a graphics device, either click the X with your mouse as you would close any device or use the dev.off function (you originally saw this command in Chapter 8 when closing a direct-to-file device). Calling dev.off() with no arguments closes the currently active device. Otherwise, you can specify the device number just as when using dev.set. To close the plot of the spatial locations, leaving the histogram as the active device, call dev.off with an argument of 2:

```
dev.off(2)
quartz
3
```

Then repeat the call without an argument to close the remaining device:

```
dev.off()
null device
1
```

Similar to dev.set, the printed output tells you what the newly active device is after you close one. When you close the last available actionable device, you're returned to the null device.

## 23.1.4 Multiple Plots in One Device

You can also control the number of individual plots in any device. There are a few ways to do this; I will describe the two easiest ways here.

### Setting the mfrow Parameter

Recall the par function is used to control various graphical parameters of traditional R plots. The mfrow argument instructs a new (or the currently active) device to invisibly divide itself into a grid of the specified dimensions, with each cell holding one plot. The mfrow option is a numeric vector of length 2 in the order of c(rows,columns); as you might expect, its default is c(1,1).

In your R session, make sure there are no plotting windows open. Say you want the two plots of quakes data side by side in the same device. You would set mfrow as a 1 x 2 grid with the vector c(1,2)—one row of plots and two columns.

```
R dev.new(width=8,height=4)
R par(mfrow=c(1,2))
R plot(quakes$long,quakes$lat,cex=0.02+quakes$stations,
     xlab="Longitude",ylab="Latitude")
R hist(quakes$stations)
R abline(v=mean(quakes$stations),lty=2)
```

The first line uses the optional arguments width and height to preset the dimensions of the new device, in inches, so it is twice as wide as it is high. Figure 23-2 shows exactly how the images are created, with a new plot filling the available cells as governed by the value of mfrow.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_612_0.png)

Figure 23-2: Using mfrow in par to generate a grid of plots in a single graphics device, showing the two plots of the quakes data

If you close any graphics devices and rerun this code without the lead-in call to dev.new, executing par(mfrow=c(1,2)) will automatically open a graphics device of the default square size of 7 x 7. The two plots will appear side by side but will be squashed. You can manually resize the device with your mouse to something more appropriate to the set value of mfrow,

and when you replot, the visualizations and their axes will be clearer.
You'll find you use this trial-and-error approach to produce multiple plots in a single device, especially if you don't want to be concerned with explicitly calling dev.new and setting width and height.

Note that use of par in this way will affect only the currently active device. Subsequent calls to dev.new will open new devices, for example, is set back to the default "one plot" with c(1,1). In other words, if you want to tailor the options of any new graphics device (including the direct-to-file devices), you need to set the required values of par after opening the device before executing any plotting commands.

### Defining a Particular Layout

You can refine the arrangements of plots in a single device using the layout function, which offers more ways to individualize the panels into which the plots will be drawn.

Return to the student survey data in survey in the MASS package. Suppose you want an array of three statistical plots—height on writing in handspans, side-by-side boxplots of height by smoking status, and a barplot of the frequencies of exercise of the students. If you want the plots arranged in a square device (as opposed to a single row or column of three plots), using nrow=0 in par may not work. You could set a square grid with par(mfrow=c(2,2)), but you would end up with a blank space for the cell with no image assigned to.

When you use layout, you provide the dimensions in mat as the first argument; these govern an invisible rectangular grid, just like controlling the nrow in mat. The difference is now that you can use numeric entries in mat to tell layout which plot number goes where. Examine the object:

```
R> lay.mat <- matrix(c(1,3,2,3),2,2)
R> lay.mat
     [1] [2]
[1,]  1    2
[2,]  3    3
```

The dimensions of this matrix create a 2 x 2 grid of plotting cells, the values inside lay.mat tell R that you want plot 1 to take the upper-left cell, plot 2 to take the upper-right cell, and plot 3 to stretch over the two bottom cells.

Calling layout as follows will either initialize the active device based on lay.mat or open a new one (if the new device is the only device currently available) and initialize it.

```
R> layout(mat=lay.mat)
```

If you're ever unsure of the result of your specification, you can use the layout.show function to see how plots will be placed. The following line produces the image on the left of Figure 23-3.

```
layout.show(n=max(lay.mat))
```

Then, once you've loaded the MASS package by calling library("MASS") you can access survey, running the following lines to place the plots in the order the plotting commands are executed, matched to the integers in lay.mat.

```
plot(survey$Wr.Hnd,survey$Height)
xlab="Writing handspan",ylab="Height"
boxplot(survey$Height$Smoke,
xlab="Smoking frequency",ylab="Height"
barplot(table(survey$Exer),horiz=TRUE,main="ExerciseExercise")
```

Note that if you've already closed the plot around layout, then you'll need to reinitialize a new device with the same call to layout for these three plots to display as intended. The result should look like the right of Figure 23-3.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_614_0.png)

Figure 23-3: Left: layout.show to visualize the planned plotting layout and order. Right: Demonstrating three plots of the survey data arranged according to lay.mat layout.

Probably the biggest benefit of layout is its ability to release the rigidity of plotting cells when compared to using the mfrow par option, you've just seen. Additional arguments to layout, namely, widths and heights, even allow you to preset the relative widths and heights of the cells as structured in the mat argument. See the documentation in ?layout for details; you'll find some other examples of its flexibility at the bottom of the file.

An unfortunate consequence of the two methods discussed here is the inability to edit a previous plot once you've finished it and moved on to the next. There is a split.screen function, which allows you to set several "screens" in a single device and switch between them. However, this method requires a lot of extra coding and in general doesn't behave well with regard to plotting regions and margins (the next section) in R. Many users (myself included) prefer to remain with layout, even if it means going through a bit of trial and error.

## 23.2 Plotting Regions and Margins

Although the main concern when plotting is the data set or model being visualized, it's additionally important to ensure the plot is annotated clearly and accurately to facilitate correct interpretation. To do this, you need to know how to manipulate and draw in all visible areas of a device, not just the area where your data lies. For any single plot created using base R graphics, there are three regions that make up the image.

- * The plot region is all you've dealt with so far. This is where your actual plot appears and where you'll usually be drawing your points, lines, text, and so on. The plot region uses the user coordinate system, which reflects the value and scale of the horizontal and vertical axes.
- The figure region is the area that contains the space for your axes, labels, and any titles. These spaces are also referred to as the figure margins.
- The outer region, also referred to as the outer margins, is additional space around the figure region that is not included by default but can be specified if it's needed.

You can explicitly measure and set margin space in a few different ways. One typical way is in terms of lines--specifically, the number of lines that can fit on top of one another parallel to each edge. You specify these as vectors of length 4 in a particular order; each of the four sides: c(bottom, left, top, right). The graphical parameters oma (outer margin) and mar (figure region) are used to control these amounts; like, they are initialized through a call to par before you draw any new plot.

### 23.2.1 Default Spacing

You can find your default figure margin settings with a call to par in R.

```
par()$oma
[1] 0000
par()$mar
[1] 5.1 4.1 2.1
```
