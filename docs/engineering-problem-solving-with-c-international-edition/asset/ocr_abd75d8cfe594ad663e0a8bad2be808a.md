![](bbox=[0.05, 0.08, 0.93, 0.5])

+   - Hyperplane
+   - System of equations
+   - Nonsingular

These ideas can be extended to more than three variables, although it is harder to visualize the corresponding situations. We call the set of points defined by an equation with more than three variables a hyperplane. In general, we consider a set of m linear equations that contain n unknowns, where each equation defines a hyperplane that is not identical to another hyperplane in the set of equations. If m < n, then the system is underspecified, and a unique solution does not exist. If m = n, then a unique solution will exist if none of the equations represents parallel hyperplanes. If m > n, then the system is overspecified and a unique solution does not exist. A set of equations is also called a system of equations. A system with a unique solution is called a nonsingular system of equations, and a system with no unique solution is called a singular set of equations.

As a specific example, consider this system of equations:

```
3x + 2y - z = 10,
-x + 3y + 2z = 5,
x - y - z = -1.
```

The solution to this set of equations is the point (-2, -5, -6). Substitute these values in each of the questions to confirm that this point is a solution to the set of equations.

The material on matrices is not required for the development of the solution presented in this section. However, if you did cover that material, it is interesting to observe that a system