Use Gaussian Elimination to solve this linear system for n = 4, a₁ = 0.8, a₂ = 0.7, a₃ = 0.6, b₁ = 0, b₂ = 0.05, b₃ = 0.15, b₄ = 0.1, and each cᵢ = 100.

# 6. Programming Problem 10 of Section 9.4 in Chapter 9 described the method of least squares for finding the equation of a line that best fits a set of data points. This method can also be used to find best-fitting curves of higher degree. For example, to find the equation of the parabola

```
y = A + Bx + Cx²
```

that best fits a set of n data points, the values of A, B, and C must be determined for which the sum of the squares of the deviations of the observed y-values from the predicted y-values (using the equation) is as small as possible. These values are found by solving the linear system

```
nA + (∑ x) B + (∑ x²) C = ∑ y
```

```
(∑ x) A + (∑ x²) B + (∑ x³) C = ∑ xy
```

```
(∑ x²) A + (∑ x³) B + (∑ x⁴) C = ∑ x² y
```

Find the equation of the least-squares parabola for the following set of data points:

| x | y |
|---|---|
| 0.05 | 0.957 |
| 0.12 | 0.851 |
| 0.15 | 0.832 |
| 0.30 | 0.720 |
| 0.45 | 0.583 |
| 0.70 | 0.378 |
| 0.84 | 0.295 |
| 1.05 | 0.156 |

# 7. Linear systems similar to those in Problem 6 must be solved to find least-squares curves of higher degrees. For example, for a least-squares cubic,

```
y = A + Bx + Cx² + Dx³
```