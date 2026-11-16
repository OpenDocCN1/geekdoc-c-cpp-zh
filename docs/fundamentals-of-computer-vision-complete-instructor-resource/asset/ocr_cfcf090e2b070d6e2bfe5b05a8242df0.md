![](bbox=[0.195, 0.115, 0.685, 0.375])

Figure 5.3 The brightness in an image can be thought of as a surface, a function of two variables. The surface is shown here as the smooth curves, and the flat surface represents the tangent plane at point x0, y0. The slopes of the tangent plane are the two spatial partial derivatives.

concept of estimating the derivative by differences, and then averaging the result in some way to compensate for noise. Probably the best known of these ad hoc kernels is the Sobel:

\frac{\partial f}{\partial x} = \frac{1}{8} \begin{bmatrix} -1 & 0 & 1 \\ -2 & 0 & 2 \\ -1 & 0 & 1 \end{bmatrix} \otimes f. (5.11)

The Sobel operator has the benefit of being center-weighted. That is, since the derivative is being estimated at the center point, it seems reasonable that the center row should count more than the rows above or below.

# 5.4.2 Derivative Estimation by Function Fitting

In this section, we present a fundamental approach to a data fitting problem, minimizing the sum-squared error. This general approach is presented in the context of a simple application: finding the plane that best fits a 2D set of points. However, it may find use in a wide variety of applications.

This approach presents an alternative way to make use of the continuous representation of an image f(x, y). Think of the brightness as a function of the two spatial coordinates, and consider a plane that is tangent to that brightness surface at a point, as illustrated in Figure 5.3.

In this case, we may write the continuous image representation of a point on the tangent plane using the equation of a plane

f(x, y) = ax + by + c. (5.12)