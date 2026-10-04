R> myplot <- qplot(foo,bar,geom="blank") + geom_line(color="red",linetype=2)
R> myplot + geom_point(size=3,shape=3,color="blue")
R> myplot + geom_point(size=3,shape=7,color="blue")

The first line stores the original plot in myplot, and the next lines call myplot with different point shapes. The second and third lines produce the graphics on the left and right of Figure 7-10, respectively.

![](bbox=[0.238, 0.238, 0.873, 0.473])

Figure 7-10: Using the object-oriented nature of ggplot2 graphics to experiment with different point characters

There are a number of geometric modifiers that can be called using a function name beginning with geom in ggplot2. To obtain a list, simply ensure the package is loaded and ??"geom_" as a help search at the prompt.

# 7.4.3 Aesthetic Mapping with Geoms

Geoms also provide efficient, automated ways to apply different styles to subsets of a plot. If you split a data set into categories using a factor object, ggplot2 can automatically map particular styles to different categories. In ggplot2's documentation, the factor is called a *variable*, which ggplot2 can map to aesthetic values. This gets rid of much of the effort that goes into isolating subsets of data and plotting them separately using base R (as you did in Section 7.3).

All this is best illustrated with an example. Let's return to the 20 observations you manually plotted, step-by-step, to produce the elaborate plot in Figure 7-6.

```
R> x <- 120
R> y <- (-1.49,3.37,2.59,-2.78,-3.94,-0.92,6.43,8.51,3.41,-8.23,
12.01,-6.58,2.87,14.12,9.63,-4.58,-14.78,-11.67,1.17,15.62)
```