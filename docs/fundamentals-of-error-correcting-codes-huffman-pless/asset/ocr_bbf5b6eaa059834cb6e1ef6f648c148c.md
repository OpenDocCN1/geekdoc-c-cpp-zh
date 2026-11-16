the right-most \( n - n' \) coordinates to form the code \( C' \) of length \( n' \) with \( M' \ge M/q^{n-n'} \) codewords, noting that distinct codewords in \( C \) remain distinct in \( C' \); the minimum distance of \( C' \) is at least that of \( C \) by our construction. This \( (n', M', \delta n) \) code satisfies \( rn' < \delta n \) by our choice of \( n' \). Applying the Plotkin Bound to \( C' \) gives

```
\(\frac{M}{q^{n-n'}} \le M' \le \frac{\delta n}{\delta n - rn'} \le \delta n,\)
```

as \( \delta n - rn' \ge 1 \). Then \( A_q(n, \delta n) = M \le q^{n-n'} \delta n \) and so

```
\(\alpha_q(\delta) \le \limsup_{n \to \infty} n^{-1} \log_q A_q(q^{n-n'} \delta n)\)
```

```
\(= \limsup_{n \to \infty} \left( 1 - \frac{n'}{n} + \frac{\log_q \delta}{n} + \frac{\log_q n}{n} \right)\)
```

```
\(= \lim_{n \to \infty} \frac{n'}{n} = 1 - \frac{\delta}{r}.\)
```

This completes the proof.

**Exercise 134** Draw the graphs of the inequalities given by the Asymptotic Singleton and Asymptotic Plotkin Bounds when \( q = 2 \), where the horizontal axis is the relative distance \( \delta \) and the vertical axis is the rate \( R = \alpha_q(\delta) \). Why is the Asymptotic Plotkin Bound stronger than the Asymptotic Singleton Bound? Repeat this for the cases \( q = 3 \) and \( q = 4 \). \(\unknown\)

# **2.10.3 Asymptotic Hamming Bound**

By the Asymptotic Plotkin Bound, when bounding \( \alpha_q(\delta) \) we can assume that \( 0 \le \delta \le r = 1 - q^{-1} \) as otherwise \( \alpha_q(\delta) = 0 \). There is an asymptotic bound derived from the Hamming Bound (Sphere Packing Bound) that is superior to the Asymptotic Plotkin Bound on an interval of values for \( \delta \). In order to derive this bound, we define the *Hilbert entropy function* on \( 0 \le x \le r \) by

```
\(H_\delta(x) = \begin{cases} 0 & \text{if } x = 0, \\ x \log_q(q-1) - x \log_q x - (1-x) \log_q(1-x) & \text{if } 0 < x \le r. \end{cases}\)
```

We will need to estimate factorials; this can be done with Stirling's Formula [115, Chapter 9], one version of which is

```
\(n^{n+1/2} e^{-n+7/8} \le n! \le n^{n+1/2} e^{-n+1}.\)
```

The results of Exercises 135 and 136 will also be needed.

**Exercise 135** Let \( 0 \le \delta \le 1 - q^{-1} \).
(a) Show that \( n \log_q n - \lfloor \delta n \rfloor \log_q \lfloor \delta n \rfloor - (n - \lfloor \delta n \rfloor) \log_q (n - \lfloor \delta n \rfloor) \le -(\delta n - 1) \times \log_q (\delta - \frac{1}{n}) + \log_q n - n(1 - \delta) \log_q (1 - \delta) \) when \( \delta n > 2 \). Hint: \( (\delta - (1/n))n = \delta n - 1 \le \lfloor \delta n \rfloor \le \delta n \).
(b) Show that \( n \log_q n - \lfloor \delta n \rfloor \log_q \lfloor \delta n \rfloor - (n - \lfloor \delta n \rfloor) \log_q (n - \lfloor \delta n \rfloor) \ge -\log_q n - \delta n \log_q (\delta - \delta n + 1) \log_q (1 - \delta + 1/(n)) \) when \( \delta n \ge 1 \). Hint: \( n - \lfloor \delta n \rfloor \le n - (\delta - (1/n))n \) and \( \lfloor \delta n \rfloor \le \delta n \).