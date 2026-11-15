+   6. If dist is less than 50.0 and time is greater than 10.0, increment time by 2; otherwise, increment time by 2.5.
+   7. If dist is greater than or equal to 100.0, increment time by 2.0. If dist is between 50 and 100, increment time by 1. Otherwise, increment time by 0.5.

# 3.5 Numerical Technique: Linear Interpolation

The collection of data from an experiment or from observing a physical phenomenon is an important step in developing a problem solution. These data points can generally be considered to be coordinates of points of a function f(x). We would often like to use these data points to determine estimates of the function f(x) for values of x that were not part of the original set of data. For example, suppose that we have data points (a, f(a)) and (c, f(c)). If we want to estimate the value of f(b), where a < b < c, we can assume that a straight line joined f(a) and f(c) and then use linear interpolation to obtain the value of f(b). If we assume that the points f(a) and f(c) are joined by a cubic (third-degree) polynomial, we could use a cubic-spline interpolation method to obtain the value of f(b). Most interpolation problems can be solved using one of these two methods. Figure 3.6 contains a set of six data points

![](bbox=[0.26, 0.51, 0.85, 0.88])

Figure 3.6 Linear and cubic spline interpolation.