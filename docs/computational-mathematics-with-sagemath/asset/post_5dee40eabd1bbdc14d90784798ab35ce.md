
| Usual mathematical functions |  |
|---|---|
| Exponential and logarithm | `exp`, `log` |
| Logarithm in base a | `log(x, a)` |
| Trigonometric functions | `sin`, `cos`, `tan` |
| Inverse trigonometric functions | `arcsin`, `arccos`, `arctan` |
| Hyperbolic functions | `sinh`, `cosh`, `tanh` |
| Inverse hyperbolic functions | `arcsinh`, `arccosh`, `arctanh` |
| Integer part, etc. | `floor`, `ceil`, `trunc`, `round` |
| Square and n-th root | `sqrt`, `nth_root` |
| Rewriting trigonometric expressions |  |
| Simplification | `simplify_trig` |
| Linearisation | `reduce_trig` |
| Anti-linearisation | `expand_trig` |

**TABLE 2.2** Usual functions and simplification.

To linearise (resp. anti-linearise) a trigonometric expression, we use `reduce_trig` (resp. `expand_trig`):

```python
sage: f = cos(x)^6; f.reduce_trig()
1/32*cos(6*x) + 3/16*cos(4*x) + 15/32*cos(2*x) + 5/16
sage: f = sin(5 * x); f.expand_trig()
5*cos(x)^4*sin(x) - 10*cos(x)^2*sin(x)^3 + sin(x)^5
```

Expressions containing factorials can also be simplified:

```python
sage: n = var('n'); f = factorial(n+1)/factorial(n)
sage: f.simplify_factorial()
n + 1
```

The `simplify_rational` method tries to simplify a fraction; whereas to simplify square roots, logarithms or exponentials, the `canonicalize_radical` method is recommended:

```python
sage: f = sqrt(abs(x)^2); f.canonicalize_radical()
abs(x)
sage: f = log(x*y); f.canonicalize_radical()
log(x) + log(y)
```

The `simplify_full` command applies the methods `simplify_factorial`, `simplify_rational`, `simplify_trig`, `simplify_rational` and `expand_sum` (in that order).

All that is needed to determine the variation of a function (derivatives, asymptotes, extrema, localisation of zeroes and graph drawing) can be easily obtained using a computer algebra system. The main Sage operations applying to functions are presented in §2.3.

### 2.1.4 Assumptions

During a computation, the symbolic variables appearing in expressions are in general considered as taking potentially any value in the complex plane. This might be a problem when a parameter represents a quantity in a restricted domain (for example, a positive real number).

A typical case is the simplification of the expression $\sqrt{x^2}$. The proper way consists of using the `assume` function, which enables us to define the properties of a variable, which can in turn be reverted by the `forget` instruction:

```python
sage: assume(x > 0); bool(sqrt(x^2) == x)
True
sage: forget(x > 0); bool(sqrt(x^2) == x)
False
sage: n = var('n'); assume(n, 'integer'); sin(n*pi)
0
```

### 2.1.5 Some Pitfalls

> **The Simplification Problem**
>
> The examples of §2.1.5 demonstrate how important normal forms are, and in particular the *test of zero*.
>
> Some families of expressions, like polynomials, have a decision procedure for the equality to zero. As a consequence, for those families, a program is able to decide whether a given expression is zero or not. In most cases, this test is done via the reduction to the normal form: the expression is zero if and only if its normal form is 0.
>
> Unfortunately, not all classes of expressions have a normal form, moreover for some classes it is possible to show that no general method is able to decide in a finite amount of time whether an expression is zero. An example of such a class is made of the rational numbers, the constants π, log 2 and a variable, together with additions, subtractions, multiplications, exponentials and the sine function. The repeated use of *numerical_approx*, while increasing the precision, succeeds in most cases to conjecture if a given expression is zero or not; however, it has been proven impossible to write a computer program taking as input an expression of this class, and returning *true* if this expression is zero, and *false* otherwise.
>
> The simplification problem is much harder in those classes. Without any normal form, computer algebra systems can only provide some rewriting functions that the user must play with to obtain some result. Some hope is however possible, if we can identify sub-classes of expressions which have a normal form, and if we know which methods should be applied to compute those normal forms. The Sage approach to handle those issues is presented in more details in Chapter 5.

Let c be a slightly complex expression:

```python
sage: a = var('a')
sage: c = (a+1)^2 - (a^2+2*a+1)
```

where we want to solve the equation $cx = 0$ in the variable $x$:

```python
sage: eq = c * x == 0
```

One might be tempted to divide out this equation by $c$ before solving it:

```python
sage: eq2 = eq / c; eq2
x == 0
sage: solve(eq2, x)
[x == 0]
```

Fortunately, Sage avoids this mistake:

```python
sage: solve(eq, x)
[x == x]
```

Sage was able to correctly solve the equation because the coefficient $c$ is a polynomial expression. It is thus easy to check whether $c$ is zero, by expanding it:

```python
sage: expand(c)
0
```

and use the fact that two mathematically identical polynomials share the same expanded form, or said otherwise, that the expanded form is a normal form for polynomials.

However, on a slightly more complex example, Sage does not avoid the pitfall:

```python
sage: c = cos(a)^2 + sin(a)^2 - 1
sage: eq = c*x == 0
sage: solve(eq, x)
[x == 0]
```

even if Sage is able to correctly simplify and test to zero this expression:

```python
sage: c.simplify_trig()
0
sage: c.is_zero()
True
```

## 2.2 Equations

We now deal with equations and how to solve them; the main functions are summarised in Table 2.3.

### 2.2.1 Explicit Solving

Let us consider the following equation, with unknown $z$ and parameter $\varphi$:

$$z^2 - \frac{2}{\cos\varphi}z + \frac{5}{\cos^2\varphi} - 4 = 0, \quad \text{with } \varphi \in \left[-\frac{\pi}{2}, \frac{\pi}{2}\right].$$

It is written in Sage:

```python
sage: solve([cos(x)*sin(x) == 1/2, x+y == 0], x, y)
[[x == 1/4*pi + pi*Z, y == -1/4*pi - pi*Z]]
```

The solve command can also solve inequalities:

```python
sage: solve(x^2+x-1 > 0, x)
[[x < -1/2*sqrt(5) - 1/2], [x > 1/2*sqrt(5) - 1/2]]
```

Sometimes, solve returns the solutions of a system as floating-point numbers. For example, let us solve in $\mathbb{C}^3$ the following system:

\[
\begin{cases}
x^2yz = 18,\\
xy^3z = 24,\\
xyz^4 = 6.
\end{cases}
\]

```python
sage: x, y, z = var('x, y, z')
sage: solve([x^2 * y * z == 18, x * y^3 * z == 24,\
    ...:       x * y * z^4 == 6], x, y, z)
[[x == 3, y == 2, z == 1],
 [x == (1.337215067329613 - 2.68549874065195*I),
  y == (-1.700434271459228 + 1.052864325754712*I),
  z == (0.9324722294043555 - 0.3612416661871523*I)], ...]
```

Sage returns here 17 tuples, among which 16 are approximate complex solutions. To obtain a fully symbolic solution, we refer to Chapter 9.

To solve equations numerically, the `find_root` function takes as input a function of one variable or a symbolic equality, and the bounds of the interval in which to search. Sage does not find any symbolic solution to this equation:

```python
sage: expr = sin(x) + sin(2 * x) + sin(3 * x)
sage: solve(expr, x)
[sin(3*x) == -sin(2*x) - sin(x)]
```

Two choices are then possible: either a numerical solution,

```python
sage: find_root(expr, 0.1, pi)
2.0943951023931957
```

or first rewrite the expression:

```python
sage: f = expr.simplify_trig(); f
2*(2*cos(x)^2 + cos(x))*sin(x)
sage: solve(f, x)
[x == 0, x == 2/3*pi, x == 1/2*pi]
```

Last but not least, the roots function gives the roots of an equation with their multiplicity. The ring in which solutions are looked for can be given; with `RR` or `CC`, we obtain floating-point roots. The solving method is specific to the given equation, contrary to the `solve` method which uses a generic method.

Let us consider the degree-3 equation $x^3 + 2x + 1 = 0$. This equation has a negative discriminant, thus it has a real root and two complex roots, which are given by the roots method:

```python
sage: (x^3+2*x+1).roots(x)
```
