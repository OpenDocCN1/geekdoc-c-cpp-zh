![](bbox=[0.19, 0.055, 0.81, 0.335])

In PureScript, we can show that Composition is Associative:

```
compose :: ∀ a b c. (b -> c) -> (a -> b) -> (a -> c)
compose g f x = g (f x) ①
```

① This equation will be used in the following proof.

```
h ∘ (g ∘ f)               = (h ∘ g) ∘ f                 -- Given (Math)
compose h (compose g f) = compose (compose h g) f -- Given (PureScript)
h ((compose g f) x)      = compose (compose h g) f -- Subst left using ①
h ((compose g f) x)      = (compose h g) (f x)      -- Subst right using ①
h (compose g f x)        = (compose h g) (f x)      -- Remove Parentheses
h (g (f x))              = (compose h g) (f x)      -- Subst left using ①
h (g (f x))              = h (g (f x))              -- Subst right using ①
```

We have now shown how Types as Objects and Functions as Morphisms form a law-abiding Category. And after this very brief introduction to Category Theory, I hope you can see how Functional Language designers were influenced by this relatively new area of Mathematics (circa 1945).

# 12.10. Concrete Examples in Hask

Let’s look at some examples in Hask starting with the Show Method, show:

```
class Show a where
  show :: a -> String
```