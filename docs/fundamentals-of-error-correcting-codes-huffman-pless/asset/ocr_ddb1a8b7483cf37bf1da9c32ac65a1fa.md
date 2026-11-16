that leads to an infinite weight codeword and the greatest common divisor \(1 + D\) of the minors.)...
Then there exist polynomials \(p(D)\) and \(q(D)\) together with nonnegative integers \(i\) and \(j\) such that \(a(D) = p(D)/D^i\) and \(b(D) = q(D)/D^j\). Then as \(G_1 K = I_1\), \((1 + D^2)a(D) + (1 + D + D^2 + D^3)b(D) = 1\), or

\(D'(1 + D^3)p(D) = D'(1 + D + D^2 + D^3)q(D) = D'^{1+j}\).

But the left-hand side is a polynomial divisible by \(1 + D\), while the right-hand side is not. Thus \(G'_1\) does not have a finite weight right inverse. In Example 14.5.1 we found a right inverse of \(G'_1\), but it was not of finite weight.

Turning to the encoder \(G_1\), we see that the two minors of \(G_1\) are \(1 + D + D^2\) and \(1 + D^2\), which have greatest common divisor 1. Thus \(G_1\) is noncatastrophic. Also \(G_1\) has the finite weight right inverse

\(K = \begin{bmatrix} D \\ 1+D \end{bmatrix}\).

also confirming that \(G_1\) is noncatastrophic.

**Example 14.5.5** In Example 14.1.1, we give three generator matrices for the (4, 2) convolutional code \(C_2\). All of these encoders are noncatastrophic. We leave the verification of this fact for \(G'_2\) and \(G''_2\) as an exercise. The minor obtained from the first and second columns of \(G_2\) is \(1 + D\), while the minor from the first and third columns of \(G_2\) is \(D\). Hence the greatest common divisor of all six minors of \(G_2\) must be 1.

**Exercise 835** Verify that the encoders \(G'_2\) and \(G''_2\) for the (4, 2) convolutional code \(C_2\) from Example 14.1.1 are noncatastrophic by showing that the greatest common divisor of the minors of each encoder is 1.

**Exercise 836** Find \(4 \times 2\) finite weight right inverses for each of the encoders \(G_2, G'_2,\) and \(G''_2\) of the (4, 2) convolutional code \(C_2\) from Example 14.1.1. Note: Many entries can be chosen to be 0.

**Exercise 837** Let \(G''_2\) be the generator matrix of the (4, 2) convolutional code \(C_2\) in Example 14.1.1. (a) Show that the greatest common divisor of the six minors of \(G''_2\) is \(1 + D + D^2\) and hence that \(G''_2\) is a catastrophic encoder. (b) Show that the input

\(\mathbf{x} = \begin{pmatrix} \frac{D^2}{1 + D + D^2} & \frac{1}{1 + D + D^2} \end{pmatrix}\)

to the encoder \(G''_2\) has infinite weight but that the encoded codeword \(\mathbf{c} = \mathbf{x}G''_2\) has finite weight. Also give \(\mathbf{c}\).

**Exercise 838** Let \(C_3\) be the (2, 1) convolutional code from Exercise 823 and Example 14.4.8 with generator matrices \(G_S = [1 \quad 1 + D]\) and \(G_S = [1 + D \quad 1 + D^2]\).