where \( g_1(x) = x - 1, g_2(x) = x^4 + x^3 + x^2 + x + 1, g_3(x) = x^2 + x + 1, \text{and } g_4(x) = x^4 + 2x^2 + 3x + 1 \). Let \( \mathcal{C} = (f(x)g(x)) \oplus (2f(x)h(x)) \) be a self-dual cyclic code of length 15. By Theorem 12.5.10, \( f^*(x) = h(x) \) and \( g^*(x) = g(x) \). This implies that if \( g(x) \) contains a given factor, it must also contain the reciprocal polynomial of that factor. Also if an irreducible factor of \( x^{15} - 1 \) is its own reciprocal polynomial, it must be a factor of \( g(x) \). Thus there are only the following possibilities: (a) \( f(x) = g_4(x), g(x) = g_1(x)g_2(x)g_3(x) \), and \( h(x) = g_1^2(x) \), (b) \( f(x) = g_4^2(x), g(x) = g_1(x)g_2(x)g_3(x) \), and \( h(x) = g_4(x) \), and (c) \( f(x) = 1, g(x) = x^{15} - 1 \), and \( h(x) = 1 \). The codes in (a) and (b) are of type \( 4^2 2^7 \), they are equivalent under the multiplier \( \mu_{-1} \). The code in (c) is the trivial self-dual code with generator matrix \( 2I_{15} \).

Exercise 744 Consider the cyclic code \( \mathcal{C} \) of length 15 with generator polynomials given by (a) in Example 12.5.11.

+   (a) Write down a \( 4 \times 15 \) generator matrix for \( \text{Res}(\mathcal{C}) \). Note that \( \text{Res}(\mathcal{C}) \) is a cyclic code with generator polynomial \( \mu(f(x)g(x)) \).

+   (b) The generator matrix from part (a) is the parity check matrix for \( \text{Tor}(\mathcal{C}) \) by Theorem 12.5.4. What well-known code is \( \text{Tor}(\mathcal{C}) \)? What well-known code is \( \text{Res}(\mathcal{C}) \)?

Exercise 745 The factorization of \( x^{21} - 1 \) over \( \mathbb{Z}_4 \) is given by

\( x^{21} - 1 = g_1(x)g_2(x)g_3(x)g_5^2(x)g_4(x)g_6^4(x) \),

where \( g_1(x) = x - 1, g_2(x) = x^2 + x + 1, g_3(x) = x^6 + 2x^5 + 3x^4 + 3x^2 + x + 1, \text{and } g_4(x) = x^3 + 2x^2 + x + 3 \).

+   (a) As in Example 12.5.11, list all possible triples \( (f(x), g(x), h(x)) \) that lead to self-dual cyclic codes of length 21 over \( \mathbb{Z}_4 \). Note: There are nine such codes including the trivial self-dual code with generator matrix \( 2I_{21} \).

+   (b) Give the types of each code found in (a).

# 12.5.3 Lattices from self-dual codes over \( \mathbb{Z}_4 \)

In Section 10.6 we introduced the concept of a lattice and described how to construct lattices from codes, particularly self-dual binary codes. One method to construct lattices from binary codes described in that section is called Construction A. There is a \( \mathbb{Z}_4 \)-analogue called \( Construction A_4 \), beginning with a \( \mathbb{Z}_4 \)-linear code \( \mathcal{C} \) of length \( n \). Construction \( A_4 \) produces a lattice \( \Lambda_4(\mathcal{C}) \), which is the set of all \( \mathbf{x} \) in \( \mathbb{R}^n \) obtained from a codeword in \( \mathcal{C} \) by viewing the codeword as an integer vector with 0s, 1s, 2s, and 3s, adding integer multiples of 4 to any components, and dividing the resulting vector by 2. In particular,

\( \Lambda_4(\mathcal{C}) = \{ \mathbf{x} \in \mathbb{R}^n \mid 2\mathbf{x} (\text{mod } 4) \in \mathcal{C} \} \).