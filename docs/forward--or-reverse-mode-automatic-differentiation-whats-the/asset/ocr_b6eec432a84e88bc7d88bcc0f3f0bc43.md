Using this in combination with the chain rule yields:

\frac{\partial (\mathbf{let}\ \mathbf{y} = \mathbf{e}_1\ \mathbf{in}\ \mathbf{e}_2)}{\partial x_i} = \frac{\partial f (\mathbf{e}_1, \dots, \mathbf{x}_n)}{\partial x_i}
= \left. \frac{\partial f (\mathbf{y}, \mathbf{x}_1, \dots, \mathbf{x}_n)}{\partial \mathbf{y}} \right|_{\mathbf{y}=\mathbf{e}_1, \mathbf{x}_1=\mathbf{x}_1, \dots, \mathbf{x}_n=\mathbf{x}_0} \times \frac{\partial \mathbf{e}_1}{\partial x_i}
+ \sum_{j=1}^{n} \left( \left. \frac{\partial f (\mathbf{y}, \mathbf{x}_1, \dots, \mathbf{x}_n)}{\partial \mathbf{x}_j} \right|_{\mathbf{y}=\mathbf{e}_1, \mathbf{x}_1=\mathbf{x}_1, \dots, \mathbf{x}_n=\mathbf{x}_0} \times \frac{\partial \mathbf{x}_j}{\partial x_i} \right)
= \frac{\partial \mathbf{e}_2}{\partial \mathbf{y}} \bigg|_{\mathbf{y}=\mathbf{e}_1} \times \frac{\partial \mathbf{e}_1}{\partial x_i} + \frac{\partial \mathbf{e}_2}{\partial \mathbf{x}_i} \bigg|_{\mathbf{y}=\mathbf{e}_1} \quad \square

# Appendix C. Haskell libraries and functionality

This section briefly introduces Haskell's type class feature and summarizes the key library functions that we use.

# C.1. Type classes

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