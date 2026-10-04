
# (1)

# (2)

![](img/b2cfc85cbb129f60fe595a2bae074fe4_169_0.png)

![](img/b2cfc85cbb129f60fe595a2bae074fe4_169_1.png)

# (3)

# (4)

![](img/b2cfc85cbb129f60fe595a2bae074fe4_169_2.png)

![](img/b2cfc85cbb129f60fe595a2bae074fe4_169_3.png)

# (5)

# (6)

![](img/b2cfc85cbb129f60fe595a2bae074fe4_169_4.png)

![](img/b2cfc85cbb129f60fe595a2bae074fe4_169_5.png)

# (7)

# (8)

![](img/b2cfc85cbb129f60fe595a2bae074fe4_169_6.png)

![](img/b2cfc85cbb129f60fe595a2bae074fe4_169_7.png)

# (9)

# (10)

![](img/b2cfc85cbb129f60fe595a2bae074fe4_169_8.png)

![](img/b2cfc85cbb129f60fe595a2bae074fe4_169_9.png)

Figure 7-7: Building the final plot given in Figure 7-6. The plots (1) through (10) correspond to the itemized lines of code in the text.

two lines red, dashed, and double-thickness. For vertical lines, you could have written v=c(-5,5), which would have drawn them at x = -5 and x = 5.

```
R abline(h=c(-5,5),col="red",lty=2,lwd=2)
```

+   3. The third line of code adds shorter vertical lines between the horizontal drawn in step 2 to form a box. For this use segments, not abline, since you don't want these lines to span the entire plotting region. The segments command takes a "from" coordinate (given as x0 and y0) and a "to" coordinate (as x1 and y1) and draws the corresponding line. The vector-oriented behavior of R matches up the sets of "from" and "to" coordinates. Both lines are red and dotted and have double-thickness. (You could also supply vectors of length 2 to these parameters, in which case the first segment would use the first parameter value and the second segment would use the second.)

```
R segments(x0=c(5,15),y0=c(-5,-5),x1=c(5,5),col="red",lty=3,lwd=2)
```

+   4. At step 4, you use points to begin adding specific coordinates from x and y to the plot. Just like plot, points takes two vectors of equal length with x and y. In this case, you want points plotted differently according to their location, so use logical vector subsetting (Section 4.1.5) to identify and extract elements of x and y where the y is greater than equal to 5. (and only these points) are added as purple x symbols and are enlarged by a factor of 2 cex.

```
R points(x[y>=5],y[y>=5],pch=4,col="magenta",cex=2)
```

+   5. The fifth line of code is like the fourth; this time it extracts the coordinates where y values are less than or equal to -5. A + point character is used, and you set the color to dark green.

```
R points(x[y<=-5],y[y<=-5],pch=3,col="darkgreen",cex=2)
```

+   6. The sixth step adds the blue "sweet spot" points, which are identified with (x>=5&x<15&y>-5&y<5). This slightly more complicated extracts points where x location between 5 and 15 (inclusive) AND y location between -5 and 5 (exclusive). Note that this line uses the "short" form of the logical operator & since you use element-wise comparisons here (see Section 4.1.3).

```
R points(x[(x>=5&x<15&y>-5&y<5)],y[(x>=5&x<15&y>-5&y<5)],pch=19,col="blue")
```

+   7. This next command identifies the remaining points in the data set (with x value that is less than 5 OR greater than 15 AND y value between -5 and 5). No graphical parameters are specified, so these points are plotted with the default black.

```
R points(x[(x<5|x>15)&(y>-5&y<5)],y[(x<5|x>15)&(y>-5&y<5)])
```

8. To draw lines connecting the coordinates in x and y, you use lines. Here you've also set lty to 4, which draws a dash-dot-dash style line.

```
R> lines(x,y,lty=4)
```

9. The ninth line of code adds the arrow pointing to the sweet spot. The function arrows is used just like segments, where you provide a "from" coordinate (x0, y0) and a "to" coordinate (x1, y1). By default, the head of the arrow is located at the "to" coordinate, (and other options such as the angle and length of the head) can be altered using optional arguments described in the help file?

```
R> arrows(x=8,y=14,lwd=1,y1=2.5)
```

10. The tenth line paints a label on the plot at the top of the arrow. As per the default behavior of text, string supplied as labels is centered on the coordinates provided with the arguments x and y.

```
R> text(x=8,y=15,labels="sweet spot")
```

As a finishing touch, you can add the label with the legend, which gives you the final product in Figure 7-6.

```
legend("bottomleft"
```

The first argument where the legend should be placed. There are various ways to do this (including setting x- and y-coordinates), but it often suffices to pick a corner using one of the four following character strings: "topleft","topright","bottomleft" or "bottomright". You supply the labels as a vector of character strings to the legend. Then you need to supply the remaining argument values in vectors of the same length so that the right elements match up with each label.

For example, for the first label ("overall process"), you want a line of type 4 with thickness and Color. In the first positions of the remaining argument values, you set pt.cex=NA,lty=4,col="black",lwd=1, and pt.cex=NA (all of these are default values, except for lty). Here cex refers to the cex parameter when calling points (using just cex in legend would expand the text, not).

Note that you have to fill in some elements in these vectors with NA when you don't want to set the corresponding graphical parameter. This is just to preserve the equal lengths of the vectors so R can track that parameter values correspond to each particular reference. As you work through this book, you'll see plenty more examples using legend.

## Exercise 7.1

a. As closely as you can, re-create the following plot:

![](img/b2cfc85cbb129f60fe595a2bae074fe4_172_0.png)

b. With the following data, create a plot on the x-axis and height on the y-axis. Use different point characters or colors to distinguish between males and females and provide a matching legend. Label the axes and the guide to a plot title.

| Weight (kg) | Height (cm) | Sex |
|---|---|---|
| 55 | 161 | female |
| 85 | 185 | male |
| 75 | 174 | male |
| 42 | 154 | female |
| 93 | 188 | male |
| 63 | 178 | male |
| 58 | 170 | female |
| 75 | 167 | male |
| 89 | 181 | male |
| 67 | 178 | female |

## 7.4 The ggplot2 Package

This chapter so far has shown R's built-in graphical tools (often called R graphics or traditional R graphics). Now, let's look at another important suite of graphical tools: ggplot2, a prominent package by Hadley Wickham (2009). Available on CRAN like any other contributed package, ggplot2 offers powerful alternatives to the standard plotting procedures in R. The gg stands for grammar of graphics approach to graphical production described by Wilkinson (2005). In following this approach, ggplot2 standardizes the production of different plot and graph types, streamlines some of the more fiddly aspects of adding to plots (such as including a legend), and lets you build plots by defining and manipulating layers. For the moment, let's see the elementary behavior of ggplot2

using the same simple examples in Sections 7.1–7. You'll get familiar with the basic plotting function aplot and how it differs from the generic plot used earlier. I'll return to the topic of ggplot2 when I cover statistical plots in Chapter 14, and you'll investigate even more advanced abilities in Chapter 24.

### 7.4.1 A Quick Plot with aplot

First, you must install the ggplot2 package by downloading it manually or simply entering install.packages("ggplot2") at the prompt (see Section A.2.3). Then, load the package with the following:

```
R library("ggplot2")
```

Now, let's go back to the five data points originally stored in Section 7.1 as foo and bar.

```
R foo <- c(1,1,2,3,5,3.9,4,2)
R bar <- c(2,2,-1.3,0,0.2,)
```

You can produce ggplot2's version of Figure 7-1 using its "quick plot" function aplot.

```
R aplot(foo,bar)
```

The result is shown in the left image of Figure 7-8. There are some obvious differences between this image and the one produced using plot, but the basic syntax of aplot is the same as earlier. The first two arguments passed to aplot are vectors of equal length, with the x-coordinates in foo supplied first, followed by the y-coordinates in bar.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_173_0.png)

Figure 7-8: Five plotted points using ggplot2's default behavior for the aplot function (left) and with title and axis labels added (right)
