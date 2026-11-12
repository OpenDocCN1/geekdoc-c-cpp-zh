
## 6.6 Compute $a^n$

### Problem Description

Let $a$ be an integer and $n$ be a nonnegative integer. Compute $a^n$. In other words, we ask for a program that does not change the values of $a$ and $n$ and assigns the value $a^n$ to another variable (say, $b$). (The program may use other variables as well.)

### Solution

Consider an integer variable $k$, whose range is $0..n$. (We maintain the property: $b = a^k$.)

**Algorithm 81** Compute $a^n$ program

```text
1: k ← 0
2: b ← 1
3: while k ≠ n do
4:     k ← k + 1
5:     b ← b × a
6: end while
```

▷ $b = a^k$

### Alternative Solution

**Algorithm 82** Compute $a^n$ alternative program

```text
1: k ← n
2: b ← 1
3: while k ≠ 0 do
4:     k ← k − 1
5:     b ← b × a
6: end while
```

▷ $a^n = b × a^k$

## 6.7 Compute $a^n$ revisited

### Problem Description

Solve the preceding problem with the additional requirement that the number of execution steps should be of order $\log n$ (i.e., it should not exceed $C \log n$ for some constant $C$).

### Solution

Let us make some changes in the second solution of the preceding problem:

**Algorithm 83** Compute $a^n$ program revisited

```text
1: k ← n
2: b ← 1
3: c ← a
4: while k ≠ 0 do
5:     if k mod 2 = 0 then
6:         k ← k ÷ 2
7:         c ← c × c
8:     else
9:         k ← k − 1
10:        b ← b × c
11:    end if
12: end while
```

In both cases (even $k$ and odd $k$) the value of $k$ decreases; if $k$ is even, it is divided by 2; if $k$ is odd, after $k \leftarrow k - 1$ it becomes even and is divided by 2 during the next iteration. Therefore, after any two iterations $k$ becomes twice decreased (or even less), so the number of steps is logarithmic.

## 6.8 Compute the product $a \times b$

### Problem Description

Two nonnegative integers $a$ and $b$ are given. Compute the product $a \times b$ (only $+$, $−$, $=$ are allowed).

### Solution

**Algorithm 84** Compute the product $a \times b$

```text
1: k ← 0
2: c ← 0
3: while k ≠ b do                         ▷ invariant: c = a × k
4:     k ← k + 1
5:     c ← c + a
6: end while                              ▷ c = a × k and k = b, therefore c = a × b
```

## 6.9 Compute the quotient and remainder

### Problem Description

A nonnegative integer $a$ and a positive integer $d$ are given. Compute the quotient $q$ and the remainder $r$ when $a$ is divided by $d$. Do not use the operations div or mod.

### Solution

By definition, $a = q \times d + r$ and $0 \le r < d$.

**Algorithm 85** Compute the quotient and remainder

```text
1: r ← a        ▷ a ≥ 0; d > 0
2: q ← 0        ▷ invariant: a = q × d + r, 0 ≤ r
3: while !(r < d) do        ▷ r ≥ d
4:     r ← r − d        ▷ r ≥ 0
5:     q ← q + 1
6: end while
```

## 6.10 Compute GCD

### Problem Description

Two nonnegative integers $a$ and $b$ are not both zero. Compute GCD($a$, $b$), the greatest common divisor of $a$ and $b$.

### Solution

**Version 1**

**Algorithm 86** Compute GCD

```text
1: if a < b then
2:     k ← a
3: else
4:     k ← b
5: end if
6: Invariant: no numbers greater than k (and therefore than a or b) are common divisors
7: while !((a mod k == 0) && (b mod k == 0)) do
8:     k ← k − 1
9: end while        ▷ k is a common divisor, all larger k are not
```

**Version 2: Euclid's algorithm**

We assume that GCD(0, 0) = 0. Then GCD(a, b) = GCD(a − b, b) = GCD(a, b − a) with GCD(a, 0) = GCD(0, a) = a $\forall a, b \ge 0$. This property allows us to decrease $a$ and $b$ without changing GCD(a, b).

**Algorithm 88** Computed Constrained GCD

```text
1: m ← a
2: n ← b
3: p ← 1
4: q ← 0
5: r ← 0
6: s ← 1
7: Invariant: GCD(a,b) = GCD(m,n); m,n ≥ 0; m = p × a + q × b; n = r × a + s × b
8: while ((m ≠ 0) && (n ≠ 0)) do
9:     if m ≥ n then
10:         m ← m − n
11:         p ← p − r
12:         q ← q − s
13:     else
14:         n ← n − m
15:         r ← r − p
16:         s ← s − q
17:     end if
18: end while
19: if m = 0 then
20:     k ← n
21:     x ← r
22:     y ← s
23: else
24:     k ← m
25:     x ← p
26:     y ← q
27: end if
```

## 6.12 Alternative Euclid’ Algorithm

### Problem

Write a version of Euclid’s algorithm using the identities

$$\operatorname{GCD}(2a,2b)=2\times\operatorname{GCD}(a,b);$$
$$\operatorname{GCD}(2a,b)=\operatorname{GCD}(a,b)$$

for odd $b$.

The algorithm should avoid division (div and mod operations): only division by 2 and the test to be even are allowed. (The number of operations should be of order $\log k$ if both numbers do not exceed $k$.)

### Solution

**Algorithm 89** Alternative Euclid's Algorithm

```text
1: m ← a
2: n ← b
3: d ← 1                              ▷ GCD(a,b) = d × GCD(m,n)
4: while ((m ≠ 0) && (n ≠ 0)) do
5:   if m mod 2 == 0 && n mod 2 == 0 then
6:     d ← d × 2
7:     m ← m ÷ 2
8:     n ← n ÷ 2
9:   else if (m mod 2 == 0)&&(n mod 2 == 1) then
10:    m ← m ÷ 2
11:  else if (m mod 2 == 1)&&(n mod 2 == 0) then
12:    n ← n ÷ 2
13:  else if (m mod 2 == 1)&&(n mod 2 == 1) then
14:    if m ≥ n then
15:      m ← m − n
16:    else                              ▷ m < n
17:      n ← n − m
18:    end if
19:  end if
20: end while
    m = 0 ⇒ answer = d × n; n = 0 ⇒ answer = d × m
```

If both numbers $m$ and $n$ do not exceed $k$, the number of operations does not exceed $C \log k$; indeed, each other operation makes at least one of the numbers $m$ and $n$ twice smaller.

## 6.13 Revisit Constrained GCD

### Problem

Modify the solution of the preceding problem to find $x$ and $y$ such that $ax + by = \operatorname{GCD}(a, b)$.

### Solution

Assume that both $a$ and $b$ are even. In this case we divide both of them by 2; the values of $x$ and $y$ we are looking for remain unchanged. Therefore, without loss of generality, we may assume that at least one of the numbers $a$ and $b$ is odd. (This property will remain true.) As before, we wish to maintain the numbers $p,q,r,s$ such that

$$m = a \times p + b \times q$$
$$n = a \times r + b \times s$$

The problem, however, is that if we divide $m$ by 2 (say), then we should at the same time divide $p$ and $q$ by 2. In this case $p$ and $q$ are no longer integers but become finite binary fractions; that is, numbers of the type $r/2^i$. Such a number can be represented by a pair $\langle r,s\rangle$. As a result, we get $d$ as a linear combination of $a$ and $b$ with coefficients being finite binary fractions. In other words, we have

$$2^i \times d = a \times x + b \times y$$

for some integers $x$, $y$ and a positive integer $i$. What should we do if $i > 0$? If both $x$ and $y$ are even, we may divide them by 2 (and decrease $i$ by 1). If not, we apply the transformation:

$$x \leftarrow x + b$$
$$y \leftarrow y - a$$

(this transformation leaves $a \times x + b \times y$ unchanged). Let us see why this works. Recall that one of the numbers $a$ or $b$ is odd (according to our assumption). Let $a$ be odd. If $y$ is even, then $x$ is even as well (otherwise $x + y$ is odd); this case is considered above. If $a$ and $b$ are odd, then $y$ becomes even after executing the statement $y \leftarrow y-a$.

## 6.14 Compute Square using only addition and subtraction

### Problem Description

Write a program that prints the squares of the natural numbers $0,\ldots,n$ for a given $n \ge 0$, but only addition and subtraction are allowed. The number of steps should be of order $n$.

### Solution

We use the variable $ksquare$, and maintain the invariant relation $ksquare = k^2$:

**Algorithm 90** Compute Square using only addition and subtraction

```text
1:  k ← 0
2:  ksquare ← 0
3:  print(ksquare)
4:  while (k != n) do
5:      k ← k + 1        ▷ ksquare = (k − 1) × (k − 1) = k × k − 2 × k + 1
6:      ksquare ← ksquare + k + k − 1
7:      print(ksquare)
8:  end while
```

We can avoid subtraction by the following trick:

```text
1: while (k != n) do
2:     ksquare ← ksquare + k        ▷ ksquare = k × k + k
3:     k ← k + 1                       ▷ ksquare = (k − 1) × (k − 1) + (k − 1) = k × k − k
4:     ksquare ← ksquare + k
5: end while
```

## 6.15 Factorization

### Problem Description

Write a program that prints the factorization of a given integer $n > 0$. (In other words, it should print prime numbers whose product is equal to $n$; if $n = 1$, nothing should be printed.)

### Solution

**Version 1**

**Algorithm 91** Factorization Program

```text
1: k ← n
2: while !(k == 1) do    ▷ invariant relation: the product of k and all numbers printed is equal to n; only prime numbers are printed
3:     t ← 2
4:     while k mod t ≠ 0 do    ▷ invariant relation: k has no divisors in (1, t)
5:         t ← t + 1
6:     end while
7:     print(t)
8:     k ← k ÷ t
9: end while
```
