```
```text
Algorithm 83  Compute a^n program revisited
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
```

In both cases (even k and odd k) the value of k decreases; if k is even, it is divided by 2; if k is odd, after k ← k − 1 it becomes even and is divided by 2 during the next iteration. Therefore, after any two iterations k becomes twice decreased (or even less), so the number of steps is logarithmic.

# 6.8  Compute the product a × b

# Problem Description

Two nonnegative integers a and b are given. Compute the product a × b (only +, −, = are allowed).

# Solution

```
```text
Algorithm 84  Compute the product a × b
1: k ← 0
2: c ← 0
3: while k ≠ b do                         ▷ invariant: c = a × k
4:     k ← k + 1
5:     c ← c + a
6: end while                              ▷ c = a × k and k = b, therefore c = a × b
```
```

# 6.9  Compute the quotient and remainder

# Problem Description

A nonnegative integer a and a positive integer d are given. Compute the quotient q and the remainder r when a is divided by d. Do not use the operations div or mod.