and the vector space of functions, which will actually be a vector space of equivalence classes of rational functions related to the function defining the curve.

We first concentrate on this latter vector space of functions. Let \( p(x, y, z) \) be a homogeneous polynomial of positive degree that defines a projective curve \( \mathcal{X} \) over a field \( \mathbb{F} \).

Define the field of rational functions on \( \mathcal{X} \) over \( \mathbb{F} \) by
\[\mathbb{F}(\mathcal{X}) = \left\{ \left. \begin{matrix} g \\ h \end{matrix} \right| g, h \in \mathbb{F}[x, y, z] \text{ homogeneous } \cup \{0\} \right\} / \approx_{\mathcal{X}} .\]

This notation means that \( \mathbb{F}(\mathcal{X}) \) is actually a collection of equivalence classes of rational functions where the numerator and denominator are homogeneous of equal degree. By requiring that the denominator not be a multiple of \( p(x, y, z) \), at least one of the points on \( \mathcal{X} \) is not a zero of the denominator. To define the equivalence we say that \( g/h \approx g'/h' \) if and only if \( gh' - g'h \) is a polynomial multiple of \( p(x, y, z) \). Furthermore, we say \( h/g \approx h \) precisely when \( g(x, y, z) \) is a polynomial multiple of \( p(x, y, z) \). By Exercise 785, \( \mathbb{F}(\mathcal{X}) \) is actually a field containing \( \mathbb{F} \) as a subfield.

**Exercise 785** Verify that \( \mathbb{F}(\mathcal{X}) \) is a field containing \( \mathbb{F} \) as a subfield (where \( \mathbb{F} \) is identified with the constant polynomials). \(\blacklozenge\)

Let \( f = g/h \in \mathbb{F}(\mathcal{X}) \) with \( f \neq_{\mathcal{X}} 0 \). Then the *divisor of f* is
\(\text{div}(f) = (\mathcal{X} \cap \mathcal{X}_g) - (\mathcal{X} \cap \mathcal{X}_h). \quad (13.10)\)

that is, the difference in the intersection divisors \( \mathcal{X} \cap \mathcal{X}_g \) and \( \mathcal{X} \cap \mathcal{X}_h \). Essentially, div(f) is a mechanism to keep track easily of the zeros and poles of f that are on \( \mathcal{X} \) together with their multiplicities and orders, respectively; in effect, div(f) is the "zeros of f on \( \mathcal{X} \)" minus the "poles of f on \( \mathcal{X} \)". There will be cancellation in (13.10) whenever a point on \( \mathcal{X} \) is both a zero and a pole; ultimately, if \( P \) appears with positive coefficient in div(f), it is a zero of f and a pole if it appears with a negative coefficient. If g and h have degrees \( d_g \) and \( d_h \), respectively, then by Bézout's Theorem, deg(div(f)) = \( d d_g - d d_h = 0 \) as \( d_g = d_h \). Since f is only a representative of an equivalence class, we need to know that div(f) is independent of the representative chosen and therefore is well-defined. This is indeed true; we do not prove it but illustrate it in Exercise 786.

**Exercise 786** Let \( \mathcal{X} \) be the elliptic curve defined by \( x^3 + xz^2 + z^3 + y^2z + yz^2 = 0 \) over a field of characteristic 2. Let \( f = g/h \) and \( f' = g'/h' \), where \( g(x, y, z) = x^2 + z^2 \), \( h(x, y, z) = z^2 \), \( g'(x, y, z) = z^2 + y^2 + yz \), and \( h'(x, y, z) = xz \). As in Example 13.3.3, let \( P_\infty = (0 : 1 : 0) \) and \( P_2 = ((1 : \omega : 1), (1 : \overline{\omega} : 1)) \). Example 13.3.7 and Exercise 783 will help with parts (b) and (c).
(a) Show that \( f \approx f' \).
(b) Show that div(f) = \( 2P_2 - 4P_\infty \) using (13.10).
(c) Show that div(f') = \( 2P_2 - 4P_\infty \) using (13.10) with f', g', and h' in place of f, g, and h. \(\blacklozenge\)

There is a partial ordering of divisors on a curve given by \( D = \sum n_P P \ge D' = \sum n'_P P \) provided \( n_P \ge n'_P \) for all P. Thus D is effective if \( D \ge 0 \). We now define the space of