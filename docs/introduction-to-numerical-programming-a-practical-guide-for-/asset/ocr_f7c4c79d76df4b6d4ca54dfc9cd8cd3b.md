![](bbox=[0.25, 0.13, 0.75, 0.35])

FIGURE 9.4 Case in which the natural cubic spline deviates significantly from the modeled function due to insufficient interpolated points. The interpolated data samples the function f(x) = 1/x^12 − 10^4/x^6.

![](bbox=[0.15, 0.48, 0.85, 0.7])

FIGURE 9.5 Interpolation with natural cubic splines (left) and clamped cubic splines (right). The modeled dependence, f(x) = sin x / x, is sampled in the interval [0, 5π/2] with a π/2 spacing.

the true behavior of the modeled function. Quite in contrast, clamped boundaries clearly improve the matching between the interpolant and the modeled dependence (see the right panel of Figure 9.5).

# 9.5 Linear Regression

In quite a few practical situations, the plot of the observations or the theoretical framework on which the data collection is based suggests a linear functional dependence of the modeled function on the independent variable (see Figure 9.6):

F(x; a, b) = a x + b. (9.40)