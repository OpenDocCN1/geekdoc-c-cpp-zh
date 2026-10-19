
```python
L = 1 (red), 10', xtitle = 'x', ytitle = 'j(x)', \
 xmin = Xmin, xmax=Xmax, ymin=-0.2,ymax=0.5)
func1 = gcurve(color=color.red)
func2 = gcurve(color=color.green)
def down (x, n, m):
    j = zeros( (start + 2), float)
    j[m + 1] = 1.
    for k in range(m, 0, -1):
        j[k - 1] = ( (2.*k + 1.)*x )*j[k] - j[k + 1]
    scale = (sin(x)/x)/j[0]
    return j[n] * scale
for x in arange(Xmin, Xmax, step):
    func1.plot(pos = (x, down(x,1, start)))
    func2.plot(pos = (x, down(x,1,start)))
```

## 3.3 Experimental Error Investigation

Numerical algorithms play a vital role in computational physics. Your problem is to take a general algorithm and decide:

- 1. Does it converge?
- 2. How precise are the converged results?
- 3. How expensive (time-consuming) is it?

On first thought you may think, “What a dumb problem! All algorithms converge if enough terms are used, and if you want more precision, then use more terms.” Well, some algorithms may be asymptotic expansions that just approximate a function in certain regions of parameter space and converge only up to a point. Yet even if a uniformly convergent power series is used as the algorithm, including more terms will decrease the algorithmic error but will also increase the round-off errors. And because round-off errors eventually diverge to infinity, the best we can hope for is a “best” approximation. Good algorithms are good not only because they are fast but also because they require fewer steps and thus incur less round-off error.

Let us assume that an algorithm takes N steps to find a good answer. As a rule of thumb, the approximation (algorithmic) error decreases rapidly, often as the inverse power of the number of terms used:

```
ε_app ≈ α / N^β .   (3.28)
```

Here α and β are empirical constants that change for different algorithms and may be only approximately constant, and even then only as N → ∞. The fact that the error must fall off for large N is just a statement that the algorithm converges.

In contrast to algorithmic error, round-off error grows slowly and somewhat randomly with N. If the round-off errors in each step of the algorithm are not correlated, then we can model the accumulation of error as a random walk with step size equal to the machine precision ε_m:

```
ε_ro ≈ √N ε_m .   (3.29)
```

This is the slow growth with N that we expect from the round-off error. The total error in a computation is the sum of the two types of errors:

```
ε_tot = ε_app + ε_ro   (3.30)

ε_tot ≈ α / N^β + √N ε_m .   (3.31)
```

For small N, we expect the first term to be the larger of the two, but as N grows it will be overcome by the growing round-off error.

As an example, in Figure 3.3 we present a log–log plot of the relative error in numerical integration using the Simpson integration rule (Chapter 5). We use the log10 of the relative error because its negative tells us the number of decimal places of precision obtained.¹ Let us assume A is the exact answer and A(N) the computed answer. If

```
(A - A(N)) / A ≈ 10^{-9}, then log10 |(A - A(N)) / A| ≈ -9 .   (3.32)
```

We see in Figure 3.3 that the error does show a rapid decrease for small N, consistent with an inverse power law (3.28). In this region, the algorithm is converging. As N keeps increasing, the error starts to look somewhat erratic, with a slow increase on average. In accordance with (3.30), in this region the round-off error has grown larger than the approximation error and will continue to grow for increasing N. Clearly then, the smallest total error will be obtained if we can stop the calculation at the minimum near 10^{-14}, that is, when ε_app ≈ ε_ro.

![](img/bccda43674e4a93dee81c749eba8d2f7_86_0.png)

> ¹ Most computer languages use ln x = log_e x. Yet because x = a^{log_a x}, we have log10 x = ln x / ln 10.

In realistic calculations, you would not know the exact answer; after all, if you did, then why would you bother with the computation? However, you may know the exact answer for a similar calculation, and you can use that similar calculation to perfect your numerical technique. Alternatively, now that you understand how the total error in a computation behaves, you should be able to look at a table or, better yet, a graph like Figure 3.3, of your answer and deduce the manner in which your algorithm is converging. Specifically, at some point you should see that the mantissa of the answer changes only in the less significant digits, with that place moving further to the right of the decimal point as the calculation executes more steps. Eventually, however, as the number of steps becomes even larger, round-off error leads to a fluctuation in the less significant digits, with a gradual move towards the left on average. It is best to quit the calculation before this occurs.

Based upon this understanding, an approach to obtaining the best approximation is to deduce when your answer behaves like (3.30). To do that, we call A the exact answer and A(N) the computed answer after N steps. We assume that for large enough values of N, the approximation converges as

```
A(N) ≈ A + α / N^β ,
```

that is, that the round-off error term in (3.30) is still small. We then run our computer program with 2N steps, which should give a better answer, and use that answer to eliminate the unknown A:

```
A(N) - A(2N) ≈ α / N^β .
```

To see if these assumptions are correct and determine what level of precision is possible for the best choice of N, plot log10(|A(N) - A(2N)| / |A(2N)|) vs. log10 N, similar to what we have performed in Figure 3.3. If you obtain a rapid straight-line drop off, then you know you are in the region of convergence and can deduce a value for β from the slope. As N gets larger, you should see the graph change from a straight-line decrease to a slow increase as the round-off error begins to dominate. A good place to quit is before this. In any case, now you understand the error in your computation and therefore have a chance to control it.

As an example of how different kinds of errors enter into a computation, we assume that we know the analytic form for the approximation and round-off errors:

```
ε_app ≈ 1 / N² ,

ε_ro ≈ √N ε_m ,

⇒ ε_tot = ε_app + ε_ro

≈ 1 / N² + √N ε_m .
```

The total error is then a minimum when

```
dε_tot/dN = -2/N³ + (1/2) ε_m / √N = 0 ,   (3.39)

⇒ N^{5/2} = 4/ε_m .   (3.40)
```

For a double-precision calculation (ε_m ≃ 10^{-15}), the minimum total error occurs when

```
N^{5/2} ≃ 4/10^{-15} ⇒ N ≃ 1099 , ⇒ ε_tot ≃ 4 × 10^{-6} .   (3.41)
```

In this case, most of the error is as a result of round-off and is not the approximation error.

Seeing that the total error is mainly the round-off error ∝ √N, an obvious way to decrease the error is to use a smaller number of steps N. Let us assume we do this by finding another algorithm that converges more rapidly with N, for example, one with approximation error behaving like

```
ε_app ≃ 2/N⁴ .   (3.42)
```

The total error is now

```
ε_tot = ε_ro + ε_app ≃ 2/N⁴ + √N ε_m .   (3.43)
```

The number of points for minimum error is found as before:

```
dε_tot/dN = 0 ⇒ N^{9/2} ⇒ N ≃ 67 ⇒ ε_tot ≃ 9 × 10^{-7} .   (3.44)
```

The error is now smaller by a factor of 4, with only 1/16 as many steps needed. Subtle are the ways of the computer. In this case, the better algorithm is quicker and, by using fewer steps, produces less round-off error.

**Exercise:** Estimate the error now for a double-precision calculation.

### 3.3.1 Error Assessment

In Section 2.5, we have already discussed the Taylor expansion of sin x:

```
sin(x) = x - x³/3! + x⁵/5! - x⁷/7! + ⋯ = Σ_{n=1}^{∞} (-1)^{n-1} x^{2n-1}/(2n-1)! .   (3.45)
```

We now extend that discussion with errors in mind. The series (3.45) converges in the mathematical sense for all values of x. Accordingly, a reasonable algorithm to compute the sin(x) might be

```
sin(x) ≃ Σ_{n=1}^{N} (-1)^{n-1} x^{2n-1}/(2n-1)! .   (3.46)
```

- 1. Write a program that calculates sin(x) as the finite sum (3.46). (If you already did this in Chapter 2, then you may reuse that program and its results here. But remember, you should not be using factorials in the algorithm.)
- 2. Calculate your series for x ≤ 1 and compare it to the built-in function Math.sin(x) (you may assume that the built-in function is exact). Stop your summation at an N value for which the next term in the series will be no more than 10^{-7} of the sum up to that point:

$$
\frac{|(-1)^N x^{2N+1}|}{(2N+1)!} \le 10^{-7} \left|\sum_{n=1}^{N} \frac{(-1)^{n-1} x^{2n-1}}{(2n-1)!}\right|. \quad (3.47)
$$

- 3. Examine the terms in the series for x ≈ 3π and observe the significant subtractive cancellations that occur when large terms add together to give small answers. (Do not use the identity sin(x + 2π) = sin x to reduce the value of x in the series.) In particular, print out the near-perfect cancellation around n ≈ x/2.
- 4. See if better precision is obtained by using trigonometric identities to keep 0 ≤ x ≤ π.
- 5. By progressively increasing x from 1 to 10, and then from 10 to 100, use your program to determine experimentally when the series starts to lose accuracy and when it no longer converges.
- 6. Make a series of graphs of the error vs. N for different values of x. You should get curves similar to those in Figure 3.4.

![](img/bccda43674e4a93dee81c749eba8d2f7_89_0.png)

Figure 3.4 The error in the summation of the series for e^{-x} vs. N for various x values. The values of x increase vertically for each curve. Note that a negative initial slope corresponds to decreasing error with N, and that the dip corresponds to a rapid convergence followed by a rapid increase in error. (Courtesy of J. Wiren.)
