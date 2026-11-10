
$$[(-1/2 (I√3+1)(1/18√3√59 - 1/2)^(1/3) + -(I√3-1)/(3(1/18√3√59 - 1/2)^(1/3)), -1/2 (-I√3+1)(1/18√3√59 - 1/2)^(1/3) + -(-I√3-1)/(3(1/18√3√59 - 1/2)^(1/3)), (1/18√3√59 - 1/2)^(1/3) + -2/(3(1/18√3√59 - 1/2)^(1/3))]$$

```sage
sage: (x^3+2*x+1).roots(x, ring=RR)
[(-0.453397651516404, 1)]
```

```sage
sage: (x^3+2*x+1).roots(x, ring=CC)
[(-0.453397651516404, 1), (0.226698825758202 - 1.46771150871022*I, 1),
 (0.226698825758202 + 1.46771150871022*I, 1)]
```

### 2.2.2 Equations with no Explicit Solution

In most cases, as soon as the equation or system becomes too complex, no explicit solution can be found:

```sage
sage: solve(x^(1/x)==(1/x)^x, x)
[(1/x)^x == x^(1/x)]
```

However, this is not necessarily a limitation! Indeed, a specificity of computer algebra is the ability to manipulate objects defined by equations, and in particular to compute their properties, without solving them explicitly. Even better: in some cases, the equation defining a mathematical object is the best algorithmic representation for it.

For example, a function given by a linear differential equation and initial conditions is perfectly defined. The set of solutions of linear differential equations is closed under sum and product (among other operations), and thus forms an important class where equality to zero can be decided. However, if we explicitly solve such an equation, the obtained solution might be part of a much larger class where very few questions are decidable.

```sage
sage: y = function('y')(x)
sage: desolve(diff(y,x) + x*diff(y,x) + y == 0, y, [0,0,1])
-1/2*I*sqrt(2)*sqrt(pi)*erf(1/2*I*sqrt(2)*x)*e^(-1/2*x^2)
```

We will go back to this in more detail in Chapter 14 and in §15.1.2.

## 2.3 Analysis

This section is a quick introduction of useful functions in real analysis. For more advanced usage or more details, we refer to the following chapters, in particular about numerical integration (Chapter 14), non-linear equations (Chapter 12), and differential equations (Chapter 10).

### 2.3.1 Sums

The sum function computes symbolic sums. Let us obtain for example the sum of the $n$ first positive integers:

```text
sage: k, n = var('k, n')
sage: sum(k, k, 1, n).factor()
\frac{1}{2} (n + 1)n
```

The sum function allows simplifications of a binomial expansion:

```text
sage: n, k, y = var('n, k, y')
sage: sum(binomial(n,k) * x^k * y^(n-k), k, 0, n)
(x + y)^n
```

Here are more examples, among them the sum of the cardinalities of all parts of a set of $n$ elements:

```text
sage: k, n = var('k, n')
sage: sum(binomial(n,k), k, 0, n), \\
......: sum(k * binomial(n, k), k, 0, n), \\
......: sum((-1)^k*binomial(n,k), k, 0, n)
(2^n, 2^(n-1)*n, 0)
```

Finally, some examples of geometric sums:

```text
sage: a, q, k, n = var('a, q, k, n')
sage: sum(a*q^k, k, 0, n)
\frac{aq^{n+1}-a}{q-1}
```

To compute the corresponding power series, we should tell Sage that the modulus $q$ of $q$ is less than 1:

```text
sage: assume(abs(q) < 1)
sage: sum(a*q^k, k, 0, infinity)
\frac{a}{1-q}
```

```text
sage: forget(); assume(q > 1); sum(a*q^k, k, 0, infinity)
Traceback (most recent call last):
...
ValueError: Sum is divergent.
```

²Remember that by default, symbolic variables represent complex values.

Exercise 2 (Computing a sum by recurrence). Compute, without using the sum command, the sum of $p$-powers of integers from 0 to $n$, for $p = 1,\dots,4$:

$$S_n(p)=\sum_{k=0}^{n} k^p.$$

The following recurrence can be useful to compute this sum:

$$S_n(p)=\frac{1}{p+1}\left((n+1)^{p+1}-\sum_{j=0}^{p-1}\binom{p+1}{j}S_n(j)\right).$$

This recurrence is easily obtained when computing by two different methods the telescopic sum $\sum_{0\le k\le n}(k+1)^{p+1}-k^{p+1}$.

$$\sum_{0\le k\le n}(k+1)^{p+1}-k^{p+1}.$$

### 2.3.2 Limits

To determine a limit, we use the limit command or its alias lim. Let us compute the following limits:

- a) $\lim_{x\to 8}\frac{\sqrt[3]{x}-2}{\sqrt[3]{x+19}-3}$ ;
- b) $\lim_{x\to \frac{\pi}{4}}\frac{\cos(\frac{\pi}{4}-x)-\tan x}{1-\sin(\frac{\pi}{4}+x)}$.

```sage
sage: limit((x**(1/3) - 2) / ((x + 19)**(1/3) - 3), x = 8)
9/4
sage: f(x) = (cos(pi/4-x)-tan(x))/(1-sin(pi/4 + x))
sage: limit(f(x), x = pi/4)
Infinity
```

The last output says that one of the limits to the left or to the right is infinite. To know more about this, we study the limits to the left (minus) and to the right (plus), with the dir option:

```sage
sage: limit(f(x), x = pi/4, dir='minus')
+Infinity
sage: limit(f(x), x = pi/4, dir='plus')
-Infinity
```

### 2.3.3 Sequences

The above functions enable us to study sequences of numbers. We illustrate this by comparing the growth of an exponential sequence and a geometric sequence.

EXAMPLE. (A sequence study) Let us consider the sequence $u_n = \frac{2^{100n}}{100^n}$. Compute the first 10 terms. How does the sequence vary? What is the sequence limit? From which value of $n$ does $u_n \in ]0,10^{-8}[$ hold?

- 1. To define the term of order \(n\), we use a symbolic function. We then compute the first 10 terms by hand (loops will be introduced in Chapter 3):

```sage
sage: u(n) = n^100 / 100^n
sage: u(1);u(2);u(3);u(4);u(5);u(6);u(7);u(8);u(9);u(10)
0.0100000000000000
1.26765060022823e26
5.15377520732011e41
1.60693804425899e52
7.88860905221012e59
6.53318623500071e65
3.23447650962476e70
2.03703597633449e74
2.65613988875875e77
1.00000000000000e80
```

We could quickly conclude that \(u_n\) tends to infinity...

- 2. To get an idea of the variation of the sequence, we can draw the graph of the function \(n \to u_n\) (cf. Figure 2.2).

```sage
sage: plot(u(x), x, 1, 40)
Graphics object consisting of 1 graphics primitive
```

![](img/99840d73c45ee58b635c4eedc727fd9a_42_0.png)

Figure 2.2 – Graph of \(x \mapsto x^{100}/100^x\).

We then conjecture that the sequence decreases from index 22 onwards.

```sage
sage: v(x) = diff(u(x), x); sol = solve(v(x) == 0, x); sol
[x == 50/log(10), x == 0]
sage: floor(sol[0].rhs())
21
```

The sequence is thus increasing up to index 21, then decreasing after index 22.

|  | Functions and operators |
|---|---|
| Derivative | `diff(f(x), x)` |
| n-th derivative | `diff(f(x), x, n)` |
| Antiderivative | `integrate(f(x), x)` |
| Numerical integration | `integral_numerical(f(x), a, b)` |
| Symbolic summation | `sum(f(i), i, imin, imax)` |
| Limit | `limit(f(x), x=a)` |
| Taylor expansion | `taylor(f(x), x, a, n)` |
| Power series expansion | `f.series(x==a, n)` |
| Graph of a function | `plot(f(x), x, a, b)` |

Table 2.4 – Useful functions in analysis.

- 3. We then compute the limit:

```sage
sage: limit(u(n), n=infinity)
0
sage: n0 = find_root(u(n) - 1e-8 == 0, 22, 1000); n0
105.07496210187252
```

Since the sequence decreases from index 22 onwards, we deduce that starting from index 106, the sequence always lies in the interval ]0, 10⁻⁸[.

### 2.3.4 Power Series Expansions (*)

To compute a power series expansion of order n at x₀, the command to use is `f(x).series(x==x0, n)`.

Let us determine the power series expansion of the following functions:

- a) \((1 + \arctan x)^{1/x}\) of order 3, at \(x_0 = 0\);
- b) \(\ln(2\sin x)\) of order 3, at \(x_0 = \frac{\pi}{6}\).

```sage
sage: ((1+arctan(x))^(1/x)).series(x==0, 3)
(e) + (-\frac{1}{2}e)x + (\frac{1}{8}e)x^2 + O(x^3)
```

```sage
sage: (ln(2*sin(x))).series(x==pi/6, 3)
(√3)(-\frac{1}{6}π + x) + (-2)(-\frac{1}{6}π + x)^2 + O(-\frac{1}{216}(π - 6x)^3)
```

To extract the regular part of a power series expansion obtained by `series`, we call the truncate method:

```sage
sage: (ln(2*sin(x))).series(x==pi/6, 3).truncate()
-\frac{1}{18}(π - 6x)^2 - \frac{1}{6}√3(π - 6x)
```

The taylor command provides asymptotic expansions too. For example, let us see how the function \((x^3 + x)^{1/3} - (x^3 - x)^{1/3}\) behaves around +∞:

```sage
sage: taylor((x**3+x)**(1/3) - (x**3-x)**(1/3), x, infinity, 2)
2/3/x
```

**Exercise 3** (Computing a symbolic limit). Let \(f\) be \(C^3\) around \(a\in\mathbb{R}\). Compute

\[\lim_{h\to 0}\frac{1}{h^3}\bigl(f(a+3h)-3f(a+2h)+3f(a+h)-f(a)\bigr).\]

Generalisation?

Example. (*Machin’s formula*) Prove the following formula:

\[\frac{\pi}{4}=4\arctan\frac{1}{5}-\arctan\frac{1}{239}.\]

The astronomer John Machin (1680-1752) used this formula and the series expansion of arctan to compute 100 decimal digits of π in 1706.

We first notice that \(4\arctan\frac{1}{5}\) and \(\frac{\pi}{4}+\arctan\frac{1}{239}\) admit the same tangent:

```sage
sage: tan(4*arctan(1/5)).simplify_trig()
120/119
sage: tan(pi/4+arctan(1/239)).simplify_trig()
120/119
```

Since the real numbers \(4\arctan\frac{1}{5}\) and \(\frac{\pi}{4}+\arctan\frac{1}{239}\) are both in the open interval \(]0,\pi[\), they are equal. To obtain an approximation of π, we thus proceed as follows:

```sage
sage: f = arctan(x).series(x, 10); f
1*x + (-1/3)*x^3 + 1/5*x^5 + (-1/7)*x^7 + 1/9*x^9 + Order(x^10)
sage: (16*f.subs(x=1/5) - 4*f.subs(x=1/239)).n(); pi.n()
3.14159268240440
3.14159265358979
```

**Exercise 4** (A formula due to Gauss). The following formula required 20 pages of factorisation tables in the edition of Gauss’ works (cf. *Werke*, ed. Königl. Ges. d. Wiss. Göttingen, vol. 2, p. 477-502):

\[\frac{\pi}{4}=12\arctan\frac{1}{38}+20\arctan\frac{1}{57}+7\arctan\frac{1}{239}+24\arctan\frac{1}{268}.\]

- 1. Define \(\theta=12\arctan\frac{1}{38}+20\arctan\frac{1}{57}+7\arctan\frac{1}{239}+24\arctan\frac{1}{268}\). Verify with Sage that \(\tan\theta=1\).
- 2. Justify the inequality: \(\forall x\ge 0,\ \arctan x\le x\). Deduce Gauss’ formula.
- 3. Approximate the arctan function by its Taylor expansion of order 21 at 0, and deduce a new approximation of \(\pi\).

### 2.3.5 Series (*)

The commands introduced earlier can be used to perform computations on series. Let us give some examples.

Example. (*Evaluation of the Riemann zeta function*)
