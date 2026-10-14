Now modify_ should be easy. We can copy modify’s implementation making sure to change it to return unit as the Pure Computation:

```
modify_ :: ∀ s. (s -> s) -> State s Unit
modify_ f = State \s -> Tuple unit (f s)
```

Here’s the parallel computation diagram for State:

![](bbox=[0.322, 0.23, 0.677, 0.61])

In the diagram, get reads the current Monadic Computation’s result and makes it available to the Pure Computation channel. put, on the other hand, takes a Value and replaces the Monadic Computation with it.

# 18.22. Using State as a Monadic Validation

Earlier we considered making Validation a Monad but ran into problems writing bind. But now that we have the State Monad, we should be able to use it to collect errors. So let’s give it a try.

We’ll start with our example before we starting using Validation example: