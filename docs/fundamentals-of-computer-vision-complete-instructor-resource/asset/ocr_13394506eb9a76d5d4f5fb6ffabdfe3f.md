![](bbox=[0.105, 0.115, 0.875, 0.325])

Figure 5.21 Results of applying the non-center-weighted operators of Eq. 5.42 to estimate \(\partial f / \partial x\) (in red) and \(\partial f / \partial y\) (in blue). The horizontal axis is the angle of the edge. The scale of the vertical axis is unimportant because the purpose of the experiment is to illustrate how poorly quantized the edge detectors are. LEFT: the two operators applied to perfect step edges. RIGHT: the two operators applied to blurred edges.

can be differentiated, creating

```
\(\frac{\partial h(x, y)}{\partial x} = \frac{-x}{2\pi\sigma^4} \exp \left( - \frac{x^2 + y^2}{2\sigma^2} \right)\) (5.44)
```

for an isotropic covariance.

The derivative of a Gaussian (DoG) convolution kernels can be derived from the above equations by simply using the result of Eq. 5.44.

In Figure 5.22, the effect of scale, \(\sigma\), is illustrated. As scale increases, the response of the operator to variations in orientation becomes increasingly smooth. This would suggest that the ability of the operator to determine orientation likewise depends on scale. That is true, but the scale of the features in the image must also be considered. This will be discussed in more detail in Chapter 11.

# The Gabor Filter

Figure 5.23 illustrates the vertical edge detector, \(\frac{\partial f}{\partial x}\), estimated using the Gabor operator. Similarity with the derivative of a Gaussian is observed when applied to the same set of edges with the same scale. However, the differences are significant – the response is not nearly as smooth. This would likely cause the Gabor to be less useful as an estimator of orientation.

# 5.8.2 Estimating Orientation

In this section, the ability of these operators to determine orientation is evaluated using the following algorithm, still applied to perfect and blurred step edges, respectively.

+   1. Apply a vertical and a horizontal version of the operator to each edge image, producing a set of estimates of gradients.
+   2. Using these estimates, apply Eq. 5.34 to estimate the orientation of the edge.
+   3. Plot the estimated angle vs. the actual angle of the edge.