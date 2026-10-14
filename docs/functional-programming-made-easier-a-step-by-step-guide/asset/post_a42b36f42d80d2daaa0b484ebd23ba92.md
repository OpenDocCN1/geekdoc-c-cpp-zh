
Use the following to test your code:

```
log "___________________________"
log $ show $ runPredicate (Predicate odd) $ 10
log $ show $ runPredicate (Predicate odd) $ 11
```

1 Helpful for delimiting our output since they're all Booleans.

2 Prints false.

3 Prints true.

Give it a try before reading on.

## 15.5. Code for runPredicate

Let's write the Type Signature first:

```
runPredicate :: ∀ a. Predicate a -> a -> Boolean
```

We take a Predicate a and a value a and return the result of that Predicate.

Notice that runPredicate is general, i.e. it will work with any Predicate. This is why we use the Polymorphic Parameter a.

Next, we write the function:

```
runPredicate :: ∀ a. Predicate a -> a -> Boolean
runPredicate (Predicate f) x = ???
```

1 We destructure Predicate using Pattern Matching to extract or unwrap the function.

Next, we simply just call that function:

```
runPredicate :: ∀ a. Predicate a -> a -> Boolean
runPredicate (Predicate f) x = f x
```

## 15.6. Writing Contravariant Instance for Predicate

We are now ready to write the Contravariant Instance.

First, add the following code to your test code:

```
log "________________________________"
log $ show $ runPredicate (cmap (_ + 1) (Predicate odd)) 10
log $ show $ runPredicate (cmap (_ + 2) (Predicate odd)) 10
log $ show $ runPredicate ((_ + 1) >$< (Predicate odd)) 10
log $ show $ runPredicate ((_ + 2) >$< (Predicate odd)) 10
```

1 Helpful for delimiting our output since they’re all Booleans.

2 Prints true.

3 Prints false.

4 Prints true.

5 Prints false.

Remember that (>$<) is the Binary Operator alias for cmap.

Notice that these tests cmap the function over the Predicate to augment the INPUT value BEFORE the Predicate function is executed.

You’ll also need to add these imports to keep the compiler happy:

```
import Data.Functor.Contravariant (cmap, (>$<))
```

Now write the Contravariant Instance for Predicate. Consult Pursuit to refresh your memory on Contravariant and look back at the previous Chapter for examples of writing such instances before moving on to the next section.

Also, keep in mind that cmap’s mapping function maps INPUTS.

## 15.7. Code for Contravariant Instance for Predicate

The instance code is very simple for Predicate. All we have to do is use cmap’s mapping function to map the INPUT to Predicate’s function. This can be accomplished using Function Composition:

```
import Data.Functor.Contravariant (class Contravariant, cmap, (>$<))

instance contravariantPredicate :: Contravariant Predicate where
  cmap f (Predicate g) = Predicate (g <<< f)
```

1 Import the Type Class Contrvariant.

2 We call f first to map the INPUT to something g expects.

Now run the test code and see what you get.

You should get:

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- contravariant
```

Add `contravariant` to `spago.dhall` and try again.

## 15.8. Folds and Moore Machines

Before we code Profunctors, let’s first model Folds in a Type, much like we did with `Predicates`.

The first step to modeling anything is to make sure we fully understand the thing we’re trying to model. Many times we can get a good overview by first look at the salient attributes of the thing we’re trying to model. So let’s list out the attributes of a Fold-Left Operation:

```
s0 :: s          -- initial State
x :: a           -- input value
step :: s -> a -> s -- function called at each step
```

When we’re finished with a `foldl` or `foldr`, we are left with the Final State of the operation. We don’t always want the full State but maybe a portion of it, e.g. we may have a Tuple in the State but we only want the `fst` of that Tuple since `snd` was just a working value.

Let’s add a function called `extract` to extract the final result we’re interested in. Realize that this function can always be `identity` when we want the Full State:

```
s0 :: s          -- initial State
x :: a           -- input value
step :: s -> a -> s -- function called at each step
extract :: s -> r  -- function to extract result from Final State
```

Here’s a diagram that shows the execution of a Fold:

![](img/8c0e9b687c62642e828ccb5481e11313_522_0.png)

Let’s breakdown the diagram:

+   - S is the set of States
+   - X is the set of Inputs
+   - step takes a current State, Sₙ and current Input, Xₙ and produces next State, Sₙ₊₁
+   - extract takes a State and extracts the result we’re interested in

It turns out that this model is very close to something called a Moore Machine. Moore Machine is a definition for a Finite State Machine.

State Machines are commonly used when writing code dealing with Protocols, Machine Control, Process Control, in fact, nearly anything we code can be modeled as a State Machine. However, some applications lend themselves to State Machine more than others.

These State Machines get their name from Edward F. Moore, whose 1956 paper, “Gedanken-experiments on Sequential Machines”, introduced the idea.

Here’s the definition of a Moore Machine from Wikipedia:

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
