the examples will have coefficients in a field. In the whole chapter, the letters A and K respectively correspond to a commutative ring and to a field.

The first step to perform a computation in an algebraic structure R is often to build R itself. We build ℚ[x] with

```
```sage
sage: R = PolynomialRing(QQ, 'x')
sage: x = R.gen()
```
```

The 'x' on the first line is a character string, which is the name of the indeterminate, or generator of the ring. The x on the second line is a Python variable in which one stores the generator; using the same name makes the code easier to read. The object stored in the variable x represents the polynomial x ∈ ℚ[x]. Its parent (the parent of a Sage object is the algebraic structure “from which it comes”, see §5.1) is the ring QQ['x']:

```
```sage
sage: x.parent()
Univariate Polynomial Ring in x over Rational Field
```
```

The polynomial x ∈ ℚ[x] is considered different from x ∈ A[x] for a base ring A ≠ ℚ, and also different from those, like t ∈ ℚ[t], whose indeterminate has a different name.

The expression PolynomialRing(QQ, 't') might also be written QQ['t']. We often combine this abbreviation with the construction S.<g> = ..., which simultaneously assigns a structure to the variable S and its generator to the variable g. The construction of the ring ℚ[x] and of its indeterminate then reduces to R.<x> = QQ[]. The form x = polygen(QQ, 'x') seen above is equivalent to

```
```sage
sage: x = PolynomialRing(QQ, 'x').gen()
```
```

Let us mention that we can choose between several memory representations when we construct a polynomial ring. The differences between representations are discussed in §7.6.

# Exercise 24 (Variables and indeterminates).

+   1. How would you define x and y to obtain the following results?

```
```sage
sage: x^2 + 1
y^2 + 1
sage: (y^2 + 1).parent()
Univariate Polynomial Ring in x over Rational Field
```
```

+   2. After the instructions

```
```sage
sage: Q.<x> = QQ[]; p = x + 1; x = 2; p = p * x
```
```

what is the value of p?