(d) Since 6 < 8, hence copy 6 and increment indices of A and C

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 2 | 3 | 5 | 6 | | | | | | | |

(e) Since 9 > 8, hence copy 8 and increment indices of B and C

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 2 | 3 | 5 | 6 | 8 | | | | | | |

(f) Since 9 < 11, hence copy 9 and increment indices of A and C

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 2 | 3 | 5 | 6 | 8 | 9 | | | | | |

(g) Since 12 > 11, hence copy 11 and increment indices of B and C

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 2 | 3 | 5 | 6 | 8 | 9 | 11 | | | | |

(h) Since 12 < 15, hence copy 12 and increment indices of A and C

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 2 | 3 | 5 | 6 | 8 | 9 | 11 | 12 | | | |

(i) Since 14 < 15, hence copy 14 and increment indices of A and C

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 2 | 3 | 5 | 6 | 8 | 9 | 11 | 12 | 14 | | |

(j) Since 17 > 15, hence copy 15 and increment indices of B and C

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 2 | 3 | 5 | 6 | 8 | 9 | 11 | 12 | 14 | 15 | |

(k) Since the B array is empty, hence remaining element of A (i.e. 17) copy to C

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 2 | 3 | 5 | 6 | 8 | 9 | 11 | 12 | 14 | 15 | 17 |

Figure 3.8 (a-k): Merging two sorted arrays

# Algorithm to merge two sorted arrays

```
Algorithm: MERGE (A, B, M, N, C)
[A and B are two sorted arrays, M is the number of elements of A, N
is the number of elements of B and C is the resultant array]
1. Set I=0, J=0, K=0
2. Repeat while I<M and J<N
   if A[I]<B[J] then
      a) Set C[K]=A[I]
      b) Set I=I+1
      c) Set K=K+1
   ELSE
      a) Set C[K]=B[J]
      b) Set J=J+1
```