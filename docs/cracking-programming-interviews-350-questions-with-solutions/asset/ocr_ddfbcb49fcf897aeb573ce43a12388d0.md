# **Version 2**

# **Algorithm 92 Factorization Alternative Program**

```
    1: k ← n
    2: t ← 2
    3: while (k ≠ 1) do        ▷ the product of k and all number printed
        is equal to n; only prime numbers are printed; k has no divisors in
        (1,t)
    4:    if k mod t == 0 then    ▷ k is a multiple of t and has no
        divisors less than t; therefore, t is prime
    5:        k ← k ÷ t
    6:        print(t)
    7:    else                    ▷ k is not a multiple of t
    8:        t ← t + 1
    9:    end if
    10: end while
```

# ## 6.16 Factorization Revisited

# ### Problem Description

Solve the preceding problem taking into account the following fact: any composite number N has a factor not exceeding √N.

# ### Solution

In *version 2* of the above solution, replace t ← t + 1 by

# **Algorithm 93 Factorization Program Revisited**

```
    1: if t × t > k then
    2:    t ← k
    3: else
    4:    t ← t + 1
    5: end if
```

# ## 6.17 Decimal Representation

# ### Problem Description

Assume the command write(i) is allowed for i = 0,1,2,...,9. Write a program that prints the decimal representation of a given positive integer n.