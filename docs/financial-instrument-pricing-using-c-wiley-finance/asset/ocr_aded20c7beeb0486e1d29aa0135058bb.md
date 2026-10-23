# 5. (Picard Iteration)

Apply the techniques of Section 24.5.1 to determine the intervals in which the following problems have unique solutions (or not):

dy/dt = y(1 − y), y(0) = 1/2

dy/dt = 1 + y², y(0) = 0 (solution y(t) = tan(t))

dy/dt = 2y/x, y(t₀) = y₀.

# 6. (Runge–Kutta Method)

Answer the following questions:

+   a) Construct the Butcher tableau for the schemes (24.34) (Ralston) and (24.35) (Heun) (see Section 24.10 (Appendix) for a definition).

+   b) Compare the accuracy of these two methods against each other.

+   c) Construct and implement the third-order Runge–Kutta method defined by the following Butcher tableau:

|   |   |   |   |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 1/2 | 1/2 | 0 | 0 |
| 1 | -1 | 2 | 0 |
|   | 1/6 | 2/3 | 1/6 |

Write the scheme in algorithmic form.

# 7. (Coding Exercises)

The goal in this exercise is to implement a number of schemes for (24.24) and to test them on some of the examples in this chapter.

Answer the following questions:

+   a) Implement the second-order Ralston method (24.34) and its extrapolated fourth-order version (see Section 24.6.3). Compare the accuracy of these methods on scalar stiff and non-stiff ODEs. Carry out the same exercise for systems of ODEs.

+   b) Implement the Heun method (24.35) and follow the steps as outlined in part a).

+   c) Test the non-stiff and stiff systems (24.48) and (24.49) using explicit Euler, fourth-order Runge–Kutta and Ralston methods for a range of time steps. Compare the relative accuracy.

# 24.10 APPENDIX

Runge–Kutta methods are one-step methods for the numerical solution of the ordinary differential equation:

dy/dt = f(t, y)