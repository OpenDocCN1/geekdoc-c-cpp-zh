
## Example 14.8 Find the solution for

```
$T(n) = 2T(n/2) + 5n^2; \quad T(1) = 7.$
```

For simplicity we assume that $n$ is a power of two, we can rewrite it as $n = 2^k$. This recurrence can be expanded as follows:

```
$T(n) = 2T(n/2) + 5n^2\n= 2T(n/4) + 5(n/2)^2 + 5n^2\n= 2(2T(n/8) + 5(n/4)^2 + 5(n/2)^2) + 5n^2\n= 2^k T(1) + 2^{k-1} \cdot 5(\frac{n}{2^{k-1}})^2 + \dots + 2 \cdot 5(\frac{n}{2})^2 + 5n^2.$
```

```
$7n + 5 \sum_{i=0}^{k-1} \frac{n^2}{2^i}\n= 7n + 5n^2 \sum_{i=0}^{k-1} 1/2^i.$
```

From Equation 2.6, we have:

```
$= 7n + 5n^2 (2-1/2^k)\n= 7n + 5n^2(2-2/n)\n= 7n + 10n^2 - 10n\n= 10n^2 - 3n.$
```

This is the *exact* solution to the recurrence for $n$ a power of two. At this point, we should use a simple induction proof to verify that our solution is indeed correct.

## Example 14.9 Our next example models the cost of the algorithm to build a heap. Recall from Section 5.5 to build a heap, we first heapify the two subheaps, push down the root to its proper position. The cost is:

```
$f(n) \le 2f(n/2) + 2 \log n.$
```

Let us find a closed form solution for this recurrence. We can expand the recurrence a few times to see that

$f(n) \le 2f(n/2) + 2\log n\n\le 2[2f(n/4) + 2\log n/2]\n\le 2[2f(n/8) + 2\log n/4] + 2\log n/2]$

We can deduce from this expansion that this recurrence is equivalent to following summation and its derivation:

```
$f(n) = \sum_{i=0}^{\log n-1} 2^{i+1}\log(n/2^i)\n=2\sum_{i=0}^{\log n-1} 2^i(\log n-i)\n=2\log n\sum_{i=0}^{\log n-1} 2^i - 4\sum_{i=0}^{\log n-1} i2^{i-1}\n=2n\log n-2\log n - 2n\log n + 4n-4\n=4n-2\log n - 4.$
```

## 14.2.3 Divide and Conquer Recurrences

The third approach to solving recurrences is to take advantage of known theorems that provide the solution for classes of recurrences. Of particular practical use is a theorem that gives the answer for a class known as **divide and conquer** recurrences. These have the

```
$T(n) = aT(n/b) + cn^k; \quad T(1) = c$
```

where $a, b, c,$ and $k$ are constants. In general, this recurrence describes a problem of size $n$ divided into $a$ subproblems of size $n/b$, while $cn^k$ is the amount of work necessary to combine the particular solution. Mergesort is an example of a divide and conquer algorithm, and its recurrence fits this form. So does binary search, we use the method of expanding recurrences to derive the general solution for any divide and conquer recurrence, assuming that $n=b^m$.

```
$T(n) = aT(n/b) + cn^k\n=a(aT(n/b^2) + c(n/b)^k) + cn^k\n=a(aT(n/b^3) + c(n/b^2)^k) + c(n/b)^k + cn^k$
```

We can summarize the above derivation as the following theorem, sometimes referred to as the **Master Theorem.**

## Theorem 14.1 (The Master Theorem) For any recurrence relation of the form
T(n) = aT(n/b) + cn^k, T(1) = c, the following relationships hold.

```
$$T(n) = \begin{cases} \Theta(n^{\log_b a}) & if \ a > b^k \\ \Theta(n^k \log n) & if \ a = b^k \ \Theta(n^k) & if \ a < b^k. \end{cases}$$
```

This theorem may be applied whenever appropriate, rather than re-deriving the solution for the recurrence.

## Example 14.10 Apply the Master Theorem to solve

```
$$T(n) = 3T(n/5) + 8n^2.$
```

Because $a = 3, b = 5, c = 8,$ and $k = 2$, we find that $3 < 5^2$. Applying case (3) of the theorem, $T(n) = \Theta(n^2)$.

## Example 14.11 Use the Master Theorem to solve the recurrence relation for Mergesort:

```
$$T(n) = 2T(n/2) + n; \quad T(1) = 1.$
```

Because $a = 2, b = 2, c = 1,$ and $k = 1$, we find that $2 = 2^1$. Applying case (2) of the theorem, $T(n) = \Theta(n \log n)$.

## 14.2.4 Average-Case Analysis of Quicksort

In Section 7.5, we determined the average-case analysis of Quicksort. This section presents the concept of amortized analysis, which deals with the cost of an operation over a sequence of operations. Rather than focusing on the worst-case of each operation independently, amortized analysis looks at the total cost of a whole sequence of operations. In particular, amortized analysis allows us to deal with the situation where some operations are expensive, but most are cheap.

In the following parts of this section, we will explore three techniques for analyzing amortized cost: the aggregate method, the accounting method, and the potential method.

### The Aggregate Method

The aggregate method analyzes the amortized cost of an operation by computing the total cost of a sequence of $n$ operations and dividing by $n$. Let $c_i$ be the cost of the $i$-th operation. The amortized cost of each operation is

$$ \frac{1}{n} \sum_{i=1}^n c_i $$

This method is used when all operations in the sequence are the same, but their actual costs vary. If we can find an upper bound on the total cost $\sum_{i=1}^n c_i$, then we have an upper bound on the amortized cost of each operation.

### The Accounting Method

The accounting method (also known as the physicist method) assigns an "amortized cost" to each operation. If the amortized cost is greater than the actual cost, the difference is stored as "credit" associated with certain data structures. When an operation costs more than its amortized cost, the stored credit is used to pay for the excess cost. The goal is to ensure that the total credit never drops below zero, which means the total amortized cost upper-bounds the total actual cost.

### The Potential Method

The potential method uses a potential function $\Phi$ to represent the "stored energy" of the data structure. The amortized cost $\hat{c}_i$ of the $i$-th operation is defined as

$$ \hat{c}_i = c_i + \Phi(D_i) - \Phi(D_{i-1}) $$

where $c_i$ is the actual cost, $D_i$ is the state of the data structure after the $i$-th operation, and $D_{i-1}$ is the state before it. The total amortized cost of $n$ operations is

$$ \sum_{i=1}^n \hat{c}_i = \sum_{i=1}^n c_i + \Phi(D_n) - \Phi(D_0) $$

If $\Phi(D_i) \ge \Phi(D_0)$ for all $i$, then the total amortized cost is an upper bound on the total actual cost.

## Example: Binary Counter

Consider an $n$-bit binary counter initialized to all zeros. Each increment operation flips bits starting from the least significant bit to the most significant. For example:

- 000 -> 001
- 001 -> 010
- 010 -> 011
- 011 -> 100

We use the aggregate method to analyze this. We define the cost of an operation as the number of bits flipped. Each bit flip takes $O(1)$ time.

Let $c_i$ be the number of bits flipped during the $i$-th increment. The first bit is flipped every increment, the second bit is flipped every 2 increments, the third bit every 4 increments, and so on. The $j$-th bit is flipped every $2^{j-1}$ increments.

The total cost of $n$ increments is

$$ \sum_{i=1}^n c_i = \sum_{j=1}^n \lfloor \frac{n}{2^{j-1}} \rfloor < \sum_{j=1}^\infty \frac{n}{2^{j-1}} = 2n $$

The amortized cost per operation is $2n/n = 2$, which is $O(1)$.

Now we use the accounting method. We assign an amortized cost of 2 to each increment. 1 unit pays for flipping the 0 that is turned to 1, and 1 unit is stored as credit on the bit that was just set to 1. When we need to flip a 1 back to 0, we use the stored credit to pay for it. Since each increment flips exactly one 0 to 1, we always have enough credit to cover the flipping of any many 1s. Thus, the amortized cost is $O(1)$.

Finally, we use the potential method. Let $\Phi(D)$ be the number of 1s in the counter. The amortized cost is

$$ \hat{c}_i = c_i + \Phi(D_i) - \Phi(D_{i-1}) $$

If the increment flips $k$ ones to 0 and then one zero to 1, then $c_i = k+1$. The change in 1s is $\Phi(D_i) - \Phi(D_{i-1}) = 1-k$.

$$ \hat{c}_i = (k+1) + (1-k) = 2 $$

The amortized cost is $O(1)$.

