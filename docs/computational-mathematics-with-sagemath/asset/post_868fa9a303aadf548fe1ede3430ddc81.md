
to the recurrence relation. The first iteration computes $u_1$ from $u_0$ for $n = 1$, the second one likewise from $u_1$ to $u_2$ when $n = 2$, and the last of the $n$ iterations updates $U$ from $u_{n-1}$ to $u_n$:

```sage
sage: U = 1.0          # or U = 1. or U = 1.000
sage: for n in [1..20]:
....:     U = 1 / (1 + U^2)
sage: U
0.682360434761105
```

The same program with the integer $U = 1$ instead of the floating-point number $U = 1.0$ on the first line will perform exact computations on rational numbers; then $u_{10}$ becomes a rational number with several hundred digits, and $u_{20}$ has hundreds of thousands of digits. Exact computations are useful when rounding errors accumulate in numerical approximations. Otherwise, *by hand or with the computer*, the computations on numerical approximations of a dozen digits are faster than those on integers or rational numbers of thousands of digits or more.

The sums or products admitting recurrence formulas are computed the same way:

$$S_n = Σ_{k=0}^n (2k)(2k+1) = 2·3 + 4·5 + ⋯ + (2n)(2n+1),$$
$$S_0 = 0,    S_n = S_{n-1} + (2n)(2n+1)   for n ∈ ℕ − {0}.$$

The following programming method follows that of recurrent sequences: starting from 0, we add successive terms for $k = 1$, $k = 2$, ..., until $k = n$:

```sage
sage: S = 0 ; n = 10
sage: for k in [1..n]:
....:     S = S + (2*k) * (2*k+1)
sage: S
1650
```

This example highlights a general method to compute a sum; however, in this simple case, a symbolic computation yields the general answer:

```sage
sage: n, k = var('n, k') ; res = sum(2*k*(2*k+1), k, 1, n)
sage: res, factor(res)        # result expanded, factorised
(4/3*n^3 + 3*n^2 + 5/3*n, 1/3*(4*n + 5)*(n + 1)*n)
```

Those results might also be obtained with the *pen and pencil* method from well-known sums:

$$Σ_{k=1}^n k = n(n+1)/2,    Σ_{k=1}^n k^2 = n(n+1)(2n+1)/6,$$
$$Σ_{k=1}^n 2k(2k+1) = 4Σ_{k=1}^n k^2 + 2Σ_{k=1}^n k = 2n(n+1)(2n+1)/3 + n(n+1)$$
$$= n(n+1)((4n+2)+3)/3 = n(n+1)(4n+5)/3.$$

$(S_{2n})_{n∈N}$ and $(S_{2n+1})_{n∈N}$ satisfy Eq. (3.1), with common limit, say ℓ. Hence the sequence $(S_n)_{n∈N}$ also converges to ℓ and we have $S_{2p+1} ≤ ℓ = \lim_{n→∞} S_n ≤ S_{2p}$.

The following program illustrates this result for the sequence $a_k = 1/k^3$ from $k = 1$, by storing in two variables $U$ and $V$ the partial sums $S_{2n}$ and $S_{2n+1}$ enclosing the limit:

```sage
sage: U = 0.0                  # the sum S0 is empty, of value zero
sage: V = -1.0                 # S1 = -1/1^3
sage: n = 0                    # U and V contain S(2n) and S(2n+1)
sage: while V-U >= 1.0e-6:
....:     n = n+1              # n += 1 is equivalent
....:     U = V + 1/(2*n)**3   # going from S(2n-1) to S(2n)
....:     V = U - 1/(2*n+1)**3 # going from S(2n) to S(2n+1)
sage: V, U
(-0.901543155458595, -0.901542184886447)
```

The main loop increases the value of $n$ until the two terms $S_{2n}$ and $S_{2n+1}$ are close enough. The two variables $U$ and $V$ contain two consecutive terms; the loop body computes $S_{2n}$ from $S_{2n−1}$, and then $S_{2n+1}$ from $S_{2n}$, with the crossed assignments to $U$ and $V$.

The program halts when two consecutive terms $S_{2n+1}$ and $S_{2n}$ surrounding the limit are close enough, the approximation error — without taking into account rounding errors — then satisfies $0 ≤ a_{2n+1} = S_{2n} − S_{2n+1} ≤ 10^{−6}$.

Programming these five alternating series is similar:

$$∑_{n≥2} (−1)^n / \log n,    ∑_{n≥1} (−1)^n / n,    ∑_{n≥1} (−1)^n / n²,$$
$$∑_{n≥1} (−1)^n / n⁴,    ∑_{n≥1} (−1)^n e^{−n \ln n} = ∑_{n≥1} (−1)^n / n^n.$$

The terms of these series converge more or less rapidly to 0, thus the limit approximations require more or fewer computations.

Looking for a precision of 3, 10, 20 or 100 digits on the limits of these series consists in solving the following inequalities:

- $1/\log n \le 10^{-3} \iff n \ge e^{10^3} \approx 1.97\cdot10^{434}$
- $1/n \le 10^{-10} \iff n \ge 10^{10}$
- $1/n \le 10^{-3} \iff n \ge 10^3$
- $1/n^2 \le 10^{-10} \iff n \ge 10^5$
- $1/n^2 \le 10^{-3} \iff n \ge \sqrt{10^3} \approx 32$
- $1/n^4 \le 10^{-10} \iff n \ge 317$
- $1/n^4 \le 10^{-3} \iff n \ge (10^3)^{1/4} \approx 6$
- $e^{-n\log n} \le 10^{-10} \iff n \ge 10$
- $e^{-n\log n} \le 10^{-3} \iff n \ge 5$
- $1/n^2 \le 10^{-20} \iff n \ge 10^{10}$
- $1/n^2 \le 10^{-100} \iff n \ge 10^{50}$
- $1/n^4 \le 10^{-20} \iff n \ge 10^5$
- $1/n^4 \le 10^{-100} \iff n \ge 10^{25}$
- $e^{-n\log n} \le 10^{-20} \iff n \ge 17$
- $e^{-n\log n} \le 10^{-100} \iff n \ge 57$

In the simplest cases solving these inequalities yields an index $n$ from which the value $S_n$ is close enough to the limit ℓ, and then a for enumeration loop is possible. However, when it is not possible to solve the inequality $a_n \le 10^{-p}$, a `while` loop is necessary.

Numerical approximations of some of the above limits are too expensive, in particular when the index $n$ gets as large as $10^{10}$ or $10^{12}$. A mathematical study can sometimes determine the limit or approach it by other methods, like for the series giving values of the Riemann zeta function:

$$
\lim_{n \to +\infty} \sum_{k=1}^n \frac{(-1)^k}{k^3} = -\frac{3}{4}\zeta(3), \quad \text{with } \zeta(p) = \lim_{n \to +\infty} \sum_{k=1}^n \frac{1}{k^p},
$$
$$
\lim_{n \to +\infty} \sum_{k=1}^n \frac{(-1)^k}{k} = -\log 2, \quad \lim_{n \to +\infty} \sum_{k=1}^n \frac{(-1)^k}{k^2} = -\frac{\pi^2}{12},
$$
$$
\lim_{n \to +\infty} \sum_{k=1}^n \frac{(-1)^k}{k^4} = -\frac{7\pi^4}{6!}.
$$

Sage is able to compute symbolically some of these series, and determine a 1200-digit numerical approximation of $\zeta(3)$ in a few seconds, by doing far fewer operations than the $10^{400}$ ones required by the definition:

```python
sage: k = var('k');
sum((-1)^k/k, k, 1, +oo)
-log(2)
sage: sum((-1)^k/k^2, k, 1, +oo), sum((-1)^k/k^3, k, 1, +oo)
(-1/12*pi^2, -3/4*zeta(3))
sage: -3/4 * zeta (N(3, digits = 1200))
-0.901542677369695714049803621133587493073739719255374161344\
2036656036786534385249716416984190507200144360964936836445539\
5638689969900496241033229762790592512109045633721202005039\
...
0199954926528892970698040801518083359081543437310705359919271\
7989701514061635603285245024606505197774421390289145054538\
9019612163591468378139165980642866722553438177035397601706262
```

### 3.2.2 Conditionals

Another important instruction is the conditional (or test), which enables us to execute some instructions depending on the result of a boolean condition. The structure of the conditional and two possible syntaxes are:

```
if a condition:                 if a condition:
    an instruction sequence         an instruction sequence
                                else:
                                    another instruction sequence
```

The Syracuse sequence is defined using a parity condition:

$$
u_0 \in \mathbb{N} - \{0\}, \quad u_{n+1} = \begin{cases} u_n/2 & \text{if } u_n \text{ is even} \\ 3u_n + 1 & \text{if } u_n \text{ is odd.} \end{cases}
$$

The Collatz conjecture says — with no known proof in 2017 — that for all initial values $u_0 ∈ \mathbb{N} − \{0\}$, there exists a rank $n$ for which $u_n = 1$. The next terms are then 4, 2, 1, 4, 2, etc. The computation of each term of this sequence requires a parity test. This condition is checked within a while loop, which determines the smallest $n ∈ \mathbb{N}$ satisfying $u_n = 1$:

```python
sage: u = 6 ; n = 0
sage: while u != 1:    # the test u <> 1 is also possible
....:   if u % 2 == 0: # the operator % yields the remainder
....:       u = u/2    # //: Euclidean division quotient
....:   else:
....:       u = 3*u+1
....:   n = n+1
sage: n
8
```

Checking whether $u_n$ is even is done by comparing to 0 the remainder of the Euclidean division of $u_n$ by 2. The variable $n$ at the end of the block is the number of iterations. The loop ends as soon as $u_n = 1$; for example if $u_0 = 6$ then $u_8 = 1$ and $8 = \min\{p ∈ \mathbb{N} \mid u_p = 1\}$:

| p | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | ... |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| u_p | 6 | 3 | 10 | 5 | 16 | 8 | 4 | 2 | 1 | 4 | 2 | ... |

Verifying step-by-step the correct behaviour of the loop can be done using a spy-instruction `print(u, n)` inside the loop body.

The if instruction also allows nested tests in the else branch using the elif keyword. The two following structures are thus equivalent:

```
if a condition cond1:
    an instruction sequence inst1
else:
    if a condition cond2:
        an instruction sequence inst2
    else:
        if a condition cond3:
            an instruction sequence inst3
        else:
            in other cases instn

if cond1:
    inst1
elif cond2:
    inst2
elif cond3:
    inst3
else:
    instn
```

Like for loops, small instruction sequences may be put after the colon on the same line, rather than in an indented block below.

### 3.2.3 Procedures and Functions

**General Syntax.** As in other computer languages, the Sage user can define her/his own procedures or functions, using the `def` command whose syntax is detailed below. In this book, we call a *function* (resp. *procedure*) a sub-program
