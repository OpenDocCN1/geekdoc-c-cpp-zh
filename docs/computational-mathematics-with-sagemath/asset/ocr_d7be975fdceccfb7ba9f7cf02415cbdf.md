possible. However, when it is not possible to solve the inequality $a_n \le 10^{-p}$, a `while` loop is necessary.

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

```
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
```

# ## 3.2.2 Conditionals

Another important instruction is the conditional (or test), which enables us to execute some instructions depending on the result of a boolean condition. The structure of the conditional and two possible syntaxes are:

```
```
if a condition:                 if a condition:
    an instruction sequence         an instruction sequence
                                else:
                                    another instruction sequence
```
```

The Syracuse sequence is defined using a parity condition:

$$
u_0 \in \mathbb{N} - \{0\}, \quad u_{n+1} = \begin{cases} u_n/2 & \text{if } u_n \text{ is even} \\ 3u_n + 1 & \text{if } u_n \text{ is odd.} \end{cases}
$$