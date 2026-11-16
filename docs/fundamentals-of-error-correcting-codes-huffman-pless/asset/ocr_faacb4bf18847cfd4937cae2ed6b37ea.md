Lemma 10.3.4 The following hold for columns of (10.4):
(i) Given \( a \in \mathbb{F}_4 \), there are exactly four possible choices for a column that projects to \( a \). Exactly two choices have even parity and two odd parity. The two of even parity are complements of each other, as are the two of odd parity.
(ii) The columns projecting to \( 0 \in \mathbb{F}_4 \) are [0000]^T, [1111]^T, [1000]^T, and [0111]^T.

Exercise 582 Prove Lemma 10.3.4.

Lemma 10.3.5 Let C be the binary code consisting of all vectors c such that:
(i) all columns of [c] have the same parity and that parity equals the parity of the first row of [c], and
(ii) the vector Pr(c) \in G_6.
The code C is the [24, 12, 8] extended binary Golay code.

Proof: If we fill in the first three rows of the matrix (10.4) arbitrarily, then the last row is uniquely determined if (i) is to be satisfied. The set of vectors satisfying (i) is clearly a linear space. Hence the set of vectors C_1 satisfying (i) is a [24, 18] code. Similarly, if we fill in the first three columns of the matrix (10.4) arbitrarily, then these columns project onto three arbitrary elements of F_4. Since the first three coordinates of the hexacode are the three information positions, the last three coordinates of the projection are uniquely determined if (ii) is to be satisfied. But there are precisely four choices for a column if it is to project to some fixed element of F_4. Thus the set of vectors satisfying (ii) has size 2^{14} = 2^{18}. This set C_2 is clearly a linear space as Pr is a linear map and G_6 is closed under addition. Thus C_2 is also a [24, 18] code. Therefore C = C_1 \cap C_2 has dimension at least 12.

By Theorem 10.1.6, the proof is completed if we show that C has minimum distance 8. The vector 111111100...0 satisfies (i) and projects onto the zero vector. Hence C has minimum distance at most 8. Suppose c \in C is a nonzero codeword. There are two cases: the top row of [c] has even parity or the top row has odd parity.

Suppose that the top row of [c] has even parity. If Pr(c) \neq 0, then as G_6 has minimum weight 4, there are at least four nonzero columns in [c] all with a (nonzero) even number of 1s. Therefore wt(c) \geq 8. Suppose now that Pr(c) = 0. The only column vectors of even number that project to 0 \in F_4 are the all-zero column and the all-one column. Since the top row of [c] has even parity, [c] must contain an even number of all-one columns. As c \neq 0, we again have wt(c) \geq 8.

Suppose now that the top row of [c] has odd parity. Thus every column of [c] has an odd number of 1s and so there are at least six 1s in [c]; we are done if one column has three 1s. So assume that every column of [c] has exactly one 1. In particular, the top row of [c] has a 1 in a given column precisely when that column projects to 0 \in F_4. Thus the number of 1s in the top row is 6 - wt(Pr(c)). However, the codewords of G_6 have even weight and so the top row of [c] has even parity, which is a contradiction.

For the remainder of this section the code C in Lemma 10.3.5 will be denoted G_{24}. In order to decode G_{24} by hand, we need to be able to recognize the codewords in G_6. If we label the coordinates by 1, 2, 3, 4, 5, 6, then the coordinates break into pairs (1, 2), (3, 4), and (5, 6). There are permutation automorphisms that permute these three pairs in any manner and switch the order within any two pairs; see Exercise 583. We list the codewords