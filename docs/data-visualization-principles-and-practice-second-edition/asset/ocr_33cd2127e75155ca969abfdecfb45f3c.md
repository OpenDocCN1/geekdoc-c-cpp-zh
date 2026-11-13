![](bbox=[0.13, 0.12, 0.72, 0.46])

Figure 5.20. (a) Height plot. (b-d) Enriged height-plot variations for the same dataset.

rendered with standard Gouraud shading. Next, instead of the linear mapping \( z = sf \), we use a non-linear mapping given by

```
\( z(x, y) = sf(x, y) + sgh \left( \frac{f(x, y) \mod h}{h} \right) \) (5.7)
```

where \( g(u) = au(1-u) \) is a parabolic function. The resulting enrigged plot for a value of \( a = 0.6 \) is shown in Figure 5.20(b). Intuitively, the effect of Equation 5.7 is to add parabolic bumps of height \( a \) to consecutive intervals in the range of \( f \) of size \( h \). The parameter \( a \in [0, 1] \) sets the strength of the bump effect. The parameter \( h \) controls how “thick” the resulting bands are, and is similar in function to the distance between consecutive contours in isoline plots.

Two observations can be made over Figure 5.20(b). First, enriged plots combine the appearance of contour plots and height plots. Indeed, the sharp shading transitions, or ridges, occurring at points where \( f \) is a multiple of \( h \) are visually salient and have the same effect as contours. This is explained by the fact that \( z \), thus its normal too (which is next used for shading) is first-order discontinuous at these points. Also, the function \( z \) in Equation 5.7 is continuous over \( D \), and is also displayed at each point of the domain \( D \), creating a dense