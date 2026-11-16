```
instance (Ord v, Semiring d) => Monoid (Sparse v d) where
zero = empty
(⊕) = unionWith (⊕)
```

Scalar multiplication is also key-wise. As d ⊗ zero = zero (Fig. 1), we can effortlessly preserve the implicit zero entries.

```
instance (Ord v, Semiring d) => Module d (Sparse v d) where
d • m = fmap (d⊗) m
```

The only non-zero entry for delta x is that for x.

```
instance (Ord v, Semiring d) => Kronecker v d (Sparse v d) where
delta x = singleton x one
```

Moreover, and crucially in what follows, we observe the following relationship between this Kronecker structure and its Module and Monoid instances:

```
d • delta v = singleton v d (1)
e ⊕ (d • delta v) = insertWith (⊕) v d e (2)
```

Lastly, the CorrectAD instance is straightforward.

```
instance (Ord v, Bounded v, Enum v, Semiring d, Eq d) => CorrectAD d v d (Sparse v d) where
rep = rep_-
abs = abs_-
```

In summary, all that the sparse gradient computation requires, in comparison to the dense computation, is the switch from d × (Dense v d) to d × (Sparse v d).

```
forwardADSparse : : (Ord v, Semiring d) => (v -> d) -> Exp v -> d × Sparse v d
forwardADsparse = abstractD
```

Theorem 2 now holds by construction. We can verify this correspondence by revisiting example2 at the point (5, 3).

```
> let {var X = 5; var Y = 3} in tan^y (forwardADsparse var example2)
[X -> 4; Y -> 5]
```

# 5. Reverse-mode automatic differentiation

We now develop the appropriate d-module structure that exhibits reverse-mode AD as an instance of abstractD by refining the above sparse representation. Motivated by the quest for improved efficiency, we optimize the time complexity of the essential functions for abstract differentiation with the underlying Nagata numbers semiring: scalar multiplication (⊙), addition (⊕) and Kronecker's delta.

# 5.1. Accumulating multiplications

We start with another function-based representation. Instead of the d-module e, we consider the space of d-module homomorphisms from d to e. It is a standard result in commutative algebra [22, p. 18] that these two structures are isomorphic, considered as d-modules. In terms of the underlying Haskell types, this amounts to taking the plain function space.

```
type d -> e = d -> e
```

7 For the case of commutative rings and their modules; the argument for semirings and modules is identical, but simpler, because there are fewer equations to check.