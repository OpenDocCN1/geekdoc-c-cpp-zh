# 316

# Chap. 9 Searching

We now show that this is the same as

$$\sum_{\sqrt{n}} P(\text{need at least } i \text{ probes})$

$= 1 + (1 - P_1) + (1 - P_2) + \cdots + P_{\sqrt{n}}$$\n$= (P_1 + \cdots + P_{\sqrt{n}}) + (P_2 + \cdots + P_{\sqrt{n}}) +$\n$( (P_3 + \cdots + P_{\sqrt{n}}) + \cdots)$$\n= 1P_1 + 2P_2 + 3P_3 + \cdots + \sqrt{n}P$

We require at least two probes to set the bounds, so the cost is

$$\sum_{i=3} P(\text{need at least } i \text{ probes})$

We now take advantage of a useful fact known as Čebyšev's Inequality.\nČebyšev's inequality states that $P(\text{need exactly } i \text{ probes})$, or $P_i$, is

$P_i \leq \frac{p(1-p)n}{(i-2)^2n} \leq \frac{1}{4(i-2)^2}$

because $p(1-p) \leq 1/4$ for any probability $p$. This assumes uniformly distributed$\ndata. The expected number of probes is

$$\sum_{i=3} \frac{1}{4(i-2)^2} < 2 + \sum_{i=1} \frac{1}{i^2} = 2 + \frac{\pi}{6} \approx 2.4112$

IS better than binary search? Theoretically, yes grows $O(\log n)$$\ngrows slower than $O(\log n)$. However, we have a situation here that illustrates$\nthe limits to the model of asymptotic complexity in practical situations. Yes,\nc_1$ $\log n$ does grow faster than $c_2$ $\log n$. In fact, it is exponentially faster!$\neven so, for practical input sizes, the absolute difference is fairly small. Thus,\nt constant factors might play a role. First we compare $\lg n$ to $\log n$.

| $n$ | $\lg n$ | $\lg lg n$ | Difference |
|---|---|---||}{
| 16 | 4 | 2 | 2 |
| 256 | 8 | 3 | 2.7 |
| $2^{16}$ | 16 | 4 | 4 |
| $2^{32}$ | 32 | 5 | 6.4 |