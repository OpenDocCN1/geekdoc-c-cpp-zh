Look at the worst percent relative error values.

```
SRE := sort(RelErr);
SRE[1..2], SRE[-2.. -1];
[-57.46925000, -44.5707500], [67.25200000, 140.8770000]
```

```
plotplot(ResidualPts, symbol = soliddiamond, symbolsize = 16,
    title = "Residuals");
```

![](bbox=[0.293, 0.219, 0.714, 0.508])

We’ve obtained the model, $y = f(t) = 49.4601 - 0.75251t$. The sum of squared error is 451.1945, the correlation is −0.94, and $R^2$, the coefficient of determination which is the correlation coefficient squared, is 0.886. These are all indicators of a “good” linear model.

But...

Although some percent relative errors are small, others are quite large, with eight of the fifteen over 20%. The largest two positive errors are ≈ 67% and 140%, and the largest two negative errors are ≈ −45% and −57%. How much confidence would you have in making predictions with this model? The residual plot clearly shows a curved pattern. The residuals and percent relative errors show that we do not have an adequate model. Advanced courses in statistical regression will show how to attempt to correct this inadequacy.

Further, suppose we need to predict the index when time was 100 days.

```
RI(100);
−28.790400
```

A negative value is clearly unacceptable and makes no sense in the context of our problem since the index is always positive. This model does not pass the common sense test.

With a strong correlation of −0.94, what went wrong? The residual plot diagnostic shows a curved pattern. In many regression analysis books, the