mation when use was called. LRU does indeed stand for *least recently used*.

# **6.28 Exchange Prefix and Suffix**

# **Problem Description**

An array x[1]..x[m+n] is considered as a concatenation of two segments: a *prefix* x[1]..x[m] of length m and a *suffix* x[m+1]..x[m+n] of length n. Without using other arrays, exchange these *prefix* and *suffix* segments. (The number of operations should be of order m+n.)

# **Solution**

# **Version 1**

Reverse the prefix segment, then the suffix segment, and finally the whole array.

# **Version 2**

Imagine that the array is written down along a circle. Then the required transformation is a rotation. Recall that rotation may be represented as the composition of two axial symmetries. Each symmetry can be performed by exchanges without extra memory.

# **Version 3**

Consider a more general problem: Exchange two adjacent segments x[p + 1]..x[q] and x[q + 1]..x[r] in an array. Assume that the length of the left segment (called A in the sequel) does not exceed the length of the right segment (called B). Split B into two segments B1 and B2, where B1 is an initial segment of B of the same length as A. (So, B = B1 + B2, where + stands for concatenation.) We need to transform A + B1 + B2 into B1 + B2 + A. We can easily exchange A and B1 because they have equal lengths. After that we get B1 + A + B2 and it remains to exchange A and B2. Therefore, we have reduced our problem to a similar one for shorter segments. Here is the outline of the program: