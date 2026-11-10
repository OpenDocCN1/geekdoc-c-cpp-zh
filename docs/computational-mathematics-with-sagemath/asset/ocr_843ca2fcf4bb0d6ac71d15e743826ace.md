This works for a large number of domains, with more or less efficiency.

In particular, selecting for D the field of algebraic numbers QQbar or that of real algebraic numbers AA enables us to compute exactly the complex or real roots of a polynomial with rational coefficients:

```
sage: roots = p.roots(AA); roots
[(-1.626576561697786?, 1), (0.50000000000000000?, 2),
(1.626576561697786?, 1), (2.0000000000000000?, 2)]
```

Sage plays transparently for the user with different representations of algebraic numbers. One encodes each α ∈ Q by its minimal polynomial together with a sufficiently accurate interval to distinguish α from the other roots. Therefore, despite their output, the returned roots are not just approximate values. They can be reused in exact computations:

```
sage: a = roots[0][0]^4; a.simplify(); a
7
```

Here, we have raised the first root found to the fourth power, then forced Sage to simplify the result to make it clear it equals the integer 7.

A variant of the exact resolution is to simply *isolate* the roots, i.e., determine intervals containing exactly one root each, by giving as domain D that of the real intervals RIF or complex intervals CIF. Among the other useful domains in the case of a polynomial with rational coefficients, let us mention RR, CC, RDF, CDF, which all correspond to approximate numerical roots, and the number fields QQ[alpha]. The specific methods `real_roots`, `complex_roots` (and for some base rings) `real_root_intervals` offer additional options or give slightly different results from the `roots` method. The numerical approximation and isolation of roots is discussed in more detail in §12.2.

# 7.3.3 Resultant

In a unique factorisation domain, the existence of a common non-constant factor between two polynomials is characterised by the nullity of their resultant Res(p,q), which is a polynomial in their coefficients. A major advantage of the resultant compared to the gcd is that it *specialises* well under ring morphisms. For example, the polynomials x − 12 and x − 20 are coprime in Z[x], but the nullity of their resultant

```
sage: x = polygen(ZZ); (x-12).resultant(x-20)
-8
```

modulo n shows that they have a common factor in Z/nZ if and only if n divides 8.
Let p = ∑_{i=0}^m p_i x^i and q = ∑_{i=0}^n q_i x^i be two non constant polynomials in