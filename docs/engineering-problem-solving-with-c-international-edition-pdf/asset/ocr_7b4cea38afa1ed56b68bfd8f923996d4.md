# Practice!

A = [ 2 1 ; 0 -1 ; 3 0 ], B = [ -2 2 ; -1 5 ] .
C = [ 3 2 ; -1 -2 ; 0 2 ]

+   1. |B|
+   2. C^T + A^T
+   3. A + B
+   4. AB
+   5. BA
+   6. B(C^T)
+   7. (CB)C^T

The problems at the end of the chapter use the matrix operations discussed in this section and also define additional matrix operations.

# 8.5 Numerical Technique: Solution to Simultaneous Equations

Gauss elimination simultaneous linear equations

The need to solve a system of simultaneous equations occurs frequently in engineering problems. A number of methods exist for solving a system of equations, and each method has its advantages and disadvantages. In this section, we present the Gauss elimination method of solving a set of simultaneous linear equations; the equations are called linear equations because the equations contain only linear (degree-1) terms such as x, y, and z. However, before we present the details of this technique, we first present a graphical interpretation of the solution to a set of equations.

# Graphical Interpretation

A linear equation with two variables, such as 2x - y = 3, defines a straight line and is often written in the form y = mx + b, where m represents the slope of the line and b represents the y-intercept. Thus, 2x - y = 3 can also be written as y = 2x - 3. If we have two linear equations, they can represent two different lines that intersect in a single point; they can represent two parallel lines that never intersect, or they can represent the same line; these possibilities are shown in Figure 8.1.

Equations that represent two intersecting lines can be easily identified because they will have different slopes, as in y = 2x - 3 and y = -x + 3. Equations that represent two parallel