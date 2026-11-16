For \( B \in \mathcal{B} \), as the only entries in \( \mathbf{c}_B \) and \( \mathbf{c}_{B'} \) are 0s and 1s, \( \mathbf{c}_B \cdot \mathbf{c}_{B'} \) is actually in \( \mathbb{F}_p \subseteq \mathbb{F}_q \) and clearly equals \( |B \cap B'| \) modulo \( p \). If \( B \neq B' \), \( |B \cap B'| = \lambda \) by Lemma 8.5.1; if \( B = B' \), \( |B \cap B'| = k \). As \( p \mid (k - \lambda) \), \( k \equiv \lambda \pmod p) \). Thus \( |B \cap B'| \equiv k \pmod p) \) for all \( B \in \mathcal{B} \) and the right-hand side of (8.8) becomes

```
\(\sum_{B \in \mathcal{B}} a_B \mathbf{c}_B \cdot \mathbf{c}_B = \sum_{B \in \mathcal{B}} k a_B,\)
```

implying

```
\(\mathbf{c}_S \cdot \mathbf{c}_{B'} = \sum_{B \in \mathcal{B}} k a_B, \quad (8.9)\)
```

The codeword \( \mathbf{c}_S \) is obtained by multiplying each row of \( A \) corresponding to \( B \) by \( a_B \) thus creating a matrix \( A' \) and adding the rows of \( A' \) in \( \mathbb{F}_q \). The sum of all the entries in \( A' \) is \( \sum_{B \in \mathcal{B}} k a_B \) as the row corresponding to \( B \) is the sum of \( a_g \) taken \( k \) times. This must be the sum of the entries in \( \mathbf{c}_S \) in \( \mathbb{F}_p \). But the sum of the entries in \( \mathbf{c}_S \) is the sum of \( k \) 1s in \( \mathbb{F}_q \). As above, \( \mathbf{c}_S \cdot \mathbf{c}_{B'} \) is again in \( \mathbb{F}_p \subseteq \mathbb{F}_q \) and equals \( |S \cap B'| \) modulo \( p \). Hence (8.9) becomes

```
\(|S \cap B'| \equiv k \equiv \lambda \pmod p).\)
```

As \( p > \lambda \), we must have \( |S \cap B'| \ge \lambda \) for all \( B' \in \mathcal{B} \). The result follows from Lemma 8.5.4.

This theorem shows that if \( p > \lambda \), the codewords in \( \mathcal{C}_q(A) \) of weight \( k \) that are multiples of binary vectors must have supports that are blocks. There are examples of designs showing that you cannot drop either the condition \( p > \lambda \) or the condition that the codeword of weight \( k \) must be constant on its support.

# **Example 8.5.6** There are three inequivalent symmetric 2-(16, 6, 2) designs. If \( A \) is the incidence matrix one of these designs, then \( \mathcal{C}_2(A) \) has dimension 6, 7, or 8. If we let \( A_i \) be the incidence matrix where \( \mathcal{C}_i = \mathcal{C}_2(A_i) \) has dimension \( i \), the weight enumerators are given in [302]:

```
\(W_{C_1}(x, y) = y^{16} + 16x^6y^{10} + 30x^8y^8 + 16x^{10}y^6 + x^{16},\)
\(W_{C_2}(x, y) = y^{16} + 4x^4y^{12} + 32x^6y^{10} + 54x^8y^8 + 32x^{10}y^6 + 4x^{12}y^4 + x^{16},\)
\(W_{C_3}(x, y) = y^{16} + 12x^4y^{12} + 64x^6y^{10} + 102x^8y^8 + 64x^{10}y^6 + 12x^{12}y^4 + x^{16}.\)
```

Notice that the 16 blocks are precisely the supports of the weight 6 codewords only in the first code. In the other cases there are codewords of weight 6 whose supports are not blocks. Thus the condition \( p > \lambda \) in Theorem 8.5.5 is necessary. Notice that in the last two cases the minimum weight is less than the block size.

# **Example 8.5.7** In Exercise 471, you are asked to construct an \( (11, 5, 2) \) cyclic difference set that will yield a symmetric 2-(11, 5, 2) design \( \mathcal{D} \). Let \( A \) be its incidence matrix. By Theorem 8.5.3(ii), \( \mathcal{C}_3(A) \) is an \( [11, 6] \) code. It turns out that the code has minimum weight 5 and that there are codewords of weight 5 whose supports are not blocks of the original design; these are codewords with nonzero components a mixture of both 1 and 2. Thus the condition that the codeword of weight \( k \) must be constant on its support is also necessary in Theorem 8.5.5.