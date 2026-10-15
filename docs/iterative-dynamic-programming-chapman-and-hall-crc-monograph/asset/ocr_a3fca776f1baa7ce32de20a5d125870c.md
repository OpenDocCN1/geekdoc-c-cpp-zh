12.52943 68.13003] was obtained 66 times. The other 34 starting points gave nonfeasible solutions by having some of the variables negative. The total computation time for the 100 starting conditions was 0.11 s. The success rate was decreased to 28 out of 100 starting points by taking a smaller range for the initial values for x₂, namely 0 ≤ x₂ ≤ 10, as was used by Gupta [7], but the computation time was reduced to 0.06 s. By using the range 0 ≤ x₁ ≤ 1000, 0 ≤ x₂ ≤ 1000, the success rate was 57 times out of 100, obtained also in a total computation time of 0.06 s.

# Example 5

Sometimes it is important to capture all the possible solutions to a set of nonlinear algebraic equations. For example, in the problem of finding the maximum distance from the origin to the intersection of an ellipsoid with a hyperboloid, as considered by Luus [12], and by Wang and Luus [30], when Lagrange multipliers are used, the optimum lies at one of the 8 stationary points. Therefore, it is important to locate all of the stationary points, and the stationary point that gives the maximum value for the square of the distance P = x₁² + x₂² + x₃² provides the solution to the problem. The system of algebraic equations is

```
x₇ = x₃ / (2x₃ + 0.2x₂)  (1.129)
x₆ = 4(x₂ − 0.2) + 0.1x₁ + 0.2x₃  (1.130)
x₅ = (x₆x₇ − x₂) / (x₂ + 2x₆x₇)  (1.131)
x₄ = (4x₅ − 2)x₇  (1.132)
f₁ = 2x₁ + x₄[8(x₁ − 0.5) + 0.1x₂] + 4x₁x₅  (1.133)
f₂ = 2(x₁² − x₃² − 1) + x₂²  (1.134)
f₃ = 4(x₁ − 0.5)² + 2(x₂ − 0.2)² + x₃² + 0.1x₁x₂ + 0.2x₂x₃ − 16,  (1.135)
```

where x₄ and x₅ are Lagrange multipliers, and we have introduced x₆ and x₇ to simplify the formulation of the problem. By choosing 200 random starting points for x₁, x₂, and x₃ in the range −2 ≤ xᵢ ≤ 2, i = 1,2,3, we were able to locate all the 8 stationary points with the frequencies given in Table 1.1. It is noted that one of the stationary points was obtained only twice and another one only three times, whereas the stationary point related to the maximum distance was obtained 21 times. To solve the algebraic equations from the 200 starting points took a minimum of 6 iterations and a maximum of 15 iterations, with a total computation time of 0.11 s on the Pentium/120 for the 200 starting points. Therefore, the computation time is quite negligible.