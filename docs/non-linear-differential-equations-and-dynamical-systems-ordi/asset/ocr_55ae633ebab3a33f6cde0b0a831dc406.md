that proves (5.513) for n+1. QED. It has been shown that the definition of first-order derivative (4.511), leads to the discretization (problem 156) second-order derivative (4.512a, b) and (4.513) derivative of arbitrary positive integer n. The latter (4.513), apart from dearrangement, is similar to the binomial expansion (4.518):

```
$$(a+b)^n = \sum_{m=0}^n \binom{n}{m} a^m b^{n-m}. \quad (4.518)$
```

The method (4.514a, b) through (4.517) could be used as an algebraic proof of the binomial expansion (4.518) in (1.25.38) instead of the proof (section I.25) using the Taylor series. The derivative of arbitrary order (4.513) without the limit $h \to 0$ is used to discretize a differential equation (note 4.9) with step $h$.

# NOTE 4.9: Relation between Ordinary Differential and Difference Equations

An ordinary differential equation (4.519b) of order (4.519a):

```
$$n=0,1,...,N: \quad 0 = F(x;y(x),y'(x),y''(x),...,y^{(n)}(x),...,y^{(N)}(x)), \quad (4.519a, b)$
```

can (problem 157) be transformed by (4.520a, b) to a finite difference equation (4.520c) with step $h$ of the same order (4.519a):

```
$$y_n = y(x),y_{n-m} \equiv y(x+mh): \quad 0 = G(x;y(x),y(x+h),...,y(x+nh)) \equiv G(x,y_n,y_{n+1},...,y_{n+N}), \quad (4.520a-c)$
```

(i) discretizing the derivatives by (4.513); and (ii) using the notation (4.520a, b) in (4.520c). The $N$ single-point boundary conditions (1.5a, b) $\equiv (4.521b) for the differential equation (4.519b) become (4.513b) $\equiv (4.521b) for the finite difference equation (4.520c):

```
$$m=0,...,n-1: \quad y^{(m)}(x_0) = a_m \sum_{k=0}^m (-1)^{m-k} \binom{m}{k} y_k. \quad (4.521a-c)$
```

For example, the linear second-order differential equation with constant coefficients (4.522a) is discretized using (4.512b) with step $h$:

```
$$y''+y=0: \quad 0 = y_{n+2}-2y_{n+1}+(1+h^2)y_n. \quad (4.522a, b)$
```