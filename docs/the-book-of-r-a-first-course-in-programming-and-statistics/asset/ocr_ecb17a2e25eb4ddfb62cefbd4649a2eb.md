![](bbox=[0.268, 0.068, 0.873, 0.281])

**Figure 21-4:** Three models, polynomials of order 1, 2, and 3, fitted to the "mileage displacement" relationship from the mtcars data set. Left: Visible plot limits constrained to the data. Right: Visible plot limits widened to illustrate unreliability in extrapolation.

It's a little more difficult to add the line corresponding to either of the polynomial-tiered models alone equipped to handle only straight-line trends. One way to do this is to make use of predict for each value in a sequence that represents the desired values of the explanatory variable. (I favor this approach because it allows you to simultaneously calculate confidence and prediction bands if you want.) To add the line for the order 2 model only, first create the required observed range of disp.

```
R disp.seq <- seq(min(mtcars$disp)-50,max(mtcars$disp)+50,length=30)
```

Here, the sequence has been widened by minus and plus 50 to predict a small amount on either side of the scope of the original covariate data, so the curve meets the edges of the graph. Then you make the prediction itself and superimpose the fitted line.

```
R car.order2.pred <- predict(car.order2,newdata=data.frame(disp=disp.seq))
R lines(disp.seq,car.order2.pred,lty=2)
```

You use the same technique, followed by the final addition of the legend, for order 3 model.

```
R car.order3.pred <- predict(car.order3,newdata=data.frame(disp=disp.seq))
R lines(disp.seq,car.order3.pred,lty=3)
R legend("topright","order 1 (linear)\
```

The result of this is on the left panel of Figure 21-4. When you've read data from only one covariate, disp, the example illustrated is considered multiple regression more than one