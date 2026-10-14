![](bbox=[0.06, 0.05, 0.94, 0.42])

In the diagram, Functor F maps a to F a.

And now with pure from Applicative we finally have a way to map Objects:

```
class Apply f <= Applicative f where
  pure :: ∀ a. a -> f a
```

pure maps a into the Context, f a, which mirrors the way Functors map Objects between Categories.

Since an Applicative is also a Functor, it also maps Morphisms which makes it the Programming equivalent of Functors in Category Theory.

# 16.3. Apply Laws

Having the definition of Apply close to hand, will make understanding its single, yet complex, law much easier:

```
class Functor f <= Apply f where
  apply :: ∀ a b. f (a -> b) -> f a -> f b
```

Here's the one and only law for Apply: