# **Algorithm 48** Circular Racecourse Program

```
```
1: n ← 1
2: f[0] ← 0
3: l ← 1
4: xx ← 0
5: x ← 0
6: while n ≠ N do
7:   x ← x + p[n−1] − q[n−1]
8:   if x > xx then
9:     skip
10:  else if x == xx then
11:    f[l] ← n
12:    l ← l+1
13:  else if x < xx then
14:    xx ← x
15:    f[0] ← n
16:    l ← 1
17:  end if
18:  n ← n+1
19: end while
```
```

# **Remarks**

The above program is such that, when under execution, the elements $p[N-1]$ and $q[N-1]$ of the arrays $p$ and $q$ are never inspected.

One of the outcomes of the above analysis is that the condition $∑_{i=0}^{N−1} p[i] = ∑_{i=0}^{N−1} q[i]$ is a sufficient condition for the existence of at least one pit from which a car can round the circuit.

# ## 2.12 Sparse Array Trick

# **Problem**

Suppose you want to use a large array $A$ for random access, although you won’t actually be referring to very many of its entries. You want $A[k]$ to be zero the first time you access it, yet you don’t want to spend the time to set every location to zero. Explain how it is possible to read and write any desired element $A[k]$ reliably, given $k$, without assuming anything about the actual initial memory contents, by doing only a small fixed number of additional operations per array access.