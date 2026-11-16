![](bbox=[0.12, 0.08, 0.78, 0.33])

Figure 15.10 Parity check matrix for a (16, 3, 4) LDPC code.

Figure 15.10 gives the parity check matrix of a (16, 3, 4) code, which is a [16, 6, 6] binary code.

Exercise 859 Show that the binary code C with parity check matrix given in Figure 15.10 has dimension 6 and minimum weight 6. Hint: Row reduce H to obtain the dimension. For the minimum weight, show that C is even and that every codeword has an even number of 1s in each of the four blocks of four coordinates, as presented in the figure. Then use Corollary 1.4.14 to show that C has no weight 4 codewords.

Gallager developed two iterative decoding algorithms designed to decode LDPC codes of long length, several thousand bits for example. The first iterative decoding algorithm is a simple hard decision algorithm. Assume that the codeword c is transmitted using an (n, c, r) binary LDPC code C, and the vector y is received. In the computation of the syndrome Hy^T, each received bit y_i affects at most c components of that syndrome, as the ith bit is in c parity checks. If among all the bits S involved in these c parity checks only the ith bit is in error, then these c components of Hy^T will equal 1 indicating the parity check equations are not satisfied. Even if there are some other errors among these bits S, one expects that several of the c components of Hy^T will equal 1. This is the basis of the Gallager Hard Decision Decoding Algorithm.

+   Decision Decoding Algorithm.
+   I. Compute Hy^T and determine the unsatisfied parity checks, that is, the parity checks where the components of Hy^T equal 1.
+   II. For each of the n bits, compute the number of unsatisfied parity checks involving that bit.
+   III. Change the bits of y that are involved in the largest number of unsatisfied parity checks; call the resulting vector y again.
+   IV. Iteratively repeat I, II, and III until either Hy^T = 0, in which case the received vector is decoded as this latest y, or until a certain number of iterations is reached, in which case the received vector is not decoded.