
```
derive_pwd ∀ var x y = e tan^n (tan^n (abstractD gen e) x) y
where gen z = N (var z) (delta z)
```

We start the derivation from a point-free formulation of derive_pwd :

```
λ y x → eval var ∘ (Sx) ∘ tan^n ∘ forwardAD_Dense Var
∘ (Sy) ∘ tan^n ∘ forwardAD_Dense Var
= { naturality of function application - }
λ y x → (Sx) ∘ fmap (eval var) ∘ tan^n ∘ forwardAD_Dense Var
∘ (Sy) ∘ tan^n ∘ forwardAD_Dense Var
= { - β - reduction - }
λ y → fmap (eval var) ∘ tan^n ∘ forwardAD_Dense Var
∘ (Sy) ∘ tan^n ∘ forwardAD_Dense Var
= { - naturality of function application - }
λ y → (Sy) ∘ fmap (fmap (eval var) ∘ tan^n ∘ forwardAD_Dense Var)
∘ tan^n ∘ forwardAD_Dense Var
= { - β - reduction - }
fmap (fmap (eval var) ∘ tan^n ∘ forwardAD_Dense Var)
∘ tan^n ∘ forwardAD_Dense Var
= { - naturality of tan^n, see equation (A.1) below - }
fmap (tan^n ∘ bimap (eval var) (fmap (eval var))) ∘ forwardAD_Dense Var
∘ tan^n ∘ forwardAD_Dense Var
= { - eval fusion - }
fmap (tan^n ∘ eval gen' ∘ tan^n ∘ forwardAD_Dense Var)
where gen' z = N (var z) (delta z)
= { - fmap fusion + naturality of tan^n - }
fmap (tan^n ∘ tan^n ∘ bimap (eval gen') (fmap (eval gen')) ∘ forwardAD_Dense Var)
where gen' z = N (var z) (delta z)
= { - eval fusion - }
fmap (tan^n ∘ tan^n ∘ eval gen'')
where gen'' z = N (N (var z) (delta z)) (delta z)
= { - abstractD definition - }
fmap tan^n ∘ abstractD
where gen z = N (var z) (delta z)
```

The steps involving the naturality of tan^n do not concern the Functor instance of Natagata numbers, but their Bifunctor instance, which allows to vary both components.

```
instance Bifunctor (<:>) where
bimap f g (N d e) = N (f d) (g e)
```

The general naturality property of tan^n : ∀ v d e. e -> e for this Bifunctor instance is:

```
g ∘ tan^n = tan^n ∘ bimap f g
```

However, for the specialized type tan^n : ∀ v d. (Dense v d) → Dense v d where the two components are not independent, we also have this specialized naturality property:

```
fmap f ∘ tan^n = tan^n ∘ bimap f (fmap f) (A.1)
```

## Appendix B. Proof of Lemma 1

Proof. We prove this rule by means of the chain rule for multi-variate functions:

```
\frac{\partial f(e_1, ..., e_n)}{\partial x} = \sum_{i=1}^n \left( \frac{\partial f(x_1, ..., x_n)}{\partial x_i} \right|_{x_1=e_1, ..., x_n=e_n} \times \frac{\partial e_i}{\partial x} \right)
```

Define f as f (y, x1, ..., xn) = e2 where x1, ..., xn comprise all the free variables of e1 and e2. Then we have that f (e1, x1, ..., xn) = let y = e1 in e2.

Using this in combination with the chain rule yields:

```
\frac{\partial (\mathbf{let}\ \mathbf{y} = \mathbf{e}_1\ \mathbf{in}\ \mathbf{e}_2)}{\partial x_i} = \frac{\partial f (\mathbf{e}_1, \dots, \mathbf{x}_n)}{\partial x_i}
= \left. \frac{\partial f (\mathbf{y}, \mathbf{x}_1, \dots, \mathbf{x}_n)}{\partial \mathbf{y}} \right|_{\mathbf{y}=\mathbf{e}_1, \mathbf{x}_1=\mathbf{x}_1, \dots, \mathbf{x}_n=\mathbf{x}_n} \times \frac{\partial \mathbf{e}_1}{\partial x_i}
+ \sum_{j=1}^{n} \left( \left. \frac{\partial f (\mathbf{y}, \mathbf{x}_1, \dots, \mathbf{x}_n)}{\partial \mathbf{x}_j} \right|_{\mathbf{y}=\mathbf{e}_1, \mathbf{x}_1=\mathbf{x}_1, \dots, \mathbf{x}_n=\mathbf{x}_n} \times \frac{\partial \mathbf{x}_j}{\partial x_i} \right)
= \frac{\partial \mathbf{e}_2}{\partial \mathbf{y}} \bigg|_{\mathbf{y}=\mathbf{e}_1} \times \frac{\partial \mathbf{e}_1}{\partial x_i} + \frac{\partial \mathbf{e}_2}{\partial \mathbf{x}_i} \bigg|_{\mathbf{y}=\mathbf{e}_1} \quad \square
```

## Appendix C. Haskell libraries and functionality

This section briefly introduces Haskell's type class feature and summarizes the key library functions that we use.

### C.1. Type classes

We use Haskell's type classes [45] to model the interface of algebraic structures, such as the semirings:

```
class Semiring d where
  zero :: d
  one :: d
  (⊕) :: d -> d -> d
  (⊗) :: d -> d -> d
```

Under the hood, the Haskell compiler creates a datatype, called a dictionary type, that contains all the methods of the type class.

```
data SemiringDict d = SD (zero :: d
                      , one :: d
                      , (⊕) :: d -> d -> d
                      , (⊗) :: d -> d -> d)
```

A type class instance provides the implementation of the interface for a specific type. For example,

```
instance Semiring (Expr v) where
  zero = Zero
  one = One
  (⊕) = Plus
  (⊗) = Times
```

Under the hood, an instance gives rise to a dictionary value that contains these implementations.

```
semiringExprDict :: SemiringDict (Expr v)
semiringExprDict = SD (zero = Zero
                   , one = One
                   , (⊕) = Plus
                   , (⊗) = Times)
```

We can use the type class methods at a specific type for which there is an instance. E.g.,

```
expr :: Expr v
expr = one ⊕ one
```

The compiler turns this into code that explicitly extracts the implementations from the appropriate dictionary:

```
expr :: Expr v
expr = d.(⊕) d.one d.one where d = semiringExprDict
```

The selection of the appropriate dictionary is known as type class resolution and directed by the type at which the methods are used. Because every type can have at most one instance of a type class, there is always at most one appropriate dictionary.

We can also abstract over the particular type used with a type variable d. Then the type variable is subject to the type class constraint Semiring d. This means that d can be freely chosen as long as it has a Semiring instance. This is known as constrained polymorphism.

```
expr :: Semiring d => d = one ⊕ one
```

Under the hood, the type class constraint is transformed into an explicit dictionary parameter.

```
expr :: SemiringDict d -> d = d ⊕ (d).one d.one
```

When using such a constraint polymorphic definition at a specific type, the Haskell compiler implicitly provides the appropriate dictionary parameter. For example, it turns expr :: Expr v into expr semiringExprDict :: Expr v.

In multi-parameter type classes, i.e., type classes with multiple parameters in their signature (e.g., Module d e), we can declare functional dependencies between parameters to aid type class resolution. A functional dependency indicates that one type parameter is uniquely determined by the other(s). For example, our Module class uses such a functional dependency:

```
class (Semiring d, Monoid e) => Module d e | e -> d where ...
```

Here the semiring type d can be determined from type e.

For a more thorough introduction to type classes and Haskell in general, we refer to Bird [46] and Hutton [47].

### C.2. Maps

The functions below are from Haskell's Data.Map library,14 copied with their type signature and explanation.

- (!) :: Ord k => Map k a -> k -> a O(log n). Find the value at a key. Calls error when the element can not be found.
- findWithDefault :: Ord k => a -> k -> Map k a -> a O(log n). The expression findWithDefault def k map returns the value at key or returns default value def when the key is not in the map.
- fromList :: Ord k => [(k, a)] -> Map k a O(n * log n). Build a map from a list of key/value pairs. If the list contains more than one value for the same key, the last value for the key is retained.
- unionWith :: Ord k => (a -> a -> a) -> Map k a -> Map k a -> Map k a O(n + m). Union with a combining function. The implementation uses the efficient hedge-union algorithm.
- insertWith :: Ord k => (a -> a -> a) -> k -> a -> Map k a -> Map k a O(log n). Insert with a function, combining new value and old value. insertWith f key value mp will insert the pair (key, value) into mp if key does not exist in the map. If the key does exist, the function will insert the pair (key, f new_value old_value).

### C.3. Arrays

The functions below are from Haskell's Data.Array.MArray library,15 copied with their type signature and explanation.

- newArray :: Ix i => (i, i) -> e -> m (a i e) Builds a new array, with every element initialised to the supplied value.
- readArray :: (MArray a e m, Ix i) => a i e -> i -> m e Read an element from a mutable array
- writeArray :: (MArray a e m, Ix i) => a i e -> i -> e -> m () Write an element in a mutable array
- getElems :: (MArray a e m, Ix i) => a i e -> m [i, e] Return a list of all the associations of a mutable array, in index order.
