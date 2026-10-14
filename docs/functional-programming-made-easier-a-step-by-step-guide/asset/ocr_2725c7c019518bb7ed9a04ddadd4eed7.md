A Moore machine can be defined as a 6-tuple (S, S₀, Σ, Λ, T, G) consisting of the following:

A finite set of states S
A start state (also called initial state) S₀ which is an element of S
A finite set called the input alphabet Σ
A finite set called the output alphabet Λ
A transition function T : S × Σ → S mapping a state and the input alphabet to the next state
An output function G : S → Λ mapping each state to the output alphabet

Although the use of Greek letters can feel a bit foreign, if we look carefully we can see the parallels with our Fold definition:

```
s0 :: s            -- initial State
x :: a             -- input value
step :: s -> a -> s -- function called at each step
extract :: s -> r   -- function to extract result from Final State
```

s = A finite set of states S
s0 = A start state (also called initial state) S₀ which is an element of S
a = A finite set called the input alphabet Σ
r = A finite set called the output alphabet Λ
step = A transition function T : S × Σ → S
extract = An output function G : S → Λ

Notice how Types in a program are Sets in the Mathematical definition. That’s because Types have Inhabitants which are Sets of Values of that Type.

Let’s look at the Type Signature for foldl to see how Moore Machines relate:

```
foldl :: ∀ a s f. Foldable f => (s -> a -> s) -> s -> f a -> s
```

The first Parameter to foldl is the step function in our model (Moore: transition function, T : S × Σ → S). Notice how Moore’s definition is just a Cartesian Product of S and Σ, which is just foldl’s function uncurried, Tuple s a -> s: