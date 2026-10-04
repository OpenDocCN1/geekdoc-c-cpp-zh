
Figure 23-8: Plotting MPG against horsepower for the mtcars data; point size proportion-to car, using a call to a plot only. Left: Default appearance. Middle: Setting xaxt="" and yaxt="" to prevent the buffer spacing on the limits of the axes. Right: Using xat, yat, xlab, ylab, and bty to suppress all box, axis, and label label drawing (alternatively achieved by setting axes=FALSE and ann=FALSE).

If you want to control the specific appearance of any boxes, axes, and their labels, you'll want to start a plot with none of these and add them as your design. The rightmost plot in Figure 23-8 is the result of suppressing the default drawing of these by a call to either

```
plot(hp, mpg, cex=wtcars, xaxt="", yaxt="", bty="", xlab="", ylab="")
```

or

```
plot(hp, mpg, cex=wtcars, axes=FALSE, ann=FALSE)
```

You can achieve this by setting the parameters xaxt, yaxt, and bty to "" and setting the default axes labels xlab and ylab to the empty string "", or by simply suppressing both axes and ann to FALSE (the former suppressing all axes and the box, the latter suppressing any annotation). Although the first way might seem overcomplicated, it affords you great flexibility in suppressing each aspect of a given plot (as opposed to the "total" suppression enforced by the second approach).

## 23.4.2 Customizing Boxes

When you're starting with a suppressed-box or suppressed-axis plot, to add a box to the current plot region in the active graphics device, use box and specify its type with bty. For example, if you start with a plot like the one on the right of Figure 23-8 (just run the most recent line of code to get this), then additionally calling the following line provides you with the image on the left of Figure 23-9.

```
box(bty="")
```

The bty argument is supplied a single character: "o" (default), "1", "7", "c", "u", or "n". The help file for bty in ?par tells you that on

one of these values, the resulting box boundaries will follow the appearance of the corresponding uppercase letter, with the exception of "n" (which, as you saw a moment ago, will suppress the box).

![](img/b2cfc85cbb129f60fe595a2bae074fe4_627_0.png)

You can use other relevant parameters that you've met already, such as lty, lwd, and col, to further control the appearance of a box. Replot the data as in the middle of Figure 23-8 and then call the following to produce the image in the middle of Figure 23-9:

```
R box(bty="1",lty=3,lwd=2)
```

The final example on the right of Figure 23-9 is created with this line:

```
R box(bty="j",lty=2,col="gray")
```

## 23.4.3 Customizing Axes

Once you have the box you want it, you can focus on the axes. The axis function allows you to control the addition and appearance of an axis on any of the four sides of the plot region in first detail. The first argument it takes is side, provided with a single integer: 1 (bottom), 2 (left), 3 (top), or 4 (right). These numbers are consistent with the positions of the relevant margin-spacing values you're setting graphical parameter vectors like mar.

The first thing you might want to change on an axis is where the tick marks are drawn. By default, R uses the built-in function to pretty a "neat" sequence of values for the scale of each axis, but you can set your own by passing the at argument to axis. The following lines create the plot on the left of Figure 23-10.

```
R hpseq <- seq(min(hp),max(hp),length=10)
R plot(hp,mpg,cex=wt, xaxt="n",bty="n",ann=FALSE)
R axis(side=1,at=hpseq)
R axis(side=3,at=round(hpseq))
```

First, an evenly spaced sequence of 10 values spanning the range of hp is stored as hseq. The initial call to plot suppresses the x-axis, the box, and any default axis labels; however, the y-axis is permitted to appear as per default. Then axis is instructed to draw the x-axis(side=1), with tick marks at hseq. To provide a comparison to that, an axis is also drawn along the top (side=3), but this the tick marks are drawn at hseq after it's rounded to the nearest integer.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_628_0.png)

Figure 23-10: Customizing axes of the mtcars scatter

As you can see on the left of the figure, the custom x-axis I've created at the bottom shows 10 tick marks at the sequence of values supplied to. R may suppress some of the labels so they don't overlap one another, which is what has occurred. Since these "decimal" values might't aesthetically pleasing, the axis that's been drawn along the top has tick marks drawn at the nearest integers of hseq, achieved using round in the final call to axis earlier. Although, strictly speaking, this means that the tick marks are no longer evenly spaced, the rounded values mean shorter default axis labels that can all be displayed in the current device.

You can see from these difficulties that tick mark locations are generally best to R, unless you have specific axis values that you know you want marked out—you'll see some tweaks you can make to your axes. In particular, the tcl (length of the ticks), las (orientation of the labels), and mgp (axis spacing) parameters are arguably among those more frequently used. The following code creates the plot on the right of Figure 23-10.

```
> R hseq <- seq(0,325,by=25)
R> plot(hp,mpg,cex=wt, axes=FALSE)
R> box(bty="l")
> R axis(side=1,tcl=-2,las=1,mgp=c(3,2.5,0))
R> axis(side=1,at=hseq,tcl=1.5,mgp=c(3.1,5,1))
```

After a new sequence—hpseq2—is defined as all integers that lie within the recorded range of the data and are evenly spaced by 25 units, the plot is initialized. The box and axes are suppressed, but the default variables (mpg and hp) allow the axes to remain.

Now, an L-shaped box and the y-axis (side=2) are added. In the latter, the tcl parameter governs the length of each tick mark in “parallel lines of text” which is a standard unit measurement for margin spacing in R plot); it defaults to -0.5. When the value is negative, it draws the marks away from the plot region; when it’s positive, the tick marks are drawn inward. For side=2, tcl=2, meaning that the ticks will point out from the plot but be four times the length they usually are (two lines of text as opposed to half a line).

The las parameter controls the labels for each tick mark and oriented; setting to 1 instructs R to produce all labels regardless of axis. The default, las=0, writes all labels parallel to the corresponding axes; the alternative las=2 means all labels are perpendicular to the corresponding axes; and using las=3 allows all labels to be read vertically, regardless of axis.

Next up, the mpg parameter controls further aspects of axis spacing and, as such, supplies a vector of length 3 as per the following definition:(axis title, axis labels, axis line). Once, these arguments are expressed in “lines of text”. The default value of mpg is c(3,1,0)—meaning that in every axis you’ve seen so far, the title has three lines of text away from the plot region, the tick marks labels one line of text away, and the axis line includes zero lines of text away from the plot region (so it’s flush with any drawn plot region box). When used in axis, only the second and third elements of mpg are relevant. In the vertical axis of the plot on the right of Figure 23-10, the only alteration from the default was to set the axis labels to the left away from the plot region. The tick marks themselves are inadvertently labeled by tcl, so this is required to avoid the tick labels going through those ticks. By retrying the image and axis, but without specifying mpg, you will see that unpleasant result.

Moving to the x-axis (side=1), you can see tick marks at hpseq placed via at. This time, a positive value has been supplied to tcl, instructing the axis to have inward-facing tick marks of 1.5 lines of text in length. In mpg, note that the third element of the vector is now set to 1, meaning you want the axis line itself to sit one line of text away from the plot region. Looking at the right of Figure 23-10, you can see that the entire axis has been moved downward, away from the plot region. To account for this in terms of the spacing of the tick mark labeling, the second element of mpg has been increased a little from its default, to be 1.5.
