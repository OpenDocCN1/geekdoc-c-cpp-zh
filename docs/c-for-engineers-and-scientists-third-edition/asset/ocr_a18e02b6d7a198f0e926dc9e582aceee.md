# Chapter 14 779

+   b. Compute $T_1$ by using the value of $T_0$ and Equation 14.11.

+   c. Continue the calculation through $T_4$.

Collect your results in the form of a table. (Be careful: Errors in one step carry over into the next.)

+   i. $\int_0^s x^2 \, dx$ (Exact result = 170.667)

+   ii. $\int_0^s x^4 \, dx$ (Exact result = 6553.63)

+   2. (Practice) Evaluate the following integrals using the trapezoidal rule:

+   a. Evaluate $T_0$ for one panel using Equation 14.6.

+   b. Compute $T_1$ using the value of $T_0$ and Equation 14.11.

+   c. Continue the calculation through $T_4$.

Collect your results in the form of a table. (Be careful: Errors in one step carry over into the next.)

+   i. $\int_0^1 e^{-x^2} \, dx$ (Exact result = 1-2/e = .264241175 . . .)

+   ii. $\int_0^{\pi/2} x \sin(x) \, dx$ (Exact result = 1.0)

+   3. (Practice) Evaluate the following integrals using the trapezoidal rule:

+   a. Evaluate $T_0$ for one panel using Equation 14.6.

+   b. Compute $T_1$ using the value of $T_0$ and Equation 14.11.

+   c. Continue the calculation through $T_4$.

Collect your results in the form of a table. (Be careful: Errors in one step carry over into the next.)

+   i. $\int_0^1 (1+x^2)^{3/2} \, dx$ (Exact result = 1.567951962 . .)

+   ii. $\int_0^\infty e^{-x^2} \, dx$ (Exact result = 0.74682404 . . .)

# 14.7 Simpson's Rule

The trapezoidal rule is based on approximating the function by straight-line segments. To improve the method's accuracy and convergence rate, an obvious approach is approximating the function by parabolic segments in place of straight lines. This approach results in an approximation for the integral known as **Simpson's rule**; a simple example is shown in Figure 14.11. Specifying a parabola uniquely requires three points, so lowest-order Simpson's rule has two panels.