# ### Algorithm 56 Median Search

```
~~~
1: function MEDIAN-BIN-SEARCH(A, B: sorted arrays, l, r: integers)
2:     if l > r then
3:         return -1
4:     end if
5:     i ← ⌊(l+r)/2⌋
6:     j ← ⌊m/2⌋ − i + 1
7:     if B[j] ≤ A[i] ≤ B[j+1] then
8:         return i
9:     end if
10:    if A[i] < B[j] then
11:        MEDIAN-BIN-SEARCH(A, B, l, i)
12:    end if
13:    if A[i] > B[j+1] then
14:        MEDIAN-BIN-SEARCH(A, B, i + 1, r)
15:    end if
16: end function
~~~
```

A not too formal proof of correctness of COMMON-MEDIAN is simply pointing out the preceding discussion and knowing that the binary search idea is correct. The time complexity is obviously Θ(log m). Alternatively, we can say the complexity is Θ(max{log p, log q}).

# ## 2.18 Finding the missing integer

# ### Problem Description

An array A[1, . . . , n] contains all the integers from 0 to n except one. It would be easy to determine the missing integer in *O(n)* time by using an auxiliary array B[0, . . . , n] to record which numbers appear in A. In this problem, however, we cannot access an entire integer in A with a single operation. The elements of A are represented in binary, and the only operation we can use to access them is fetch the j-th bit of A[i], which takes constant time. Show that if we use only this operation, we can still determine the missing integer in *O(n)* time.

# ### Solution

# ### Analysis

Let m be the number of bits required to represent n in binary. It is well known that m = ⌊log₂ n⌋ + 1. In this problem we think of A as an m × n, 0-1 matrix. Row number m of A consists of the least significant bits of the numbers in A, row number m − 1 consists of the second least significant bits, etc., row number 1 consists of the most significant bits.