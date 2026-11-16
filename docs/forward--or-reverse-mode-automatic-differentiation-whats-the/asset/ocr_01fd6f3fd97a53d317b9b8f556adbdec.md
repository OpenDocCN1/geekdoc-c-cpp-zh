```
xcs ⊗ yys = (x ⊗ y) : λv → ((xs ⊗ yys) ⊕ (xss ⊗ ys v))
where xss = (x :< xs)
yys = (y :< ys)
```

The `Module` and `Kronecker` instances follow naturally from this definition. They allow us to automatically differentiate a symbolic expression and obtain its stream (of series of derivatives).

```
forwardADAll :: (Eq v, Semiring d) => (v -> d) -> Expr v -> Stream d
forwardADAll var = eval gen where gen y = var y :< delta y
> forwardADAll (λX -> (5 :Int)) example₃
300 :< (X -> 170 :< (λX -> 64 :< (λX -> 12 :< (λX -> 0 :< ...
```

# Hybrid automatic differentiation

In second-order optimization, it is often preferred to use a hybrid approach, i.e., combine forward mode and backward mode to get a more efficient algorithm. For instance, when taking a function's curvature into account, it is necessary to compute the Hessian¹¹ applied to a vector. Pearlmutter [31] introduces this mix of the two modes. In a forward sweep the first derivative is computed, whereupon the second, reverse sweep computes the second-order derivative at a point. This can be obtained by exploiting the d-module isomorphisms to work with

```
data Nᵢ v d = Nᵢ d (Dense v (d (<- (Cayley (Sparse v d)))))
```

# 6.5. Basic sharing of subexpressions

Our approach so far ignores any sharing in the source expression. Consider for instance example₄, which denotes the expression (x + x) · (x + x), but at the level of Haskell shares the two occurrences of x + x by means of a `let` binding.

```
example₄ :: Expr X
example₄ = let y = Plus (Var X) (Var X) in Times y y
```

The `eval` recursion scheme used by `abstractD` does not see the `let` binding and processes both occurrences of x + x. In particular, `abstractD (λX -> 5) example₄` reduces to (N 5 one ⊕ N 5 one) ⊗ (N 5 one ⊕ N 5 one) which features two (⊕) operations instead of one. To avoid this recomputation of intermediate results, we extend the symbolic expression language with a let-construct so that we can write example₄' with this new syntax.

```
data Expr v = ... example₄' :: Expr XY
| Let v (Expr v) example₄' = Let Y (Plus (Var X) (Var X))
(Expr v) (Times (Var Y) (Var Y))
```

We adapt the evaluator accordingly with the standard semantics for let-binding.

```
eval :: (Eq v, Semiring d) => (v -> d) -> Expr v -> d
...
eval gen (Let y e₁ e₂) = let d₁ = eval gen e₁;
gen₂ x = if x == y then d₁ else gen x
in eval gen₂ e₂
```

Observe that, because e₂ has the additional `let`-bound variable in scope, we evaluate it with the extended generator `gen₂`, which maps the free variables to their given `gen` meaning and the new `let`-bound variable `y` to the meaning `d₁` of `e₁`. The definition of `abstractD` is as before, now with support for sharing.

Sharing for sparse maps Now, `abstractD (λX -> 5) example₄'` reduces to an intermediate form with only one (⊕) operation, and if we commit for the tangent to the sparse module, this reduces further in a way that nicely preserves the sharing.

```
let y = N 5 ⊕ₑ N 5 one in (y ⊗ y)
≡ let y = N 5 (X -> 1) ⊕ₑ N 5 (X -> 1) in (y ⊗ y)
≡ let y = N 10 (fromList [(1, 2)]) in (y ⊗ y)
≡ N (10 x 10) (fmap (10 x) (X -> 2) @|fmap (10 x) (X -> 2))
```