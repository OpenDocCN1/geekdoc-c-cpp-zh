
For your reference, my result is given here.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_712_0.png)

## 25.6 Perspective Plots

The last kind of plot you will look at in this chapter is the *perspective plot*, sometimes also referred to as a *wireframe*. Unlike contour plots and pixel images, where fluctuations in the surface are emphasized with line patterns and/or colors, a perspective plot uses a physical third dimension against which the z value is plotted.

### 25.6.1 Basic Plots and Angle Adjustment

Perspective plots are especially useful when you want to emphasize the fluctuating nature of the values populating your z-matrix. For example, in some applications you might want to get a good impression of the relative extremity of any peaks and/or troughs in the plotted surface, which is harder to do in, for example, a pixel image or contour plot.

Recall the mtcars response surface plotted as contours and as pixel images in Sections 25.4.1 and 25.5.1. You created a 20 x 20 evaluation grid in the horsepower and weight variables, as well as a corresponding z-matrix of 400 giving the predicted mean result MPG:

```r
R car.fit <- lm(mpg+hp+wt,data=mtcars)
R len <- 20
R hp.seq <- seq(min(mtcars$hp),max(mtcars$hp),length=len)
R wt.seq <- seq(min(mtcars$wt),max(mtcars$wt),length=len)
R hp.wt <- expand.grid(hp=hp.seq,wt=wt.seq,newdata=hp.wt,nrow=len,ncol=len)
R car.pred.mat <- matrix(predict(car.fit,hp.wt))
```

The built-in R function persp is used to create perspective plots. Its basic usage is the same as contour, filled.contour, and image. Your increasing sequences in the x and y-axis directions, which define the evaluation grid, are passed to x and y, with your corresponding z-matrix passed to z. Bring up the default appearance for the 20 x20 mtcars surface with the following:

```r
persp(x=hp.seq,y=wt.seq,z=car.pred.mat)
```

This appears in the top left of Figure 25-19.

Interpreting the perspective plot is straightforward. The default viewing angle shows the x-axis in the foreground, increasing from left to right, and the y-axis on the left, increasing from the foreground to deeper in the background. In this way, the evaluation grid lies flat along which your surface is plotted from the bottom vertically to the top.

The viewing angle is one of the most important aspects of such a plot. In persp, you can control it with the two options theta, which spins the plot horizontally, and phi, which adjusts the vertical viewing position. Both are specified in degrees; theta defaults to 0, and phi defaults to 15 to give a slightly elevated viewing position so you can see the y-axis extending foreground to background. In general, you can think of the possible value of theta as anywhere from 0 to 360, representing a complete rotation all around the plot, and the possible value of phi as anywhere from 90 to -90, the range of which you moves from a bird's-eye view directly from the top looking down to a submarine view directly from the top up.

The second example demonstrates this behavior:

```r
persp(x=hp.seq,y=wt.seq,z=car.pred.mat,theta=30,phi=23,
xlab="Horsepower",ylab="Weight",zlab="mean MPG")
```

In fact, this line of code that originally produced the rightmost image in Figure 25-19 on page 92 (when you were introduced to the concept of an interactive term between two continuous predictors in a linear regression model). The graphic is reproduced in the top right of Figure 25-19. The axes are titled up using xlabel and ylab, with zlab used to control the title for the third vertical axis. The use of theta and phi in this has elevated the viewing position slightly more than the default and rotated the plot so that the origin (in other words, the lower vertex denoting the lower limit of the x-y plane) is prominent in the foreground. It's worth noting that increasing theta from 0 rotates the plot in a clockwise fashion, but you could also supply a negative value to rotate the plot in the other direction. Setting theta=-30, as shown here, has the same effect as theta=30.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_712_0.png)
