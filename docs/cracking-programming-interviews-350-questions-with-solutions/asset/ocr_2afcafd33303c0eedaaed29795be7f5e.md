$A.p.(n+1) ≡ (∀i : p ≤ i < n+1 : X.i = 0) ≡ (∀i : p ≤ i < n : X.i = 0) ∧ X.n = 0 ≡ A.p.n ∧ X.n = 0$

Hence,

$Q ∧ X.n = 0 ⇒ Q(n ← n+1)$

and

$X.n ≠ 0 ⇒ (∀p : s ≤ p ≤ n : ¬A.p.(n+1))$

from which we infer, since $A.(n+1).(n+1)$ holds

$X.n ≠ 0 ⇒ Q(n ← n+1)(s ← n+1)$

This leads to the following solutions to all zeros:

# Algorithm 18 All Zeros Program

```
```text
1: n, s : int
2: n ← 0
3: r ← 0
4: s ← 0
5: while n ≠ N do
6:     if X.n == 0 then
7:         skip
8:     else if X.n ≠ 0 then
9:         s ← n + 1
10:    end if
11:    r ← r max (n + 1 - s)
12:    n ← n + 1
13: end while
```
```

Please note that we did not use the postfix-closedness of $A$.

# 1.12 Exponentiation

# Problem Description

Write a program that, given two fixed integers $X ≥ 0$ and $Y ≥ 0$, establishes $z = X^Y$.

# Solution

Let us define $0^0 = 1$. The program is to consist of a loop with the following invariant and bound functions:

+   - $P : 0 ≤ y ∧ z × x^y = X^Y$.
+   - $t : y$