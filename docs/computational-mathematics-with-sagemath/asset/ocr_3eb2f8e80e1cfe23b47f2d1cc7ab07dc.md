| Domain | Sage representation |
|---|---|
| **Some basic Python types** | |
| Python integers | `int` |
| Python floating-point numbers | `float` |
| Booleans (`true`, `false`) | `bool` |
| Character strings | `str` |
| **Basic numerical domains** | |
| Integers ℤ | `ZZ` or `IntegerRing()` |
| Rational numbers ℚ | `QQ` or `RationalField()` |
| Floating-point numbers with *p* bits | `Reals(p)` or `RealField(p)` |
| Complex floating-point numbers with *p* bits | `Complexes(p)` or `ComplexField(p)` |
| **Rings and finite fields** | |
| Integers modulo *n*, ℤ/*n*ℤ | `Integers(n)` or `IntegerModRing(n)` |
| Finite field 𝔽<sub>q</sub> | `GF(q)` or `FiniteField(q)` |
| **Algebraic numbers** | |
| Algebraic numbers ℚ̄ | `QQbar` or `AlgebraicField()` |
| Real algebraic numbers | `AA` or `AlgebraicRealField()` |
| Number fields ℚ[*x*]/(*p*) | `NumberField(p)` |
| **Symbolic computation** | |
| Matrices *m* × *n* with coefficients in *A* | `MatrixSpace(A, m, n)` |
| Polynomials *A*[*x*,*y*] | `A[x,y]` or `PolynomialRing(A, 'x,y')` |
| Series *A*[[*x*]] | `A[['x']]` or `PowerSeriesRing(A, 'x')` |
| Symbolic expressions | `SR` |

Table 5.1 – Main domains and parents.

# 5.3.1 Elementary Domains

We call *elementary computational domains* (or simply elementary domains) the classical sets of constants, with no variable: integers, rational numbers, floating-point numbers, booleans, integers modulo *n*...

**Integers.** The integers are represented in radix two internally, and printed by default in radix ten. As seen above, the Sage integers are objects of the class `Integer`. Their parent is the ring ℤ:

```
sage: 5.parent()
Integer Ring
```

The integers are always in normal form; their equality is thus easy to check. As a consequence, to be able to represent integers in factorised form, the `factor` command needs a specific class:

```
sage: type(factor(4))
<class 'sage.structure.factorization_integer.IntegerFactorization'>
```