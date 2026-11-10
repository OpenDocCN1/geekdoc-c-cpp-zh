```
x^3 - 6*I*x^2 - 12*x + 8*I
```

Here, we can also write `p.map_coefficients(conjugate)`, since `conjugate(z)` has the same effect as `z.conjugate` for `z ∈ ℚ[i]`. Calling explicitly a method of the object `z` is more robust: the code then works for all objects having a `conjugate()` method, and only for those.

# Operations on polynomial rings

The parents of polynomial objects, i.e., the rings `A[x]`, are themselves first class Sage objects. Let us briefly see how to use them.

A first family of methods enables us to construct particular polynomials, to draw random ones, or to enumerate families, here those of degree exactly 2 over `𝔽₂`:

```
sage: list(GF(2)['x'].polynomials(of_degree=2))
[x^2, x^2 + 1, x^2 + x, x^2 + x + 1]
```

We will call some of these methods in the examples of the next sections, to build objects on which we will work. Chapter 15 explains more generally how to enumerate finite sets with Sage.

Secondly, the system “knows” some basic facts for each polynomial ring. We can check whether a given object is a ring, if it is noetherian:

```
sage: A = QQ['x']
sage: A.is_ring() and A.is_noetherian()
True
```

or if `ℤ` is a sub-ring of `ℚ[x]`, and for which values of `n` the ring `ℤ/nℤ` is integral:

```
sage: ZZ.is_subring(A)
True
sage: [n for n in range(20)
....:     if Integers(n)['x'].is_integral_domain()]
[0, 2, 3, 5, 7, 11, 13, 17, 19]
```

These capabilities largely rely on the Sage category system (see also §5.2.3). Polynomial rings belong to a number of “categories”, like the category of sets, that of Euclidean rings, and many more:

```
sage: R.categories()
[Category of euclidean domains,
 Category of principal ideal domains,
 ...
 Category of sets with partial maps, Category of objects]
```

This reflects that any polynomial ring is also a set, a Euclidean domain, and so on. The system can thus automatically transfer to polynomial rings the general properties of objects from these different categories.