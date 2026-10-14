![](bbox=[0.12, 0.16, 0.82, 0.32])

Figure 2.2. Left: Bilinear interpolation at V from V1, V2 and V3 in a triangle. Right: Bilinear interpolation to find the value of F at P from the value of F at the integer pixels at (i, j), (i + 1, j), (i, j + 1) and (i + 1, j + 1) in an image.

and therefore we are using linear interpolation. Given the locations of the points V1, V2 and V, we can find α by solving the equation

```
x = α x1 + (1 − α) x2
```

and use this α to find the value of C(V) from C(V1) and C(V2). The coefficients for V1 and V2 are both between 0 and 1 and their sum is equal to 1.0. Therefore, the function at V is estimated by a weighted sum of functions at V1 and V2 where each of the weights are fraction between 0 to 1 and their sum is equal to 1. This is called a convex combination of V1 and V2.

If the constraint is only that the sum of the coefficients is 1.0, but the coefficients can be of any value, then it is called an affine combination. If there are no constraints on the coefficients, it is called a linear combination. Note that a linear combination does not always mean linear interpolation. For example, if the Equation 2.1 was C(V) = α² C(V1) + (1 − α²) C(V2), it would not be a linear interpolation in α, but would still be a linear combination of C(V1) and C(V2) because alpha² and (1 − alpha²) are still scalar values. In other words, for linear interpolation, the derivative of the interpolated function should be a constant.

# 2.1.2 Bilinear Interpolation

Instead of considering 1D data, let us now consider 2D data where the neighborhood of a sample extends in two different directions. Bilinear interpolation entails interpolating in one direction followed by interpolating in the second direction.

For this, let us consider a triangle with three vertices V1, V2 and V3 (Figure 2.2a). To estimate the function C at a point V inside the triangle, we first estimate the function in the two directions V1V3 and V1V2. The point Q on V1V3