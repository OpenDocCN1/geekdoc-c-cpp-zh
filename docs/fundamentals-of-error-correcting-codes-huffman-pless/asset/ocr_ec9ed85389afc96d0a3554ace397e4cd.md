# 10.3.3 Decoding the Golay code with the hexacode

In Section 10.2, we presented a method to decode the [24, 12, 8] extended binary Golay code. To be used effectively, this decoding must be done by computer. Here we present another method for decoding, found in [268], which can certainly be programmed on a computer but can also be done by hand. We use a version of the [24, 12, 8] extended binary Golay code defined in terms of the hexacode.

We first establish some notation. Let \(\mathbf{v} = v_1 v_2 \cdots v_{24} \in \mathbb{F}_2^{24}\). We rearrange \(\mathbf{v}\) into a \(4 \times 6\) array

![](bbox=[0.15, 0.27, 0.35, 0.33])

which we denote by \([\mathbf{v}]\). The parity of a column of \([\mathbf{v}]\) is even or odd if the binary sum of the entries in that column is 0 or 1, respectively. There is an analogous definition for the parity of a row. The set of vectors written as \(4 \times 6\) matrices that satisfy two criteria will form the [24, 12, 8] extended binary Golay code. The second criterion involves the hexacode. The version of the hexacode \(\mathcal{G}_6\) used throughout the remainder of this section has generator matrix

![](bbox=[0.15, 0.44, 0.4, 0.5])

which is obtained from the generator matrix \([I_3 \ A]\), where \(A\) is given in (10.3), by interchanging the first and third columns of \([I_3 \ A]\). This form is used because it is easy to identify the 64 codewords in the hexacode. To use the hexacode we send an element of \(\mathbb{F}_4^{24}\) into an element of \(\mathbb{F}_4^6\) by defining the projection \(\text{Pr}(\mathbf{v})\) of \(\mathbf{v}\) into \(\mathbb{F}_4^6\) as the matrix product

```
\(\text{Pr}(\mathbf{v}) = [0 \ 1 \ \omega \ \bar{\omega}][\mathbf{v}]\)
```

Example 10.3.3 Suppose that \(\mathbf{v} = 111111000000001101010110\). The projection operation can be visualized by writing

![](bbox=[0.15, 0.66, 0.4, 0.78])

where the projection is accomplished by multiplying the first row of \([\mathbf{v}]\) by 0, multiplying the second row by 1, multiplying the third row by \(\omega\), multiplying the fourth row by \(\bar{\omega}\), and then adding.

Recall that the complement of a binary vector \(\mathbf{v}\) is the binary vector \(\mathbf{v} + \mathbf{1}\) obtained by replacing the 0s in \(\mathbf{v}\) by 1s and the 1s by 0s. We will repeatedly use the following lemma without reference; its proof is left as an exercise.