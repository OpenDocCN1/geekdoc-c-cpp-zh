Now, for any value $n$ exists $k$ and $l$ such that

$n = km + l \text{ where } m > l \geq 0. $

From the definition of the mod function, we can derive the fact that

$n = |n/m|m + n \bmod m. $

Since the LCF is a factor of both $n$ and $m$, and since $n = km + l$, the LCF must therefore be a factor of both $km$ and $l$, and also the largest common factor of each of these terms. $LCF(n,m) = LCF(m,l) = LCF(m,n \bmod m). $

This observation leads to a simple algorithm. We will assume that $n \geq m$. At each iteration we replace $n$ with $m$ and $m$ with $n \bmod m$ until we have driven $m$ to zero.

```
int LCF(int n, int m) {
    if (m == 0) return n;
    return LCF(m, n % m);
}
```

To determine how expensive this algorithm is, we need to know how much progress we are making at each step. Note that after two iterations, we have replaced $n$ with $n \bmod m$. So the key question becomes: How is $n \bmod m$ relative to $n?

+   $n \geq m \Rightarrow n/m \geq 1$\n$\Rightarrow 2[n/m] > n/m$\n$\Rightarrow m[n/m] > n/2$\n$\Rightarrow n/2 > n - m[n/m] = n \bmod m$\n$\Rightarrow n/2 > n \bmod m$

Thus, function LCF will halve its first parameter in no more than 2 iterations. The total cost is $O(\log n)$.

# 16.3.3 Matrix Multiplication

The standard algorithm for multiplying two $n \times n$ matrices requires $\Theta(n^3)$ time. It is possible to do better than this by rearranging and grouping the multiplications in various ways. One example of this is Strassen's matrix multiplication algorithm.

For simplicity, we will assume that $n$ is a power of two. In the following, $A$ and $B$ are $n \times n$ arrays, $A_{ij}$ and $B_{ij}$ refer to arrays of size $n/2 \times n/2$. Using