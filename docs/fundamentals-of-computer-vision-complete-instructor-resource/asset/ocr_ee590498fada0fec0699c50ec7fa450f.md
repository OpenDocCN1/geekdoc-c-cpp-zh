![](bbox=[0.186, 0.116, 0.746, 0.416])

Figure 10.18 A fish contour from the SQUID data base [10.1, 10.25] and the corresponding CSS image. The vertical axis in the right-hand image is scale.

The figure on the right of Figure 10.18 illustrates a curvature scale space with two high peaks, marked by letters. The horizontal axis, s, represents arc length between zero and one as the curve is traversed. The vertical axis is scale. The peak marked with B indicates that somewhere near the end of the contour the curvature changes sign with a high scale.

The curvature scale space matching algorithm is described in detail in [10.25] [10.1]. Every curve in their database is represented as a set {(s, \(\sigma\))} of pairs, each denoting the arc length and scale of a maximum\(^8\) in the CSS image. The matching process involves finding correspondences between the maxima of the two contours. We will refer to the two images as the target and the model.

Let \(M_{target} = ((t_1, \gamma_1), (t_2, \gamma_2), \dots, (t_L, \gamma_L))\) be the maxima of the target, parametrized by arc length t and arranged in descending order of scale \(\gamma\). Similarly, let \(M_{model} = ((s_1, \sigma_1), (s_2, \sigma_2), \dots, (s_N, \sigma_N))\) be the maxima of the model, parametrized by arc length s and arranged in descending order of scale \(\sigma\). The matching algorithm is as follows:

+   1. The highest maximum in the target and the model CSS image are used to find the CSS shift parameter.

```
\(\alpha = s_1 - t_1\) (10.68)
```

This will compensate for any changes in the starting point and orientation of the contour. Two lists are initialized: one with the maximum pair \((t_1, \gamma_1)\) from the target and the other with the maximum pair \((s_1, \sigma_1)\) from the model. The cost for the match is initialized as:

```
\(MC = |\sigma_1 - \gamma_1|\) (10.69)
```

\(^8\) Here, maxima means the point of highest scale.