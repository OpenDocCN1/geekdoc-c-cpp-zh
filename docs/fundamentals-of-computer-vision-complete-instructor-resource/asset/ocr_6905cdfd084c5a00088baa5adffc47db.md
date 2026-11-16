![](bbox=[0.09, 0.12, 0.89, 0.34])

Figure 5.24 Estimate of edge orientation vs. actual orientation for 3 x 1 kernels used to estimate vertical and horizontal partial derivatives. The true edge orientation is in blue, and the estimated is in red. The left figure is the result for ideal edges and the right figure is that for blurred edges.

# Simple 1 x 3 Filters

Figure 5.24 graphs the actual angle vs. the estimate, using 1 x 3 operators to estimate the directional derivatives. Clearly, the 1 x 3 operators are not useful for this application, at least not for perfect edges. As we have seen before, the slight blur spreads the information out and allows more accurate edge estimations.

# Sobel Kernels

Figure 5.25 illustrates the accuracy resulting from derivative estimates using the Sobel operators shown previously, combined with Eq. 5.34. Here, a substantial improvement in accuracy is observed over the 1 x 3, but it is still not particularly good.

![](bbox=[0.09, 0.64, 0.89, 0.86])

Figure 5.25 Using the two 3 x 3 Sobel kernels to estimate the angle produces somewhat better estimates, but still not very good. The edge used to produce the results in the left image was an ideal step edge, in the right image, a blurred step edge.