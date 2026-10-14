```
-- HASKELL Applicative
class Functor f => Applicative f where ①
  pure :: a -> f a ②
  (<*>) :: f (a -> b) -> f a -> f b ③
```

① In Haskell, Constraints on classes have the same forward arrow as Constraints on functions.

② In Haskell, ∀ a is implied.

③ In Haskell, Binary Operators do not have to be aliased.

Notice how Haskell's Applicative has the same Typeclass Methods as PureScript's Apply and Applicative.

This is a minor difference, but we'll see that in PureScript, the decision was made to be a bit more granular with both Applicative and Monads.

Hopefully, this example is more proof that moving from PureScript to Haskell will be pretty easy compared to learning Functional Programming in the first place. Sort of like moving from Java to C#.

# 16.2. Applicative Functors in Category Theory

Unlike Functor, the Applicative Functor has it's origins in programming. But it does round out the Categorical Functor.

If you remember, Functor only maps Morphisms:

```
class Functor f where
  map :: ∀ a b. (a -> b) -> (f a -> f b) ①
```

① We've added the implied Parentheses here.

But in Category Theory, Functors map BOTH Morphisms and Objects: