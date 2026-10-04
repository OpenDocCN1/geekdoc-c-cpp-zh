```
R wt.seq <- seq(mtcars$wt),max(mtcars$wt),length=len
R hp.wt <- expand.grid(hp=hp.seq,wt=wt.seq)
R nrow(hp.wt)
[1] 400
R hp.wt[1:5,]
     hp    wt
1 52.00000 1.513
2 66.89474 1.513
3 81.78947 1.513
4 96.68421 1.513
5 111.57895 1.513
```

First, this code sets up evenly spaced sequences (each of 20, spanning the range of the observed data) in both hp and wt—these are your x-20 x 20 = 400 unique coordinates at which you will be evaluating the fitted model; these coordinates are obtained using expand.grid in Section 25.3.

Next, you can use predict to get the 400 corresponding mean MPG (z) values; it's already a data frame in the required format, hp.wt can be passed directly to the newdata argument.

```
R car.pred <- predict(car.fit,newdata=hp.wt)
```

Then, you simply need to arrange the resulting vector as the appropriate 20 × 20 z-matrix.

```
R car.pred.mat <- matrix(car.pred,nrow=len,ncol=len)
```

Finally, you plot the result as contours, as shown in Figure 25-11.

```
R contour(x=hp.seq,y=wt.seq,z=car.pred.mat,levels=32,8,lty=2,lwd=1.5,xaxs="i",yaxis="i",xlab="Horsepower",ylab="Weight",main="MPG model")
```

In this case, you can see the use of the optional argument. Rather than R automatically decide at which values of z to show contours, you can supply a numeric vector to this argument with the specific levels to draw the lines. This numeric value must be on the same scale as the resulting bivariate function of interest; here, I asked for contours at all integer levels from 32 through 8. I also employ familylty and lwd to control the appearance of the contours themselves, which are set here as dashed and slightly thicker than usual.

Furthermore, for contour plots in particular, you'll want to deviate from the default axis limit style, the small amount of additional "padding" space that's included in the default plot region (refer to Section 23.4.1) can be prominent—take another look at the volcano contour plot in Figure 25-10. As previously shown, setting xaxs and yaxs to "i" restricts all plotting to the exact limits imposed by x and y.