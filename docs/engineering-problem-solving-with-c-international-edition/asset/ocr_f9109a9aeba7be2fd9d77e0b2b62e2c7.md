# MODIFY!

These problems relate to the program developed in this section, which compares the analytical and simulated reliabilities.

+   1. Use this program to compute information comparing the simulation results for 10, 100, 1000, and 10000 trials, assuming that the component reliability is 0.85.
+   2. Use this program to compute information comparing the simulation results for 1000 trials, using five different random-number seeds. Assume that the component reliability is 0.75.
+   3. What component reliability is necessary to give a series reliability of 0.7? (Hint: Use the analytical reliability equation.) Validate your answer using this program.
+   4. What component reliability is necessary to give a parallel reliability of 0.9? Using the analytical reliability equation is not as easy in this case. If your calculator does not find roots of polynomial equations, just experiment with the program until you are close to the desired reliability.

![](bbox=[0.07, 0.385, 0.12, 0.425])

# 4.7 Numerical Technique: Roots of Polynomials*

A polynomial is a function of a single variable that can be expressed in the following general form:

```
f(x) = a_0 x^N + a_1 x^{N-1} + a_2 x^{N-2} + \cdots + a_{N-2} x^2 + a_{N-1} x + a_N, \quad (4.10)
```

where the variable is x and the coefficients are represented by $a_0, a_1, ... a_N$. The degree of a polynomial is equal to the largest nonzero exponent. Therefore, the general form for a cubic (degree 3) polynomial is

```
g(x) = a_0 x^3 + a_1 x^2 + a_2 x + a_3,
```

and a specific example of a cubic polynomial is

```
h(x) = x^3 - 2x^2 + 0.5x - 6.5.
```

Note that, for each term in the equation, the sum of the coefficient subscript and the variable exponent is equal to the polynomial degree using the notation in Equation (4.10).

# Polynomial Roots

The solutions to many engineering problems involve finding the roots of an equation of the form

```
y = f(x),
```

where the roots are the values of x for which y is equal to zero. Examples of applications in which we need to find roots of equations include designing the control system for a robotic arm, designing springs and shock absorbers for an automobile, analyzing the response of a motor, and analyzing the stability of a digital filter.

If a function f(x) is a polynomial of degree N, then f(x) has exactly N roots. These N roots may contain real roots or complex roots, as shown in the following examples. If we

*Optional section.