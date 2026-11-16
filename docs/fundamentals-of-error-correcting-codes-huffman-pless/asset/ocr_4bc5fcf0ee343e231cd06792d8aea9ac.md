# # 1.8 Hamming codes

We now generalize the binary code H3 of Example 1.2.3. The parity check matrix obtained in that example was

\( H = [A^\top | I_3] = \begin{bmatrix} 0 & 1 & 1 & 1 & 1 & 0 & 0 \\ 1 & 0 & 1 & 1 & 0 & 1 & 0 \\ 1 & 1 & 0 & 1 & 0 & 0 & 1 \end{bmatrix} . \)

Notice that the columns of this parity check matrix are all the distinct nonzero binary columns of length 3. So H3 is equivalent to the code with parity check matrix

\( H' = \begin{bmatrix} 0 & 0 & 0 & 1 & 1 & 1 & 1 \\ 0 & 1 & 1 & 0 & 0 & 1 & 1 \\ 1 & 0 & 1 & 0 & 1 & 0 & 1 \end{bmatrix} \)

whose columns are the numbers 1 through 7 written as binary numerals r (with leading 0s as necessary to have a 3-tuple) in their natural order.

This form generalizes easily. Let n = 2^r - 1, with r >= 2. Then the r x (2^r - 1) matrix Hr, whose columns, in order, are the numbers 1, 2, ... , 2^r - 1 written as binary numerals, is the parity check matrix of an [n = 2^r - 1, k = n - r] binary code. Any rearrangement of columns of Hr gives an equivalent code, and hence any one of these equivalent codes will be called the **binary Hamming code** of length n = 2^r - 1 and denoted by either Hr or H_{n,r}. It is customary when naming a code, such as the Hamming code, the tetracode, or the hexacode, to identify equivalent codes. We will follow this practice with these and other codes as well.

Since the columns of Hr are distinct and nonzero, the minimum distance is at least 3 by Corollary 1.4.14. Since the columns corresponding to the numbers 1, 2, and 3 are linearly dependent, the minimum distance equals 3, by the same corollary. Thus Hr is a binary [2^r - 1, 2^r - 1 - r, 3] code. In the following sense, these codes are unique.

**Theorem 1.8.1** Any [2^r - 1, 2^r - 1 - r, 3] binary code is equivalent to the binary Hamming code Hr.

**Exercise 55** Prove Theorem 1.8.1. \(\unknown\)

**Exercise 56** Prove that every [8, 4, 4] binary code is equivalent to the extended Hamming code H~3~. (So for that reason, we say that the [8, 4, 4] binary code is unique.) \(\unknown\)

Similarly, Hamming codes H_{q,r} can be defined over an arbitrary finite field F_q. For r >= 2, H_{q,r} has parity check matrix H_{q,r}, defined by choosing for its columns a nonzero vector from each 1-dimensional subspace of F_q^r. (Alternately, these columns are the points of the projective geometry PG(r - 1, q). There are (q^r - 1)/(q - 1) 1-dimensional subspaces. Therefore H_{q,r} has length n = (q^r - 1)/(q - 1), dimension n - r, and redundancy r. As no two columns are multiples of each other, H_{q,r} has minimum weight at least 3. Adding