Program Code 10.1 is the implementation of the OBST construction through the dynamic approach we just discussed. Let us see its working with Example 10.2.

# EXAMPLE 10.2 Find an OBST using a dynamic programming for n = 4 and keys (k1 < k2 < k3 < k4) = (do, if, int, while) given that p(1:4) = (3, 3, 1, 1) and q(0:4) = (2, 3, 1, 1, 1).

# Solution

Step 1 Initially, c(i, i) = 0, r(i, i) = 0, and w(i, i) = q(i) for 0 <= i <= 4. Hence, w(0, 0) = 2, w(1, 1) = 3, w(2, 2) = w(3, 3) = w(4, 4) = 1 This is shown in Table 10.1

| | 0 | 1 | 2 | 3 | 4 | Initial values |
|---|---|---|---|---|---|---|
| 0 | w00 = 2
w00 = 0
r00 = 0 | w11 = 3
w11 = 0
r11 = 0 | w22 = 1
w22 = 0
r22 = 0 | w33 = 1
w33 = 0
r33 = 0 | w44 = 1
w44 = 0
r44 = 0 | <- |
| 1 | | | | | | |
| 2 | | | | | | |
| 3 | | | | | | |
| 4 | | | | | | |

Step 2: w(i, j) = p(j) + q(j) + w(i, j - 1)

```
c(i, j) = min
i < a <= j [c(i, a - 1) + c(a, j) + w(i, j)]
r = (i, j) = value of a which minimizes c(i, j)
Let us compute c(i, j) for j - i = 1
w(0, 1) = p(1) + q(1) + w(0, 0)
= 3 + 3 + 2 = 8
c(0, 1) = w(0, 1) + min[c(0, 0) + c(1, 1)] for a = 1
= 8 + [0 + 0] = 8
r(0, 1) = 1
w(1, 2) = p(2) + q(2) + w(1, 1) = 3 + 1 + 3 = 7
c(1, 2) = w(1, 2) + min[c(1, 1) + c(2, 2)] = 7 + [0 + 0] = 7 for a = 2
```