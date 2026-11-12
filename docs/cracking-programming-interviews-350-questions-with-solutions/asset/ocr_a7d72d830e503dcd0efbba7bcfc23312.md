# ## 2.23 Find a number not sum of subsets of array

# ### Problem Description

A non-decreasing integer array $a[1..n]$ contains positive numbers only. Find the minimal positive integer that cannot be represented as a sum of several elements of this array (no element may be used more than once). The number of operations should be of order $n$.

# ### Solution

Assume all numbers that can be represented as sums of subsets of ${a[1],...,a[k]}$ form the set ${1,2,...,N}$ for some $N$. If $a[k+1]$ is greater than $N+1$, then $N+1$ is the smallest number that cannot be represented as a sum of some subsets of ${a[1],...,a[k]}$. If $a[k+1] \leq N+1$, then all numbers that can be represented as sums of subsets of ${a[1],...,a[k+1]}$ form the set ${1,2,...,N+a[k+1]}$.

```
Algorithm 60 Find a number not sum of subsets of array

1: $k \leftarrow 0$
2: $N \leftarrow 0$
3: Invariant: all the numbers that can be represented as sums of subsets of ${a[1],...,a[k]}$, form the set ${1,2,...,N}$
4: while $k+1 \leq n$ and $a[k+1] \leq N+1$ do
5:     $N \leftarrow N+a[k+1]$
6:     $k \leftarrow k+1$
7: end while ▷ $(k=n)$ or $(a[k+1]>N+1)$; the answer is $N+1$ in both cases
8: print$(N+1)$
```

# ## 2.24 $k^{th}$ Smallest Element in Two Sorted Arrays

# ### Problem Description

Given two sorted arrays $a[1..n]$ and $b[1..m]$, find the $k^{th}$ smallest element in the union of the two arrays. Time Complexity should be $O(\log n + \log m)$.

# ### Solution

We are searching for the $k^{th}$ smallest element $x_k$ in the union of the arrays $a[1,...,n]$ and $b[1,...,m]$.

Because we are looking at the $k^{th}$ smallest element, we can restrict our attention to the arrays $a[1,...,k]$ and $b[1,...,k]$. If $k>m$ or $k>n$, we can take all the elements with index larger than $k$ in the array boundary to have infinite value.