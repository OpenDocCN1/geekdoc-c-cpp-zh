![](bbox=[0.22, 0.11, 0.58, 0.37])

Figure 5.13 In a stack scale space, the original image is at the bottom, and each higher level is increasingly blurred, using a Gaussian blur with scale of \(\sigma\).

# ## 5.6.2 Scale Space without Resampling

In a modern (stacked) scale space representation the concept that each level is a blurring of the previous level is preserved, but no subsampling is done – each level is the same size as the previous level, but more blurred. Clearly, at high levels of scale, i.e., \(\sigma\) is large, only the largest features are visible. This is illustrated in Figure 5.13.

Here is a gedankenexperiment for you: Take an image, blur it with a Gaussian kernel of standard deviation 1.

```
\(f(x, y, 1) = G(x, y, 1) \circledast f(x, y)\)
```

where

```
\(G(x, y, \sigma) = \frac{1}{2\pi\sigma^2} e^{-\frac{x^2+y^2}{2\sigma^2}}\)
```

This operation produces a new image. Call that image 1. Now, blur the original image with a Gaussian kernel of standard deviation 2. Call that image 2. Continue until you have a set of images that you can think of as stacked, and the “top” image is almost blurred away. We say the top image is a representation of the image at “large scale”. This stack of images is referred to as a scale-space representation. Clearly, since we are not required to use only integer values of the standard deviation, we can create scale space representations with as much resolution in scale as desired. The essential premise of scale space representations is that certain features can be tracked over scale, and how those features vary with scale tells something about the image.

A scale space has been formally defined [5.22, 5.23] as having the following properties:

+   - All signals should be defined on the same domain (no pyramids).
+   - Increasing values of the scale parameter should produce coarser representations.