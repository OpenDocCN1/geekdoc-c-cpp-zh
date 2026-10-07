# ERRORS

$p_1 > p_2$ and then shift $x_2$ to the form

```
$x_2 = 0.0 \cdots 0b_{21} \cdots b_{2m} 2^{p_1}$
```

with $p_1 - p_2 -1$ bits being counted from the first bit on the right side of the decimal. The sum or difference can now be computed through binary addition or subtraction of the original $x_1$ and shifted $x_2$ significands with the result being rounded to $m$ bits to the right of the decimal. There are practical considerations that arise in terms of how to store the shifted version of $x2$ and problems arise if only $m$ decimal bits are used to store the shifted value. Guard bits (e.g., Kaneko and Liu 1991) can be used to deal with such issues.

# 2.5 Errors

As in the last section, most numbers cannot be represented exactly in floating-point format. In this section we will explore the consequences of the precision of computations that are carried out in binary arithmetic.

First let us address the losses that can arise from conversion of a number to its floating-point representation. It is possible to place bounds on the amount of error that can be incurred. The bounds are, of course, depending on the type of “rounding” that is employed. The simplest approach is truncation or chopping.

Sign plays no real role in development. So, suppose that $x$ is a positive real number that can be written

```
$x = \sum_{j=0}^{\infty} b_j 2^{p-j}$
```

with $b_0 = 1$. Then, *chopping* replaces $x$ by the approximation

```
$\tilde{x} = 2^p + \sum_{j=1}^{m} b_j 2^{p-j}$
```

for some integer $m$. The error that is incurred by this approach is

```
$x - \tilde{x} = \sum_{j=m+1}^{\infty} b_j 2^{p-j} \nle 2^p \sum_{j=m+1}^{\infty} 2^{-j} \n = 2^{p-(m+1)} \sum_{j=0}^{\infty} 2^{-j} \n = 2^{p-m}$.
```

Instead of choosing an alternative approximation $	ilde{x}$ can be produced by rounding to the value that is closest to $x$ in the sense of minimizing $|x - \tilde{x}|$. The cut cuts the bound in half for $2^{p-(m+1)}$ as we now demonstrate.

First observe that the *round-to-close* value for $	ilde{x}$ is obtained by increasing $b_m$ by one if $b_{m+1}=1$ and using the chopped approximation otherwise. Consequently,

```
$\tilde{x} = 2^p \sum_{j=0}^{m} b_j 2^{p-j} + b_{m+1} 2^{-(m+1)}]$
```

with $\hat{b}_{m+1}$ being either two or zero depending on whether or not $b_{m+1}$ is 1 or 0, respectively.