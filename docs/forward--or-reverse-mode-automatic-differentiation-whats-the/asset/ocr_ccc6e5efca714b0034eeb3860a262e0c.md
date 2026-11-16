But we intend this type d -> e to represent only the d-module homomorphisms. This is the case for linear functions from d to e. A function f : d -> e is linear^3 iff it has the multiplicative homogeneity property:

f (\x) y = x • f y

As the Haskell type d -> e also includes non-linear functions, we have to make disciplined use of d -> e, being careful to avoid the non-linear ones. Intuitively, we can think of d -> e as augmenting e with an accumulator for a scalar multiplier of type d. By supplying the scalar one, we recover the original module.

```
```haskell
rep_- :: Module d e => d -> e -> (d -> e)
rep_e e = \x d -> d • e
abs_- :: Module d e => (d -> e) -> e
abs_- f = f one
```
```

In particular, as one e • e = e (Fig. 3), we have that abs_- o rep_- = id. Moreover, for linear functions also rep_- o abs_- = id. Now we derive Monoid, Module and Kronecker instances that make rep_- a homomorphism by construction. It follows that d -> e inherits its monoid structure in a pointwise fashion from e. For e = Dense v d, the time complexity for additive operations remains linear in the number of variables.

```
```haskell
instance Monoid e => Monoid (d -> e) where
  zero = \x d -> zero
  f ⊕ g = \x d -> f x d ⊕ g x d
```
```

Furthermore, its d-module structure uses the function parameter as an accumulator for the scalar multiplier. This affords a "strength reduction": the expensive scalar multiplication (•) is replaced by the cheaper semiring multiplication (⊕).

```
```haskell
instance Module d e => Module d (d -> e) where
  d' • f = \x d -> f (x ⊕ d d)
```
```

This reduces the time complexity of scalar multiplication from O(|V|) (where V denotes the number of variables with non-zero values in the given sparse map) for the Sparse v d representation to O(1) for that of d -> Sparse v d. However, the general Kronecker instance of d -> e still contains the expensive (•) operator.

```
```haskell
instance Kronecker v d e => Kronecker v d (d -> e) where
  delta v = \x d -> d • delta v
```
```

Fortunately, we only require a specialized instance for sparse maps, which operates in constant time, as a consequence of equation (1) for d -> delta v.

```
```haskell
instance (Ord v, Semiring d) => Kronecker v d (d -> Sparse v d) where
  delta = singleton
```
```

Finally, the CorrectAD instance for d -> e is defined as the composition of rep_-/abs_- with rep/abs of e.

```
```haskell
instance CorrectAD v d e => CorrectAD v d (d -> e) where
  rep = rep_- . o rep
  abs = abs_- o abs_-
```
```

In summary, by using d < (d -> Sparse v d) we obtain reverse-mode AD.

```
```haskell
reverseAD :: (Ord v, Semiring d) => (v -> d) -> Exp v -> d < (d -> Sparse v d)
reverseAD = abstractD
```
```

For instance, consider the more extensive example expression x x × (x + 1) × (x + x), encoded in Haskell as example_3.

```
```haskell
example_3 :: Exp X
example_3 = Times (Var X) (Times (Plus (Var X) One) (Plus (Var X) (Var X)))
```
```

Running reverse-mode AD on this expression, the derivative at X = 5 is 170.

```
```
> (abs_- . tanh^n) (reverseAD (\x -> 5) example_3)
{X -> 170}
```
```