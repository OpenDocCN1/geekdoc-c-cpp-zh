The curvature of such a curve is given by:

```
\(\kappa(s) = \frac{(\dot{x}(s)\ddot{y}(s) - \dot{x}(s)\ddot{y}(s))}{(\dot{x}(s)^2 + \dot{y}(s)^2)^{3/2}},\) (10.64)
```

where \(\dot{x}\) denotes \(\frac{\partial x}{\partial s}\).

The above contour can be successively blurred by convolving it with a 1D Gaussian kernel of width \(\sigma\), where the scale \(\sigma)\) is increased at each level of blurring. Let this blurred version of the contour be given by \(C : \mathbb{R} \times \mathbb{R} \rightarrow \mathbb{R} \times \mathbb{R}\).

```
\(C(s, \sigma) = x(s) * G_\sigma(s, \sigma), y(s) * G(s, \sigma).\) (10.65)
```

The first and second derivatives of the curve at each scale \(\sigma\) can be estimated as follows:

```
\(x_s(s, \sigma) = x(s) * G_s(s, \sigma)\)
\(y_s(s, \sigma) = y(s) * G_s(s, \sigma)\)
\(x_{ss}(s, \sigma) = x(s) * G_{ss}(s, \sigma)\)
\(y_{ss}(s, \sigma) = y(s) * G_{ss}(s, \sigma)\) (10.66)
```

where the subscript denotes partial differentiation.

The curvature at each scale \(\sigma\) can be found by making the dependence on scale explicit as:

```
\(\kappa(s, \sigma) = \frac{(x_s(s, \sigma)y_{ss}(s, \sigma) - x_{ss}(s, \sigma)y_s(s, \sigma))}{(x_s(s, \sigma)^2 + y_s(s, \sigma)^2)^{3/2}}.\) (10.67)
```

The curvature zero-crossings are the points on the contour where the curvature changes sign. The CSS representation computes the points of curvature zero-crossings at each scale and represents them in the \((s, \sigma)\) plane. This is shown in Figure 10.18 with arc length(s) along the horizontal axis and the scale (\(\sigma\)) along the vertical axis. This is called the CSS image. The contour of the fish was obtained from the SQUID base data.6 We implemented a version of CSS and applied it to obtain the right-hand figure.

The set of maxima of the CSS image is used as the shape signature for the given contour. Maxima with low scale values in the CSS image are related to the noise in the curve and are ignored. Following Mokhtarian [10.1], we assume anything below \(\frac{\sigma_{max}}{20}\) is considered to be noise and is not used in the matching process, where \(\sigma_{max}\) is the highest maximum in the CSS image.

CSS descriptors are translation-invariant because of the use of curvature. Scale invariance is obtained by resampling the curve to a fixed number7 of boundary points. Rotation and starting point changes cause circular shifts in the CSS image and are compensated for during the matching process, described later in this section.

# Matching Contours with Curvature Scale Space Matching

Earlier in this section the curvature scale space was defined. Here, we discuss the use of this representation in matching plane curves.

6 http://www.ee.surrey.ac.uk/CVSSP/demos/csas/demo.html.

7 We recommend resampling the contour to 200 points.