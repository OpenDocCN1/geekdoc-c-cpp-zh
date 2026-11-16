Corollary 1.4.14 A linear code has minimum weight d if and only if its parity check matrix has a set of d linearly dependent columns but no set of d - 1 linearly dependent columns.

Exercise 21 Prove Theorem 1.4.13 and Corollary 1.4.14.

The minimum weight is also characterized in the following theorem.

Theorem 1.4.15 If C is an [n, k, d] code, then every n - d + 1 coordinate position contains an information set. Furthermore, d is the largest number with this property.

Proof: Let G be a generator matrix for C, and consider any set X of s coordinate positions. To make the argument easier, we assume X is the set of the last s positions. (After we develop the notion of equivalent codes, the reader will see that this argument is in fact general.) Suppose X does not contain an information set. Let G = [A | B], where A is k x (n - s) and B is k x s. Then the column rank of B, and hence the row rank of B, is less than k. Hence there exists a nontrivial linear combination of the rows of B which equals 0, and hence a codeword c which is 0 in the last s positions. Since the rows of G are linearly independent, c != 0 and hence d <= n - s, equivalently, s <= n - d. The theorem now follows.

Exercise 22 Find the number of information sets for the [7, 4] Hamming code H3 given in Example 1.2.3. Do the same for the extended Hamming code H~3 from Example 1.3.2.

# 1.5 New codes from old

As we will see throughout this book, many interesting and important codes will arise by modifying or combining existing codes. We will discuss five ways to do this.

# 1.5.1 Puncturing codes

Let C be an [n, k, d] code over Fq. We can puncture C by deleting the same coordinate i in each codeword. The resulting code is still linear, a fact that we leave as an exercise; its length is n - 1, and we often denote the punctured code by C*. If G is a generator matrix for C, then a generator matrix for C* is obtained from G by deleting column i (and omitting a zero or duplicate row that may occur). What are the dimension and minimum weight of C*? Because C contains q^k codewords, the only way that C* could contain fewer codewords is if two codewords of C agree in all coordinate i. In that case C has minimum distance d = 1 and a codeword of weight 1 whose nonzero entry is in coordinate i. The minimum distance decreases by 1 only if a minimum weight codeword of C has a nonzero i'th coordinate. Summarizing, we have the following theorem.

Theorem 1.5.1 Let C be an [n, k, d] code over Fq, and let C* be the code C punctured on the ith coordinate.