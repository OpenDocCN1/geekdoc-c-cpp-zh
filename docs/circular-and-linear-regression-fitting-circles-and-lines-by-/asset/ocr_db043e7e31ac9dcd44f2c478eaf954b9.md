| | Pratt | Taubin | Geometric | Hyper | Consistent |
|---|---|---|---|---|---|
| n = 20 | 5.6301 | 5.4945 | 5.4540 | 5.4555 | 5.4566 |
| n = 100 | 1.5164 | 1.3451 | 1.2952 | 1.2892 | 1.2895 |
| n = 1,000 | 0.3750 | 0.1947 | 0.1483 | 0.1341 | 0.1341 |
| n = 10,000 | 0.2557 | 0.0745 | 0.0286 | 0.0135 | 0.0134 |
| n = 50,000 | 0.2450 | 0.0637 | 0.0180 | 0.00272 | 0.00270 |

> Table 7.3 Mean squared error for five circle fits (10\u00b9\u2074 \u00d7values are shown). In this test n points are placed (equally spaced) along a semicircle of radius R = 1 and the noise level is \u03c3 = 0.05.

The results are summarized in Table 7.3. It shows the mean squared error (MSE) of the radius estimate \u0134 for each circle fit (obtained by averaging over 10\u2076 randomly generated samples). We see that for small samples, n < 100, all the circle fits perform nearly equally well. For larger samples, they have very different characteristics. The MSE of the Pratt fit is the biggest, due to its highest essential bias; see Section 7.6. The MSE of the Taubin fit is about 4 times smaller, again because its essential bias is half of that of Pratt (Section 7.6). The MSE of the geometric fit is about 4 times smaller than that of Taubin, again in perfect agreement with our theoretical analysis of Section 7.1.

The Hyper fit introduced in Section 7.5 has zero essential bias, hence its MSE becomes very small for very large samples; its mean error is several times smaller than that of the geometric fit! However, the Hyper fit is inconsistent, in view of our early analysis, hence its MSE does not completely vanish as n \u2192 \u221e.

Lastly, the Consistent fit included in Table 7.3 is the one computed by (7.77), which is nothing but our implementation of the two (theoretically identical) estimators: the Kukush\u2013Markovsky\u2013van Huffel (KMvH) method from Section 7.10 and the second order renormalization method of Kanatani from this section. We see that the Consistent circle fit becomes the most efficient for very large samples (n > 1,000).

In image processing applications, the sample size n typically ranges from 10 to 20 to several hundreds. It is not normal to have n > 1,000 data points, although occasionaly digitized images of circular arcs consist of thousands of points (pixels), see below.

For example, in an archaeological research by Chernov and Sapirstein [44], circular arcs appear as fragments of wheelmade and molded circular architectural terracottas whose original diameters are unknown and need be determined. Using a profile gauge, the profiles are transferred to graph paper,