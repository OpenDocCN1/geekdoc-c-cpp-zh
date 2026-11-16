Exercise 857 Let C be the code in Example 15.5.1 with Tanner graph in Figure 15.8. Use the Message Passing Decoding Algorithm to decode the following received vectors; use the values of \(\mu(y, c)\) given in Example 15.2.1. (a) y = 0,1,0;1,0,0,1,0,1,13, (b) y = 1,0,0;0,1,0,0,4,12.

Exercise 858 Construct the Tanner graph for the [10, 6, 2] binary code with parity check matrix

H = [ 1 1 1 0 1 0 0 0 0 0 1 0 0 0 1 1 0 0 0 0 0 0 0 0 1 0 1 1 0 0 0 0 1 0 0 0 0 0 1 1 ]

Then use the Message Passing Decoding Algorithm to decode y = 1,0,2,15,0,1,11,2,15,14,0,13,1.

Use the values of \(\mu(y, c)\) given in Example 15.2.1.

# 15.6 Low density parity check codes

In the previous section we introduced our first example of iterative decoding through message passing. In the mid 1990s, iterative decoding became a significant technique for the decoding of turbo codes. Iterative decoding was introduced by Elias in 1954 [77]. Iterative decoding reappeared with the work of R. G. Gallager on low density parity check codes in 1963 but since then seems to have been largely neglected, with only a few exceptions, until researchers realized that the decoding of turbo codes was closely related to Gallager's techniques. In this section we will introduce low density parity check codes and examine Gallager's two versions of iterative decoding. Our presentation relies heavily on [94, 95, 211]. For the interested reader, the use of message passing in low density parity check code is described in [295].

In short, a binary low density parity check code is a code having a parity check matrix with relatively few 1s which are dispersed with a certain regularity in the matrix. An [n, k] binary linear code C is a low density parity check (LDPC) code provided it has an m x n parity check matrix H where every column has fixed weight c and every row of H has fixed weight r.? This type of code will be denoted an (n, c, r) LDPC code. Note that such a matrix may not have independent rows so is technically not a parity check matrix in the sense we have used in this text. However, H can be row reduced and the zero rows removed to form a parity check matrix for C with independent rows. Thus the dimension of C is at least n - m. Counting the number of 1s in H by both rows and columns gives the relationship nc = mr among the parameters. Generally, we want r and c to be relatively small compared to n and thus the density of 1s in H is low.

7 A natural generalization for LDPC codes is to allow the row weights and column weights of H to vary, in some controlled manner. The resulting codes are sometimes termed 'irregular' LDPC codes.