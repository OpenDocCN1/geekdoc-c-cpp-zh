```
S = A finite set of states S
a = A finite set called the input alphabet Σ
Tuple s a = (s, a) ∈ S × Σ
```

The second Parameter to `foldl` is the initial State (Moore: start state, s₀).

`foldl`’s third Parameter is a `Foldable`, which contains the input values (Moore: input alphabet, Σ)

And the final Parameter to `foldl` is the Final State, which doesn’t have a direct parallelism to a Moore Machine. Our `foldl` simply returns the full Final State, but Moore has an output function **G : S → A** that extracts out the result. This corresponds to our `extract` function in our Fold Model from earlier.

Since a Moore Machine is slightly more general than Folds, we’re going to model a Moore Machine:

```
data Moore s a b = Moore ???
```

Here s is the State Type, a is the Input Type and b is the Output Type.

Let’s add the Initial State to our definition:

```
data Moore s a b = Moore s ???
```

Looking back at the definition for a Moore Machine, we’re only missing the Output Function and the Transition Function. So let’s first add the Output Function, i.e. a function that takes a State and produces an Output:

```
data Moore s a b = Moore s (s -> b) ???
```

Remember, s is the State Type and b is the Output Type. When folding, we’ll use this function to produce our final result. But in a Moore Machine, each State has an Output value.

This can be seen in the following State Diagram, which is an overly simplistic control of an Oven: