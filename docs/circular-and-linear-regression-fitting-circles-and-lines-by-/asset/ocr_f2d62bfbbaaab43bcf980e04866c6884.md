Similarly, a circle can be described by an algebraic equation

```
$$A(x^2 + y^2) + Bx + Cy + D = 0$$
```

with four parameters $A, B, C, D$ subject to constraint $B^2 + C^2 - 4AD = 1$, cf. (3.8) and (3.10). We have proved in Section 3.2 that the maximum likelihood estimates of $A, B, C, D$ are essentially restricted to a finite box, cf. (3.16); now it takes a little extra work (we omit details) to verify that the estimates of $A, B, C, D$ have finite moments.

# 6.5  General algebraic fits

Here we discuss curve fitting methods that are different from maximum likelihood estimation, i.e., from geometric fitting. Such methods are used in two ways, as it is explained in the beginning of Chapter 5. First, they supply an accurate initial guess to the subsequent iterative procedures that find the MLE. Second, they provide a fast inexpensive fit in applications where the geometric fitting procedures are prohibitively slow.

Simple algebraic fit. Perhaps the simplest nongeometric fit is the one minimizing

```
$$\mathscr{F}_1(\Theta) = \sum_{i=1}^{n} [P(x_i, y_i; \Theta)]^2. \quad (6.8)$$
```

To justify this method one notes that $P(x_i, y_i; \Theta) = 0$ if and only if the point $(x_i, y_i)$ lies on the curve; also, $[P(x_i, y_i; \Theta)]^2$ is small if and only if the point lies near the curve. If we fit a circle $P = (x-a)^2 + (y-b)^2 - R^2$, then the minimization of (6.8) brings us back to the popular Kåsa fit described in Section 5.1.

Oftentimes, $P$ is a polynomial in $\Theta$, then $\mathscr{F}_1(\Theta)$ is also a polynomial in $\Theta$, so its minimization is a fairly standard algebraic problem. For this reason the method (6.8) is called a *simple algebraic fit*.

Modified algebraic fit. In many fitting problems, $P(x, y; \Theta)$ is a polynomial in $x$ and $y$, too, and the parameter vector $\Theta$ is made by its coefficients. For example, a conic (ellipse, hyperbola) can be specified by

```
$$P(x, y; \Theta) = \theta_1 + \theta_2 x + \theta_3 y + \theta_4 x^2 + \theta_5 xy + \theta_6 y^2 = 0. \quad (6.9)$$
```

In such cases $\mathscr{F}_1(\Theta)$ is a quadratic form of $\Theta$, i.e., (6.8) minimizes

```
$$\mathscr{F}_1(\Theta) = \Theta^T \mathbf{M} \Theta, \quad (6.10)$$
```

where $\mathbf{M}$ is a symmetric positive semi-definite matrix computed from the data $(x_i, y_i)$, $1 \leq i \leq n$.

Note that the parameter $\Theta$ only needs to be determined up to a scalar multiple, because the desired curve $P(x, y; \Theta) = 0$ is the zero set of the function $P$, and it is not affected by the rescaling of $\Theta$.