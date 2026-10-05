488

Chap. 14 Analysis Techniques

# 14.5 Use the shifting method to solve the summation

$$\sum_{i=1}^{n} i^2.$

# 14.6 Use the shifting method to solve the summation

$$\sum_{i=1}^{n} 2^i.$

# 14.7 Use the shifting method to solve the summation

$$\sum_{i=1}^{n} 2^{n-i}.$

# 14.8 Consider the following code fragment.

```
sum = 0; inc = 0;
for (i=1; i<=n; i++)
  for (j=1; j<=i; j++) {
    sum = sum + inc;
  inc++;
}
```

+   (a) Determine a determination that defines the final value for variable sum as a function of n.

+   (b) Determine a closed-form solution for your summation.

14.9 A company decides to promote its chocolate bars by including a coupon with each bar. A bar costs $d$, and with $c$ coupons you get a free bar. Depending on the value of $c$, you get more than one bar of chocolate for a dollar when considering the value of the coupons. How much chocolate is a dollar worth (as a function of $c$)?

14.10 Write and solve a recurrence relation to compute the number of times Fib is called in the Fib of Exercise 2.11.

14.11 Give and prove the closed-form solution for the recurrence relation $T(n) = T(n-1) + 1, T(1) = 1$.

14.12 Give and prove the closed-form solution for the recurrence relation $T(n) = T(n-1) + c, T(1) = c$.

14.13 Prove by induction that the closed-form solution for the recurrence relation

$T(n) = 2T(n/2) + n; \ T(2) = 1$

is in $\Omega(n \log n)$.