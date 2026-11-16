![](bbox=[0.25, 0.1, 0.72, 0.42])

# 9.3.2 Soft Thresholding

Soft thresholding is defined as

```
y = sgn(x)f(|x| - \sigma), \quad \text{for } |x| \ge \sigma
= 0, \quad \text{for } |x| < \sigma.
(9.6)
```

The function $f(x)$ is generally a linear function (a straight line with slope to be chosen; Figure 9.8). However, spline curves of the third or fourth order may be used to effectively weight the values greater than $\sigma$. In some signal compression applications, using a quadratic spline curves of order $m > 2$ may affect the compression ratio by a small amount.

FIGURE 9.8: Soft thresholding.