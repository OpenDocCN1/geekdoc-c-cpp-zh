
+   b. Now, open a new graphics device of 8 × 7 inches. Set the figure margins to be two, five, three, and five lines on the bottom, top, and right, respectively. Also allow one line of outer margin space on each side other than the bottom, which should get two lines of outer margin.

+   i. Produce a scatterplot of diamond price on the vertical axis and carat weight on the horizontal axis. Use the colors red, green, and blue to distinguish the points according to certification. Suppress all axes, boxes, labels, and titles in the initial plot, then add a U-shaped box.

+   ii. Add the horizontal axis. Use place marks at an evenly spaced sequence of carat values from 0.2 and 1.1, in steps of 0.1. Use a bold, italic, sans-style font for the labels and add the labels to be only half a line from the axis. Then add smaller, outward-facing tick marks between the existing ones. To do this, make a second call to the axis function and place the ticks at a sequence of values from 0.15 to 1.05 in steps of 0.1. Set these secondary tick marks to have a length of one-quarter of a line and suppress the axes.

+   iii. Add the vertical axes. On the left, ticks should appear at SGD$1000–17000. Labels should be horizontally readable and in the same font style as the horizontal axis. On the right, axis ticks should be made in the equivalent of US dollars (USD$) in the sequence SGD$1000–11000 in steps of SGD$100 and should be labeled as such. To do this, use the conversion USD = 1.37 × SGD$. Label orientation and font should match the other axes.

+   iv. Fit a linear model of price on a quadratic polynomial of carat weight for the data. Provide a prediction of the model for a sequence of carat values spanning the range of the observed values; include estimation of a 95 percent prediction interval. Use this information to superimpose a gray solid line for the fitted values and gray dashed lines for the prediction interval upon the scatterplot.

+   v. Set expression objects for labeling the approximate US dollar conversion and the regression equation. Name the conversion expr1; it should look like USD ≈ 1.37 × SGD$. The regression equation should look similar to Price = $\beta_0 + \beta_1Carat + \beta_2Carat^2$, name it expr2.

+   vi. Use mtext to add an appropriate name and titles for three individual axes. You may need to experiment with a little line depth for each one, as well as whether to write in

the outer margin or the figure margin, depending on your own spacing preference. The rightmost axis title should make use of expr1.
vii. Either via trial and error to find appropriate coordinates or by using the interactive.arrow function from Exercise 23.1, place an arrow pointing to the fitted polynomial line and label it with expr2.
viii. Finally, use a locator to place a legend in any appropriate location, referencing the color of the points according to the appropriate certification.

My version of the plot looks like this:

![](img/b2cfc85cbb129f60fe595a2bae074fe4_641_0.png)

## Important Code in This Chapter

| Function/operator | Brief description | First occurrence |
|---|---|---|
| dev.new | Open new graphics device | Section 23.1.1, p. 576 |
| dev.set | Change active device | Section 23.1.2, p. 577 |
| dev.off | Close device | Section 23.1.3, p. 578 |
| par | Set graphical parameters | Section 23.1.4, p. 579 |
| layout | Open new graphics device | Section 23.1.4, p. 580 |
| box | Add box to plot | Section 23.2.1, p. 583 |
| mtext | Write text in margins | Section 23.2.2, p. 584 |
| locator | Interpolate coordinates | Section 23.3.1, p. 587 |
| axis | Add axis to plot | Section 23.4.3, p. 594 |
| expression | Render Greek/math in plot | Section 23.5.2, p. 598 |
| title | Add main/axis titles | Section 23.5.2, p. 598 |
| italic | Italicize text | Section 23.5.3, p. 600 |
| grid | Add grid to plot | Section 23.6, p. 605 |

# 24

# GOING FURTHER WITH THE
GRAMMAR OF GRAPHICS

![](img/b2cfc85cbb129f60fe595a2bae074fe4_642_0.png)

You covered the basics of the ggplot2 package—which offers an alternative to traditional R graphics—in Section 7.4 and throughout Chapter 14. In this chapter, you'll look at a couple of this package's more popular and useful features, as well as its relatively young cousin, ggvis, which provides an interactive, browser-based experience.

## 24.1 ggplot or qplot?

So far when creating the relatively simple ggplot graphics, you've used the qplot function to initialize the visual object. In fact, the more general ggplot command is the core function of ggplot2. There are several key differences between these two initialization functions:

- qplot is a shortcut version of ggplot; it's used if you just want a quick look at your data or if you're working directly in the R console.

- qplot is designed to be reminiscent of the base R plot function—pass it x and y-coordinate vectors and tell it what to do. By contrast, ggplot prefers its data as a data frame object, and tell you what to do by explicitly adding geom layers.

- A call to qplot alone can produce a graphic. When using ggplot, layers have to be added before anything visible.

- To access the full power and flexibility of ggplot2 graphics, ggplot is the recommended function; this comes at the cost of providing a little more instruction than qplot requires.

All in all, you can create plots using either qplot or ggplot. Many users make the decision based on the form their data are (in other words, a data frame or as separate vectors in the global environment) and whether they wanted polished visuals (for example, for publication purposes) or just a quick look at the data while working directly in the console.

As a quick example of the syntax, flip back to the code page 297 used to create the histogram on the right of Figure 14-5. You could argue that the numerous modifications made to that particular plot warrant a more compartmentalized approach over qplot. Load ggplot2 and create the following three:

```
R> gg.static <- ggplot(mtcars, aes(x=hp)) + 
ggtitle("Horsepower") + labs(x="HP")
R> mtcars.mm <- data.frame(mm=mean(mtcars$hp),median(mtcars$hp),
  stats=factor(c("mean", "median")))
R> gg.lines <- geom_vline(mapping=aes(xintercept=mm, linetype=stats),
  show.legend=TRUE,data=mtcars.mm)
```

The first object, gg.static, represents the part of the plot that will stay the same throughout, if you wanted to experiment with adding other features later. Note that the call to ggplot differs from qplot in that the first argument is the entire data frame of interest, allowing access to all data columns within the frame for any subsequent geoms or annotations. Then you add the ggtitle and labels to set the main and horizontal axis title. The second object, mtcars.mm, stores the horsepower mean and median as a "dummy" data frame. The mean and median lines are then superimposed on the histogram by the third object, which is single call to the geom_vline function with the same content used in the earlier code, albeit in a slightly modified form to stay true to the initial use of ggplot.

Nothing is displayed until you make a call that prints the ggplot2 object (as noted in Section 7.4). The following call reproduces the image on the right of Figure 14-5:

```
R> gg.static <- geom_histogram(color="black",fill="white") + 
breaks=seq(0,400,25),closed="right") + gg.lines + 
scale_linetype_manual(values=c(2,3)) + labs(linetype="")
```

The pieces are put together in much the same way for the creation of Figure 14-5: the addition of the geom_histogram layer to gg_static invokes the plot, and the addition of gg_lines line types made with scale_linetype_manual off the mean and median. If you wanted to produce the histogram without these lines, you would simply print the gg_static object plot_histogram.

As you get experienced with ggplot2, you'll find yourself leaning either ggplot or dplyr, depending on the application. The help file in ?ggplot provides a good description of the typical types ggplot uses and how it stacks up against ?plot. For further information, refer to ggplot2: Elegant Graphics for Data Analysis by Wickham (2009). I'll use ggplot for the rest of the plots in this chapter to provide some examples of the syntax of the ggplot to compare with the earlier uses of ggplot.

## 24.2 Smoothing and Shading

Data visualization using ggplot2 package is particularly when you want to split features of the plot by one or more categorical variables. This is especially apparent when you're enhancing your plot with features that are more difficult to achieve using R commands.

### 24.2.1 Adding LOESS Trends

When you're looking at raw data, it's sometimes difficult to get an overall impression of trends without fitting a parametric model (for example, via linear regression), which means making assumptions about the nature of these trends. This is where nonparametric smoothing comes in—you can use certain methods to determine how your data appear to behave without fitting a specific model. These methods are a flexible aid for interpreting all trends, whatever their form, the trade-off is that you're not provided with specific numeric details of the relationships between response and predictors (since you're not estimating any coefficients such as outliers and intercepts) and you lose any reliable ability to extrapolate.

Locally weighted scatter smoothing (LOESS or LOWESS) is a nonparametric smoothing technique that produces the trend by regression methods on localized subsets of the data, step-by-step over the entire range of the explanatory variable.

> For theoretical details, Chapter 6 of Applied Nonparametric Regression (Härle, 1990), as well as Chapters 2 and 3 of Introduction to Nonparametric Regression (Takazawa, 2006), provide clear discussions of LOESS methods.

For an illustration, load the MASS package and return your attention to the survey data frame. First, create a new data frame or return with any missing values deleted to avoid warning messages:

```
R> surv <- na.omit(survey[,c("Sex", "Wr.Hnd", "Height")])
```
