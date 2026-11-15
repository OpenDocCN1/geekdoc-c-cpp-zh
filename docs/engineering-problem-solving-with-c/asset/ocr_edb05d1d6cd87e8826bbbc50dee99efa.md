# The best fit to a set of points computed by using linear regression

![](bbox=[0.22, 0.1, 0.88, 0.3])

# Figure 5.7 Least-squares linear regression model.

For the sample set of data, the optimum value for m is 20.83, and the optimum value for b is 3.76. The set of data points and this best-fit linear equation are shown in Figure 5.7. The sum of squares for this best fit is 356.82, compared with 573 for the straight line in Figure 5.6.

One of the advantages of performing a linear regression for a set of data points that is nearly linear in nature is that we can then estimate or predict points for which we had no data. For example, in the cylinder-head temperature example, suppose that we want to estimate the temperature for the cylinder head at 3.3 seconds. By using the equation computed with linear regression, we find that the estimated temperature is

```
y = mx + b
= (20.83)(3.3) + 3.76
= 72.5.
```

With an equation model, we can compute estimates that we could not compute with linear interpolation. For example, using the linear model, we can compute an estimate of the temperature for 8 seconds, but we could not compute an estimate at 8 seconds using linear interpolation, because we do not have a point with a time greater than 8 seconds. (This would be extrapolation, not interpolation.)

It is also important to remember that linear models do not provide a good fit to all sets of data. Therefore, it is important to first determine whether a linear model is a good model for the data before using it to predict new data points. Techniques for measuring the quality of a linear model for a set of data is presented in Chapter 6.

In the next section, we develop a problem section that determines the best fit for a set of sensor data collected from a satellite, and then we use that model to estimate or predict other sensor values.

# 5.7 Problem Solving Applied: Ozone Measurements

Satellite sensors can be used to measure many different pieces of information that help us understand more about the atmosphere, which is composed of a number of layers around the Earth [12]. Starting at the Earth’s surface, we know that the layers are the troposphere, stratosphere,