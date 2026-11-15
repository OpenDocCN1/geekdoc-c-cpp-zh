
## Practice 8.6

Use the matrices A, B, and C presented next to evaluate by hand the expressions in these problems. If the expression can be evaluated, then write programs to test your answers using the functions developed in this section. The functions are available in a file matrix.cpp on the Instructor Resource Center.

A = [ 2  1 ] , B = [ -2  2 ]
    [ 0 -1 ]     [ -1  5 ]
    [ 3  0 ]

C = [ 3  2 ]
    [ -1 -2 ]
    [ 0  0 ]

- 1. |B|
- 2. C^T + A^T
- 3. A + B
- 4. AB
- 5. BA
- 6. B(C^T)
- 7. (BC)C^T

The problems at the end of the chapter use the matrix operations discussed in this section and also define additional matrix operations.

## 8.5 Numerical Technique: Solution to Simultaneous Equations

### Gauss elimination simultaneous linear equations

The need to solve a system of simultaneous equations occurs frequently in engineering problems. A number of methods exist for solving a system of equations, and each method has its advantages and disadvantages. In this section, we present the Gauss elimination method of solving a set of simultaneous linear equations; the equations are called linear equations because the equations contain only linear (degree-1) terms such as x, y, and z. However, before we present the details of this technique, we first present a graphical interpretation of the solution to a set of equations.

### Graphical Interpretation

A linear equation with two variables, such as 2x - y = 3, defines a straight line and is often written in the form y = mx + b, where m represents the slope of the line and b represents the y-intercept. Thus, 2x - y = 3 can also be written as y = 2x - 3. If we have two linear equations, they can represent two different lines that intersect in a single point; they can represent two parallel lines that never intersect, or they can represent the same line; these possibilities are shown in Figure 8.1.

Equations that represent two intersecting lines can be easily identified because they will have different slopes, as in y = 2x - 3 and y = -x + 3. Equations that represent two parallel lines will have the same slope, but different y-intercepts, as in y = 2x - 3 and y = 2x + 1. Equations that represent the same line have the same slope and y-intercept, as in y = 2x - 3 and 3y = 6x - 9.

If a linear equation contains three variables, x, y, and z, then it represents a plane in three-dimensional space. If we have two equations with three variables, they can represent two planes that intersect in a straight line, they can represent two parallel planes, or they can represent the same plane; these possibilities are shown in Figure 8.2. If we have three equations with three variables, the three planes can intersect in a single point, they can intersect in a plane, they can have no common intersection point, or they can represent the same plane. Examples of the possibilities that exist if the three equations define three different planes are shown in Figure 8.3. These ideas can be extended to more than three variables, although it is harder to visualize the corresponding situations.

### hyperplane

We call the set of points defined by an equation with more than three variables a hyperplane. In general, we consider a set of m linear equations that contain n unknowns, where each equation defines a hyperplane that is not identical to another hyperplane in the set of equations. If m < n then the system is underspecified, and a unique solution does not exist. If m = n, then a unique solution will exist if none of the equations represents parallel hyperplanes. If m > n, then the system is overspecified, and a unique solution does not exist. A set of equations is also called a system of equations. A system with a unique solution is called a nonsingular system of equations, and a system with no unique solution is called a singular set of equations.

system of equations nonsingular

As a specific example, consider the following system of equations:

```
3x + 2y - z = 10,
-x + 3y + 2z = 5,
x - y - z = -1.
```

![](img/0235a4ea835dc4575bd036e024a533b3_482_0.png)

![](img/0235a4ea835dc4575bd036e024a533b3_482_1.png)

![](img/0235a4ea835dc4575bd036e024a533b3_482_2.png)

Figure 8.1 Two lines.

The solution to this set of equations is the point (-2, 5, -6). Substitute these values in each of the questions to confirm that this point is a solution to the set of equations.

The material in the previous section on matrices is not required for the development of the solution presented in this section. However, if you did cover that material, it is interesting to observe that a system of linear equations can be expressed in terms of a matrix multiplication. To illustrate, let the information in the previous equations be expressed using the following matrices:

$$ A = \begin{bmatrix} 3 & 2 & -1 \\ -1 & 3 & 2 \\ 1 & -1 & -1 \end{bmatrix}, \quad X = \begin{bmatrix} x \\ y \\ z \end{bmatrix}, \quad B = \begin{bmatrix} 10 \\ 5 \\ -1 \end{bmatrix} . $$

![](img/0235a4ea835dc4575bd036e024a533b3_483_0.png)

Figure 8.2 Two planes.

Then, using matrix multiplication, we find that the system of equations can be written in the form

AX = B.

Go through the multiplication to convince yourself that this matrix equation yields the original set of equations.

In many engineering problems, we are interested in determining whether a common solution exists to a system of equations. If the common solution exists, then we want to determine it. In the next part of this section, we present the Gauss elimination technique for solving a set of simultaneous linear equations.

### Gauss Elimination

Before presenting a general description of the Gauss elimination technique, we illustrate the technique with a specific example, using the set of equations presented earlier:

- 3x + 2y - z = 10 (first equation),
- -x + 3y + 2z = 5 (second equation),
- x - y - z = -1 (third equation).

### elimination

The first step is an elimination step in which the first variable is eliminated from each equation that follows the first equation. This elimination is achieved by adding a scaled form of the first equation to each of the other equations. The term involving the first variable, x, in the second equation is -x. Therefore, if we multiply the first equation by 1/3 and add it to equation 2, we obtain a new equation in which the x variable has been eliminated:

```
-x + 3y + 2z = 5   (second equation)
x + 2/3 y - 1/3 z = 10   (first equation times 1/3)
-------------------------------------------
0x + 11/3 y + 5/3 z = 25/3   (sum).
```

The modified set of equations is then

```
3x + 2y - z = 10,
0x + 11/3 y + 5/3 z = 25/3,
x - y - z = -1.
```

We now eliminate the first variable from the third equation, using a similar process:

```
x - y - z = -1   (third equation),
-x - 2/3 y + 1/3 z = -10/3   (first equation times -1/3),
-------------------------------------------
0x - 5/3 y - 2/3 z = -13/3   (sum).
```

The modified set of equations is then

```
3x + 2y - z = 10,
11/3 y + 5/3 z = 25/3,
0x - 5/3 y - 2/3 z = -13/3.
```

We have now eliminated the first variable in all equations except for the first.

The next step is to eliminate the second variable in all equations except for the first and second, by adding the equations to a scaled form of the second equation:

```
0x - 5/3 y - 2/3 z = -13/3   (third equation),
0x + 5/3 y + 25/3 z = 125/33   (second equation times 5/11),
-------------------------------------------
0x + 0y + 3/33 z = 18/33   (sum).
```

![](img/0235a4ea835dc4575bd036e024a533b3_484_0.png)

![](img/0235a4ea835dc4575bd036e024a533b3_484_1.png)

![](img/0235a4ea835dc4575bd036e024a533b3_484_2.png)

![](img/0235a4ea835dc4575bd036e024a533b3_484_3.png)

![](img/0235a4ea835dc4575bd036e024a533b3_484_4.png)

Figure 8.3 Three distinct planes.
