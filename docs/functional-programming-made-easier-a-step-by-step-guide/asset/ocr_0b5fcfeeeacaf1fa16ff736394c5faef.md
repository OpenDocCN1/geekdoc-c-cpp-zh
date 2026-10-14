```
f :: c -> a
g :: b -> d
output :: s -> b
g <<< output :: s -> d ①
```

① Remember, we’re calling output first and then passing it’s return value of Type b to g.

The composition of the mapping function g with output gives us the Type we expect, i.e. b has been mapped to d and now we can update our code:

```
instance profunctorMoore :: Profunctor (Moore s) where
  dimap :: ∀ a b c d. (c -> a) -> (b -> d) -> Moore s a b -> Moore s c d
  dimap f g (Moore s0 output transition) = Moore s0 (g <<< output) ??? ①
```

① Call the original output function then transform the b to a d using g :: b -> d.

Finally, we’re ready to transform the Transition Function, s -> a -> s. But the a isn’t the first Parameter like we saw in the previous Chapter. We can’t simply compose f with transition since the Types won’t line up.

If transition had a Type Signature of a -> s, then we’d be able to compose it with f. To fix this, we’ll just have to pass an s to transition. By partially applying s to transition we get:

```
transition s :: a -> s
```

Let’s next add the mapping functions and their Types to this list:

```
transition s :: a -> s
f :: c -> a
g :: b -> d
```

It’s clear that g cannot be used to map transition s since they have no Types in common. But, f looks promising. So let’s compose them and add it to our list:

```
transition s :: a -> s
f :: c -> a
g :: b -> d
transition s <<< f :: c -> s ①
```

① Unlike the mapping of output, we call f FIRST, which is because f is Contravariant, i.e. maps INPUTS.