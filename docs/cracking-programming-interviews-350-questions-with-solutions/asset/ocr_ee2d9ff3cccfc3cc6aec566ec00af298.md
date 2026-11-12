# ### Algorithm 106 Exchange Prefix and Suffix

```
    1: p ← 0
    2: q ← m
    3: r ← m + n
    4: while (p ≠ q) and q ≠ r do        ▷ invariant relation: it remains to
    5:     exchange x[p + 1..q], x[q + 1..r]        ▷ both segments are nonempty
    6:     if (q − p) ≤ (r − p) then       ▷ exchange x[p + 1..x[q] and
    7:         p_new ← q
    8:         q_new ← q + (q − p)
    9:         x[q + 1..x[q + (q − p)]]
    10:         q ← q_new
    11:     else        ▷ exchange x[q − (r − q) + 1..x[q] and x[q + 1..x[r]
    12:         q_new ← q − (r − q)
    13:         r_new ← q
    14:         q ← q_new
    15:         r ← r_new
    16:     end if
    17: end while
```

The number of operations may be estimated as follows. At each step the part of the array that should be processed becomes shorter by the length of A. The number of operations required is also proportional to the length of A.