# Non-Linear Differential Equations and Dynamical Systems

leading to a linear second-order differential equation (3.96). Thus the change of variable (3.95a) = (3.97a, b):

```
$$y(x) = -\frac{1}{R(x)} \frac{d}{dx}\{\log[u(x)]\} \quad \Leftrightarrow \quad u(x) = C \exp\left\{-\int^x R(\xi)y(\xi)d\xi\right\}$$$\$
$(3.97a, b)$
```

transforms (standard LVIII) the Riccati equation (3.58) into (3.96) = (3.98a-c), a linear second-order differential equation (3.98a) with coefficients (3.98b, c):

```
$$u'' + Au' + Bu = 0; \quad A = -P-\frac{R'}{R}, \quad B = QR.$$
$(3.98a-c)$
```

The general integral of the linear second-order differential equation (3.98a) is a linear combination of two linearly independent particular integrals (3.99b) involving two arbitrary constants:

```
$$C = \frac{C_2}{C_1} \quad u(x) = C_1u_1(x) + C_2u_2(x); \quad y(x) =-\frac{\u_1'(x) + Cu_2'(x)}{R(x)u_1(x) + Cu_2(x)},$\$
$(3.99a-c)$
```

it follows (3.95a) = (3.97a) that the solution of the Riccati equation (3.58) is a bilinear function (3.99c) of a single constant of integration (3.99a).

# 3.6.2 Relation with the Theory of Special Functions

The transformations (3.97a, b) hold in directions: (i) if y is a solution of the Riccati equation (3.58), then (3.97b) is a solution of the linear second-order differential equation (3.98a-c); (ii) if u is a solution of the linear differential equation (3.98a-c) is known, then (3.97a) specifies a solution of the Riccati equation (3.100):

```
$$y' =-\frac{B}{R}\left(A-\frac{R'}{R}\right)y + Ry^2.$$
$(3.100)$
```

The solution of linear second-order differential equations specifies a wide variety of special functions, as Legendre (hyperspherical Legendre) polynomials [section III.8.3 (III.9.6)] and hypergeometric functions (notes I.23.2-I.23.3). These special functions generally have infinite representations, like the power series for the Gaussian (sections I.29.9 and II.3.9) and generalized (section I.30.20 and note II.3) of hypergeometric series and also hypergeometric series (section II.1.9). The theory of linear differential equations with variable coefficients and related special functions is