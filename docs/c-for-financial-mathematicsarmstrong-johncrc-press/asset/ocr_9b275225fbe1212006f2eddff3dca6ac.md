3.9.6. For each $n \in N$ define a mathematical function $h_n$ as follows

```
$\begin{align*}h_0(x, a_0) &= a_0\\h_n(x, a_0, a_1, a_2, \dots, a_n) &= a_0 + x h_{n-1}(x, a_1, a_2, \dots, a_n).\end{align*}$
```

We will call these “Horner functions” because they use the Horner method of evaluating a polynomial. Any polynomial in $x$ can be rewritten as

```
$h_n(x, a_0, a_1, a_2, \dots, a_n)$
```

for appropriate constants $a_i$. The advantage of using $h$ to evaluate the polynomial is that you don’t have to compute high powers of $x$.

Implement the first few Horner functions in C++. Give all your functions the same overloaded name **hornerFunction**. Use a Horner function to simplify your **normcdf** function.

> **Note:** This question requires some tedious cutting and pasting. Hopefully you will want to rebel against this and find a better way of solving the problem than just cutting and pasting! However, in this case some tedious cutting and pasting is the right thing to do. This is a rare time where you should violate the Once and Only Once principle. The original code for **normcdf** should have been very fast because it contains no complex code like loops (to be covered in Chapter 4). We’re introducing **hornerFunction** to improve readability, but we don’t want to harm the speed too much. That’s why we don’t want to be too clever.

3.9.7. Implement the Moro algorithm for the inverse function of the cumulative normal distribution. Call the resulting function **norminv**.

The Moro algorithm proceeds as follows:

Suppose $x \in [0, 1]$. Define $y = x - 0.5$. If $|y| < 0.42$, define $r = y^2$ and approximate **norminv** with the following formula:

```
$y \frac{h_3(r, a_0, a_1, a_2, a_3)}{h_4(r, 1.0, b_1, b_2, b_3, b_4)}$.
```

We will define the constants $a_i$ and $b_i$ shortly.

Suppose $|y| >= 0.42$. If $y$ is negative let $r = x$. Otherwise let $r = 1 - x$. Define $s = \log(-\log(r))$. Define $t$ by

```
$t = h_8(s, c_0, c_1, \dots, c_8)$.
```

If $x > 0.5$, **norminv** is approximated by $t$, otherwise by $-t$.

Here is a table of values for the constants: