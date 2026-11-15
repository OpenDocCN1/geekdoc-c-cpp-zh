![](bbox=[0.22, 0.09, 0.55, 0.21])

Thus, the area of the first trapezoid, \(A_1\), is computed using the pair of points \((x_1, y_1)\) and \((x_2, y_2)\).

\(A_1 = 1/2 * (x_2 - x_1) * (y_1 + y_2)\).

Since the points on the curve are equally spaced along the x-axis in this example, the base of each of the trapezoids is the same value. We can then compute the individual areas of the trapezoids as

+   - \(A1 = 1/2 * base * (y1 + y2),\)
+   - \(A2 = 1/2 * base * (y2 + y3),\)
+   - \(A3 = 1/2 * base * (y3 + y4),\)
+   - \(A4 = 1/2 * base * (y4 + y5).\)

Thus, the total area between \(a\) and \(b\) can be approximated by the sum of the areas of the four trapezoids:

\(\int_a^b f(x) dx \approx \frac{base}{2} ((y_1 + y_2) + (y_2 + y_3) + (y_3 + y_4) + (y_4 + y_5))\)
\(\approx \frac{base}{2} (y_1 + 2y_2 + 2y_3 + 2y_4 + y_5).\)

In general, if the area under a curve is divided into \(N\) trapezoids with equal bases, the area can be approximated by the following equation

\(\int_a^b f(x) dx \approx \frac{base}{2} \left( y_1 + 2 \sum_{k=2}^N y_k + y_{N+1} \right).\)

This equation is referred to as the trapezoidal rule.

When computing an integral with this numerical technique, we need to remember that the data points on the curve could come from different sources. If we have the equation for the curve, a C++ program can compute the data points that we use as the height of the trapezoids; in this case, we can choose the data points to be as close together or as far apart as we wish. Another possibility is that the points are experimentally collected data; in this case, we have a set of x-coordinates that represent the trapezoid base values and the y-coordinates that represent the heights of the trapezoids. We can still use the trapezoid areas to estimate the integral, but